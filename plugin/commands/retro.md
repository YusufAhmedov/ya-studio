---
description: 10-минутное ретро после проекта/задачи — уроки в плейбук, правила в token-economy
argument-hint: [проект или задача — опционально]
---

Run a short retrospective in the main thread (no subagent). Scope: $ARGUMENTS or the
most recent completed task.

1. Read the recent `decision-log.md` entries and the latest `review-report.md` /
   `lint-report.md` for this task.
2. Ask the user 3 questions (in Russian, one message):
   - Что сломалось или потребовало ручного вмешательства?
   - Что съело больше всего времени/лимитов?
   - Что сделать правилом, чтобы это не повторилось?
3. Based on answers, append (with user's confirmation):
   - operational lessons → `docs/process/figma-build-playbook.md`
   - cost lessons → `docs/process/token-economy.md`
   - deferred ideas → `docs/follow-ups/parking-lot.md`
   - one summary entry → `docs/project/decision-log.md`

Keep additions to 1–3 lines each. The environment must learn, not bloat.
