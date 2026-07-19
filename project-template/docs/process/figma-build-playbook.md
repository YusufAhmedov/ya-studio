# Figma build playbook (operational "how")

Practical, code-level guidance for whoever drives `use_figma` (the **design-builder**
subagent, or the coordinator). `design-system-rules.md` says *what* the result must be;
this file says *how* to get there reliably with the Alif UI libraries. **Read this before
assembling.** Keys and token names live in `docs/design-system/ds-index.md` — this file
holds the procedures and the traps.

> Talk to the user in Russian; this doc is English on purpose (cheaper tokens, models
> follow it more reliably). See `CLAUDE.md` → Language policy.

---

## 0. Typography — the correct agent workflow

**How it works.** A new Figma text node defaults to **Inter**. The agent loads Inter,
writes the text content, then applies a DS text style via `setTextStyleIdAsync`. The style
is variable-bound: `fontFamily`, `fontSize`, `lineHeight`, `fontWeight` all resolve per
**Brand** mode. When the page Brand mode is `alif`, Figma renders the text in **ALS Hauss VF**
— verified live in Figma (2026-06-25): the font visibly changes from Inter to ALS Hauss VF
when brand is switched. The agent never needs to load ALS Hauss VF itself. The file is
correct and fully token-bound from the start.

**This is the standard process. No workarounds needed.**

> **Scope:** This workflow applies only when building within the **Alif Design System**
> (using DS text styles from Tokens 2.0). The DS style carries the font as a variable —
> that is what makes this work. If a task requires text in a custom font that is NOT in
> the DS (e.g. a one-off brand outside the three official libraries), cloud MCP will not
> have that font available and the task must be flagged to the designer.

```javascript
// ✅ Standard pattern — works in cloud MCP, correct result for the designer
const t = figma.createText();
parent.appendChild(t);

await figma.loadFontAsync({ family: 'Inter', style: 'Regular' }); // Inter is always available
t.characters = 'Текст';

const style = await figma.importStyleByKeyAsync('243b651cd9b9c7c1782e211169868e47f594bea2');
await t.setTextStyleIdAsync(style.id); // no font load required — applies style ID reference
```

