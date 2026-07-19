---
description: Реализация утверждённых Figma-экранов в React-коде на alif-ui (субагент design-engineer)
argument-hint: [ссылка на Figma-фрейм или node ID; опционально — папка проекта]
---

Launch the **design-engineer** subagent (Task tool, `subagent_type: design-engineer`)
to implement approved Figma screens as React code. Give it this context:

- Target: $ARGUMENTS — Figma frame URL / node ID (if empty, take the screens accepted
  in the latest `outputs/review-report.md`).
- Use the **alif-ui** npm package, default `@alpha` (DS-first: no custom elements where
  alif-ui has a component). Check `docs/design-system/figma-to-code-map.md` first.
  Code Connect is unavailable on our Figma plan — don't call those tools.
- Target project folder: ask the user if not obvious from context.
- Verify: build must pass; compare rendered result against the Figma screenshot.

Gate: only screens with review verdict «Принято» / «Принято с правками» go to code.
If the screen wasn't reviewed — suggest `/review` first, but let the user override.

When the subagent returns, summarize in Russian: files created, components used,
custom deviations (→ `docs/follow-ups/parking-lot.md` as DS backlog), open questions.
Record decisions in `docs/project/decision-log.md`.
