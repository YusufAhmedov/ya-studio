---
description: Построение low-fi wireframe в Figma — информационная архитектура и layout (субагент ux-wireframer)
argument-hint: [экран или флоу; опционально — ссылка на бриф/ТЗ]
---

Launch the **ux-wireframer** subagent (Task tool, `subagent_type: ux-wireframer`) to
plan the IA and build greyscale wireframes. Give it this context:

- Target screen/flow: $ARGUMENTS — if empty, take the Must scope from `outputs/prd.md`
  or ask the user what to wireframe.
- Context files: `outputs/brief.md`, `outputs/prd.md`, `outputs/tz-analysis.md` (those
  that exist).
- Greyscale only, no DS components — per the agent's own rules.

When the subagent returns: show the user the built screens (node IDs), key UX decisions,
and open questions. Wireframe must be **approved by the user** before `/design` —
this is a human gate. Record the approval in `docs/project/decision-log.md`.
