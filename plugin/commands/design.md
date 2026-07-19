---
description: Сборка экранов Must-скоупа в Figma из дизайн-системы (субагент design-builder)
argument-hint: [конкретный экран — опционально]
---

Launch the **design-builder** subagent (Task tool, `subagent_type: design-builder`) to
assemble screens in Figma. Give it this context:

- Build the Must-scope screens from `outputs/prd.md`, following `docs/process/design-system-rules.md`.
- Target screen (if specified): $ARGUMENTS — otherwise go through the Must scope in order.
- Build from library component instances (Components 2.0 / Organism 2.0) on Tokens 2.0;
  no custom where a component exists; repeating elements as components, not copy-paste.

When the subagent returns, summarize its result to the user in Russian, record any
decisions in `docs/project/decision-log.md`, and propose the next step (usually `/review`).
