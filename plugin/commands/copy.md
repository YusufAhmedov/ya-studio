---
description: Аудит и написание UX-текстов — кнопки, заголовки, ошибки, пустые состояния (субагент ux-copywriter)
argument-hint: [экран / ссылка на Figma-фрейм; "apply" — применить прямо в Figma]
---

Launch the **ux-copywriter** subagent (Task tool, `subagent_type: ux-copywriter`) to
audit or write interface copy. Give it this context:

- Target: $ARGUMENTS — Figma frame / screen name. If empty, ask which screens to work on.
- Default output: copy document `outputs/copy-[screen].md`.
- If the user said "apply" — the agent may update Figma text nodes directly (text
  content only, never styles or layout).

When the subagent returns: relay the summary in Russian — issues found by type,
path to the copy doc, open questions for the product owner.