**Key facts (verified: Figma docs + GitHub issue #1440 + live test):**

| Operation | Needs `loadFontAsync`? | Result in cloud MCP |
|---|---|---|
| `setTextStyleIdAsync(styleId)` | **No** | ✅ Applies style correctly |
| `t.characters = '...'` on a new node | Yes — load **Inter** | ✅ Works |
| `t.characters = '...'` after `setTextStyleIdAsync` | Yes — load **Inter** (font stays Inter in runtime) | ✅ Works |
| `createInstance()` of DS component with text internally | Yes (ALS Hauss VF, internally) | ❌ Fails |
| `.fontName` / `.fontSize` set manually | Yes | ❌ Never do this — use DS styles |

**DS component instances with text** — `createInstance()` fails when the component's
internal text uses ALS Hauss VF under `alif` mode. Workflow:
1. Check DS first — if the component exists, use an instance.
2. Text override via `setProperties(TEXT)` may fail — set it afterwards:
   ```javascript
   const textNode = inst.findOne(n => n.type === 'TEXT' && n.name === 'Label text#28:14');
   await figma.loadFontAsync({ family: 'Inter', style: 'Regular' });
   textNode.characters = 'Купить';
   ```
3. If no DS component exists — build from scratch with `figma.createText()` + pattern above.

**Never manually set `fontFamily`, `fontSize`, `fontWeight`.** Always use `setTextStyleIdAsync`.
Style keys are in `ds-index.md` Section 3.

**NEVER call `setExplicitVariableModeForCollection` from code — not on frames, not on
instances.** The Brand mode is set by the designer at the **page level** via Figma's
Design panel (right-click page → Brand → select mode). Figma cascades it automatically
to every node. Any programmatic mode assignment creates an explicit override badge that
overrides the page-level setting and blocks the designer from switching brands later.

```javascript
// ❌ WRONG — never do this:
// rootFrame.setExplicitVariableModeForCollection(col, '10502:1');
// inst.setExplicitVariableModeForCollection(col, '10502:1');

// ✅ CORRECT — do nothing. Designer sets Brand mode in Figma UI. Your code only creates
// nodes, applies DS text styles and variable-bound fills.
```

**If override badges are present** (from a previous bad build run), clean them:
```javascript
const v = await figma.variables.importVariableByKeyAsync('b09d6267c504e754c7e8b702fc9b078628940bbc');
const col = await figma.variables.getVariableCollectionByIdAsync(v.variableCollectionId);
const toClean = [rootFrame, ...rootFrame.findAll(n => n.explicitVariableModes &&
  Object.keys(n.explicitVariableModes).length > 0)];
for (const n of toClean) try { n.clearExplicitVariableModeForCollection(col); } catch {}
```

**Brand collection** `652feaa179b078ecfe31e88ff2151257d08df80f`, modes:
`alif`=`10502:0` (ALS Hauss VF), `universal`=`10502:1` (Inter), `aliftech`=`10502:2`,
`mobi`=`16742:1`, `other Brands`=`13533:0`. No "jewelry/red" mode yet — the designer
will add it later; token-bound elements repaint automatically when it's added.

**Brand colour rule (always).** Never hardcode a brand colour (e.g. `#ec3d45`) onto a DS
instance. Keep everything bound to tokens — when the designer adds a "jewelry" Brand mode,
every token-bound element repaints automatically. Hardcoding breaks that.

---

## 1. Inspect a component before you instantiate it

Variant and boolean property **keys carry suffixes** (`Icon right#28:7`, `Label#18748:0`)
— never guess them. Import the set and read the definitions first:

```javascript
const set = await figma.importComponentSetByKeyAsync(KEY);
console.log(JSON.stringify({
  propDefs: set.componentPropertyDefinitions,
  variants: set.children.map(c => c.name).slice(0, 80),
}, null, 2));
```

Then create and configure:

```javascript
const inst = (set.defaultVariant || set.children[0]).createInstance();
parent.appendChild(inst);
inst.setProperties({ 'Variant':'Main', 'Color':'Primary', 'Size':'M',
                     'Label#18748:0': false, 'Icon right#28:7': false });
```

Swap an instance-swap icon by component id:
```javascript
const icon = await figma.importComponentByKeyAsync(ICON_KEY);
inst.setProperties({ 'Icon left variant#28:29': icon.id });
```

### Import access — when it works and when it doesn't

`importComponentSetByKeyAsync` / `importComponentByKeyAsync` require **write access** to the
document. Write access is available when:
- Figma Desktop is open and the file is in **Edit mode** (not Dev Mode), OR
- The file is open in Figma Web in Edit mode.

In Dev Mode (read-only) these calls are blocked. If the call fails, use the `findAll()`
fallback below to locate and clone existing instances already in the document.

**`findAll()` fallback — clone an existing instance:**
```javascript
// Find any existing Button instance already in the document
const existing = figma.root.findAll(n =>
  n.type === 'INSTANCE' &&
  n.mainComponent?.name?.includes('Button')
)[0];
if (existing) {
  const clone = existing.clone();
  clone.setProperties({ 'Variant': 'Function', 'Size': 'S' });
  parent.appendChild(clone);
}
```

Use `figma.root.findAll()` (not `figma.currentPage.findAll()`) to search all pages —
the component you need may already be used on another page.

---

## 2. Typography = DS text styles, ALWAYS. No exceptions.

**Rule: every text node must have a DS text style applied via `setTextStyleIdAsync`.
Never set `fontFamily`, `fontSize`, `fontWeight`, `lineHeight` manually.**
The style resolves all those properties automatically per Brand mode.

Text style keys are in `ds-index.md` Section 3. Quick lookup:

```javascript
// Import a style by key and apply it
const style = await figma.importStyleByKeyAsync('243b651cd9b9c7c1782e211169868e47f594bea2'); // body/m/Regular
await figma.loadFontAsync({ family: 'Inter', style: 'Regular' }); // needed for .characters, NOT for setTextStyleIdAsync
textNode.characters = 'Your text';                                  // set characters BEFORE or AFTER — both work
await textNode.setTextStyleIdAsync(style.id);                       // no font load required
```

**Role → style cheat sheet (most common):**

| Role | Style name | styleKey |
|---|---|---|
| Page / section heading | `heading/h2/Semi Bold` | `03ae4268a7ee95a029d6cb6f8c7860b1bb6b2c0e` |
| Card / block subheading | `heading/h4/Semi Bold` | `cb9fe5b7e30819f16ee821ff29cf69550f1f9c54` |
| Product name in card | `body/m/Medium` | `8600c03a71b1921c831ab29dd1142b6e3e58b452` |
| Price (accent) | `body/m/Bold` | `f916854092690bda303fba0988ade00da606edee` |
| Body / description text | `body/m/Regular` | `243b651cd9b9c7c1782e211169868e47f594bea2` |
| Secondary text, labels | `body/s/Regular` | `da476d343161a0f3524d926ee653262035c3cf41` |
| Old price (strikethrough) | `body/s/Regular` | `da476d343161a0f3524d926ee653262035c3cf41` |
| Installment, meta caption | `body/xs/Regular` | `309fa95224dd830947baddd585d97eb16888ff51` |
| Nav links, footer labels | `body/m/Regular` | `243b651cd9b9c7c1782e211169868e47f594bea2` |
| Trust strip captions | `description/m/Medium` | `a52464ad7245c8bbce7685ef3f38f1bb94facb39` |

Load all needed Inter weights before applying styles:
```javascript
for (const s of ['Regular','Medium','Semi Bold','Bold']) {
  await figma.loadFontAsync({ family: 'Inter', style: s });
}
```

---

## 3. Colors = bound variables, ALWAYS. No hardcode, no hex.

**Rule: ALL text fills, icon fills, and shape fills must be bound to a DS variable.
Never write a hex value. The variable resolves the correct color per Brand mode automatically.**

Full variable list is in `ds-index.md` Section 2.

**Bind a variable to any fill (text, shape, icon):**
```javascript
const v = await figma.variables.importVariableByKeyAsync(VARIABLE_KEY);
let paint = { type: 'SOLID', color: { r: 0, g: 0, b: 0 } };
paint = figma.variables.setBoundVariableForPaint(paint, 'color', v);
node.fills = [paint];
```

**Quick decision — which content variable?**

| Context | Variable | variableKey |
|---|---|---|
| Headlines, product names, nav labels, icons | `brand/content/default` | `d67feacf5fb58c2c03aba7733092935a0231d97e` |
| Old price, captions, placeholder text | `brand/content/secondary` | `6db647786dd9f9cbde1a16fe200382d31d0e8b96` |
| Active tab, brand accent text/icon | `brand/content/accent` | `5ed341c1228a85243d8291f4d244b93f36d4f886` |
| "See all →", links | `brand/content/link` | `8c2a2dd44b34d04e0149cc659a831ea46448c51b` |
| Discount "−15%", error labels | `brand/content/danger` | `913a12780bc878596d15502d84c94c67fffd62bc` |
| Text on dark/colored bg | `brand/content/alwaysWhite` | `31d9d57fbe22b3cab2bf5bc766ffdcf069952945` |

Prefer a DS component over a hand-built coloured shape: e.g. a discount chip = **Badge**
instance (`Type=Secondary, State=error`) — contrast and colours are handled inside it,
and it repaints with the brand mode.

---

## 4. Auto-layout always; floats are explicitly absolute

Containers use auto-layout (`layoutMode`, `itemSpacing`, padding, `layoutSizing*`). Set
the parent's `layoutMode` first, then children sizing (`layoutSizingHorizontal='FILL'`
etc.). Elements that overlap the flow (badge over an image, a FAB over a card) are
`layoutPositioning = 'ABSOLUTE'` with `constraints` (e.g. `{horizontal:'MAX', vertical:'MAX'}`),
positioned after layout settles.

