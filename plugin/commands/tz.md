---
description: Анализ дизайн-ТЗ — находит пробелы, формулирует вопросы к менеджеру → outputs/tz-analysis.md
argument-hint: [ссылка на Notion/Google Doc, путь к файлу, или напиши задачу текстом]
---

Launch the **tz-analyst** subagent to analyze the design brief.

Pass it:
- The input from `$ARGUMENTS` (URL / file path / text) — if empty, the agent will ask
- Context: save result to `outputs/tz-analysis.md`, write in Russian

When the agent returns, relay the verdict to the user:
- If "Можно начинать" → confirm and propose next step
- If questions remain → show the questions list so the designer can take them to the manager
