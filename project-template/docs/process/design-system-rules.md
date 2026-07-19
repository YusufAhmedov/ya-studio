# Design-system rules

This is the rubric the **builder assembles** by and the **reviewer checks** against.
The source of truth is our alif-ui 2.0 design system, connected to the Figma file via
three libraries:

- **⚙️ alif tech Tokens 2.0** (`WpqrOClQnvecHvCoqsNMPW`) — colors, typography, sizes, spacing, radii (variables).
- **💠 alif tech Components 2.0** (`w0iCAEcFuUdpG6HaYPLtsp`) — base components (Button, Badge, Select, Checkbox, icons, etc.).
- **alif tech Organism 2.0** (`0gDtMHhglMe2ZxAkpRTPwk`) — organisms screens are assembled from (sidebar, table rows `Tr`,
  table headers, Link, etc.).

> **ONLY these three libraries.** Never use components or icons from other libraries
> (aliftech-ui, ionic, MUW, Mobi UI, Tailwind UI, Material Kit, or any other library
> visible in `search_design_system` results). If a needed component does not exist in
> these three — build it custom and record the reason in `decision-log.md`.

---

## 1. Library component vs custom

**Rule.** If a suitable component exists in Components 2.0 or Organism 2.0 — use it as
an instance. Don't rebuild a button / input / badge / table row / menu item out of
plain frames and rectangles.

**A custom frame is allowed only if:**
- no suitable component exists in the library, **and**
- it is recorded in `docs/project/decision-log.md` with a reason.

**How the reviewer checks it (via the Figma tree):**
- A library component instance = a node of type `INSTANCE`.
- Hand-built custom = `FRAME` / `RECTANGLE` / `GROUP` / `TEXT` with no component link.
- A screen built mostly from `FRAME`/`RECTANGLE` where the library already has the
  component is a **violation** (severity: high).

---

## 2. Tokens, not hardcode

**Rule.** Colors, font sizes, spacing, radii — only via variables from Tokens 2.0.
Hardcoded hex (`#0A7D56`), arbitrary pixels, eyeballed sizes are violations.

**How the reviewer checks it:**
- Fills / strokes must reference variables (bound variables), not raw color.
- Text must use typography styles/tokens, not arbitrary sizes.
- `get_variable_defs` shows available tokens; a mismatch is a finding.

---

## 3. Reuse (DRY)

**Rule.** A repeating element = a component/instance, not copy-paste.

- An element appears **3+ times** (product card, order row, nav item, status badge) →
  must be one component multiplied as instances.
- The same block across screens (header, sidebar, footer) → a shared component.
- Copy-pasting identical layer groups instead of instances is a violation
  (severity: medium): it breaks maintenance — a fix must then be applied in N places.

---

## 4. Structure & hygiene

- **Auto-layout** on containers (no eyeballed absolute positioning). Floating elements
  (a badge over an image, a FAB over a card) are deliberately `layoutPositioning='ABSOLUTE'`
  with constraints — not the default for everything else.
- **Text is not locked to a fixed height.** A text node hugs its content; long text is
  capped with `maxLines` + ellipsis (`textTruncation='ENDING'`), so short text leaves no
  empty gap and long text truncates cleanly. Fixing a text node's height to force a fit is
  a violation (severity: medium). See `figma-build-playbook.md` §5.
- **8 px grid** for spacing and sizes.
- A **screen** is a fixed-size frame (1440×… for desktop, 375×… for mobile).
- **Meaningful layer/frame names** (`Header`, `OrderRow`, not `Frame 47`).
- One type scale and consistent spacing across all screens.

> **Operational how-to:** the *what* is here; the *how* (brand-font handling when the font
> is/ isn't available in the build env, applying text styles, binding colour variables,
> instancing components, truncation property order) lives in
> `docs/process/figma-build-playbook.md` — the builder reads it before assembling.

---

## 5. Requirement coverage & brand

- Every **Must** item in the PRD's MoSCoW table must have a screen/state.
- A missing Must item is a high-severity finding.
- The visual must match the PRD's **"Brand visual language"** block (tone, style,
  imagery, references).
- A niche theme (if the PRD declares an adaptive theme system) is checked against
  what's declared.

---

## Severity scale (for the reviewer's report)

| Severity | What it is | Examples |
|---|---|---|
| 🔴 High | Breaks the PRD contract or a design-system principle | Custom instead of a component, missing Must screen, hardcoded color instead of a token |
| 🟡 Medium | Doesn't break it, but hurts maintenance/consistency | Copy-paste instead of an instance, 8px grid broken, inconsistent typography |
| 🔵 Low | Cosmetics & hygiene | Layer names `Frame 12`, leftover empty groups |

## Verdict

- **Accepted** — no high-severity findings, only a few medium ones.
- **Accepted with fixes** — medium/low findings; list them, builder fixes, re-review
  doesn't block delivery.
- **Rejected** — there are high-severity findings; builder must fix and pass review again.
