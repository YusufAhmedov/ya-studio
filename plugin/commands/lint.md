---
description: Быстрый структурный пре-чек экранов (Haiku, без скриншотов) перед полным /review
argument-hint: [ссылка на Figma-фрейм или node ID]
---

Launch the **design-lint** subagent (Task tool, `subagent_type: design-lint`).
Target: $ARGUMENTS (if empty — the screens from the current build task).

Flow: after each design-builder pass run `/lint` FIRST. If it finds structural issues —
send the lint report straight back to design-builder (cheap fix round). Only when lint
is clean — run the full `/review`. This saves the expensive reviewer pass for real work.

Relay to the user: findings count and whether screens are ready for `/review`.