---

## 4a. Dynamic content — use Hug, not fixed size

**Rule.** If the content inside a container can change at runtime — text grows, a button
appears or disappears, the number of items varies — **never set a fixed width or height**
on that container. Use `layoutSizing = 'HUG'` so the frame expands with its content
instead of clipping it.

**Fixed size is allowed only when:**
- the element has a hard layout constraint (e.g. a full-bleed image, a fixed-width
  sidebar), **or**
- you explicitly want to truncate overflow (then pair with `overflow: hidden` and document
  why).

**Decision rule — ask yourself before setting a size:**
> "Can the content inside ever be larger or smaller than this number?" If yes → Hug.

```javascript
// Container that wraps dynamic content (card info block, button row, tag list)
frame.layoutMode           = 'VERTICAL';   // or HORIZONTAL
frame.layoutSizingVertical = 'HUG';        // height follows content
frame.layoutSizingHorizontal = 'FILL';     // stretches to parent width

// Child text node — always hug height, fill width
textNode.layoutSizingHorizontal = 'FILL';
textNode.textAutoResize          = 'HEIGHT';  // height follows text

// Fixed size only for a deliberately constrained slot (e.g. image placeholder)
imageFrame.layoutSizingHorizontal = 'FIXED';
imageFrame.layoutSizingVertical   = 'FIXED';
imageFrame.resize(width, height);
```

