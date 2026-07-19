# Token economy — rules to stop burning the 5-hour limit

Context: assembling 2 screens once consumed a full 5-hour limit (~40 min of agents).
Main cost drivers, in order: (1) expensive model on mechanical work, (2) screenshots
after every step, (3) `get_design_context` on huge nodes, (4) unbounded fix-loops,
(5) many small `use_figma` calls instead of one batched script.

## Rules (coordinator enforces these when dispatching)

### 1. Model per task — the biggest lever
- **design-builder, design-reviewer, ux-wireframer, ux-copywriter → Sonnet.**
  Assembly and audit are mechanical: the thinking already happened in the PRD and
  ds-index. Add `model: sonnet` to their frontmatter. Opus on a builder can cost ~5×
  more for near-identical output.
- Keep Opus (or main-thread model) only for: coordinator dialogue, brief/PRD strategy,
  ambiguous design decisions.

### 2. Read Figma cheap
- `get_metadata` (sparse outline) FIRST; `get_design_context` only on small, specific
  nodes — never on a whole page (25k-token truncation + waste).
- Re-use `ds-index.md` instead of re-crawling libraries — that's what it's for.

### 3. Screenshot budget
- **Max 1 screenshot per screen per build pass** (at the end), +1 after fixes.
  Not "after each meaningful step". Screenshots are image tokens — the silent killer.
- Reviewer: screenshot once per screen, then work from `get_metadata`.

### 4. Batch `use_figma`
- One big script per screen (imports → components → layout → content), not dozens of
  small calls. Every call round-trips the whole tool context.
- Test tricky API calls on ONE node before applying to all (avoid 10 failed retries).

### 5. Master-screen pattern
- Build screen #1 fully → run review → lock patterns (Header, Footer, cards as Figma
  components). Screens #2…N are then instance placement — cheap.
- Never build N screens in parallel before the first one passed review.

### 6. Cap the fix-loop
- Max **2** builder↔reviewer rounds. Still "Отклонено" after round 2 → stop, show the
  human the report and let them decide. Endless auto-loops are where limits die.

### 7. Context hygiene
- New task = new session (`/clear`). Don't drag yesterday's build log into today.
- Subagents already isolate context — keep it that way; don't paste huge Figma JSON
  into the main thread.

## Figma-first vs code-first — when to use which

| Deliverable | Path | Why |
|---|---|---|
| Screens for team review / handoff in Figma | Figma-first (current pipeline) | Figma is the contract |
| Working product screens | **Code-first on alif-ui** (`/code` from wireframe or PRD directly) | Text-only iteration, compiler feedback is free, no MCP payloads — several times cheaper |
| Quick UX exploration | HTML/code prototype or greyscale wireframe | Cheapest possible iteration |

**Avoid ping-pong** (code → Figma → edit → back to code → …): every crossing costs a
full translation and the two representations drift. Pick the source of truth per task;
cross the bridge once, in one direction, when the thing is approved.