**Common trap:** after instancing a DS component, Figma sometimes keeps a fixed size
from the master variant. Always re-check `layoutSizingHorizontal/Vertical` on newly
created instances and override if needed.

---

## 5. Text height: don't lock it; cap with maxLines

Never freeze a text node to a fixed height "to make it fit". Let it hug, and cap long
text to N lines with an ellipsis. **Property order matters** — set truncation, *then*
`maxLines`, or the height sticks at one line:

```javascript
textNode.layoutSizingHorizontal = 'FILL';
textNode.textAutoResize = 'HEIGHT';
textNode.textTruncation = 'ENDING';   // FIRST
textNode.maxLines = 2;                // THEN  (lineHeight 24 → 1 line=24, 2 lines=48)
```

Short text → no empty gap; long text → 2 lines + "…".

---

## 6. Verify visually

After each meaningful change, `get_screenshot` the node and actually look at it. The
`use_figma` log says "added", the screenshot says whether it's *right* (contrast, wrapping,
position, brand colour). Download via the returned URL and read the PNG.

---

## 7. Keep the approved wireframe (normal practice, not a hard gate)

The usual flow: wireframe → show it → after approval, **leave it as-is and start the
Hi-Fi on a new page**. Either copy the wireframe frames onto a new Page and build there
without touching the originals, or just begin fresh on a new sheet. The point is simply
that the approved wireframe stays intact — so if a question comes up later ("what did we
actually approve?", or a designer wants to see where it started), the evidence is still
there. It's a sensible default, not a strict rule to police. Verify real node ids first
(`get_metadata`) — stored ids drift.

---

## 8. Wireframe styling: greyscale only

When building a **wireframe** (not Hi-Fi), use white/grey tones only — neutral surfaces
(`brand/bg/surface 1|2|3`), grey text, plain placeholders. **No bright or brand colour at
this stage.** Convey buttons/accents by shape and position, not colour. Colour (brand,
accents, real components) arrives only at the Hi-Fi stage. Rationale: a wireframe is about
structure and hierarchy; colour there distracts and prematurely "decides" the visual.

---

*This playbook grows. When you hit a new DS trap and solve it, add the procedure here so
the next builder (and the next designer) doesn't rediscover it.*
