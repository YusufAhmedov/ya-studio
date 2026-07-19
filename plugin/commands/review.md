---
description: Ревью собранных макетов синьор-ревьюером → outputs/review-report.md (субагент design-reviewer, read-only)
argument-hint: [Figma-файл/экраны — опционально]
---

Launch the **design-reviewer** subagent (Task tool, `subagent_type: design-reviewer`) to
audit the assembled screens. Give it this context:

- Review against `outputs/prd.md` + `docs/process/design-system-rules.md`; report format
  in `templates/review_report.md`; write the verdict to `outputs/review-report.md` (Russian).
- Target Figma file/screens (if specified): $ARGUMENTS — otherwise ask which to review.
- The reviewer is strictly read-only: it inspects and reports, it fixes nothing.

When the subagent returns, relay the verdict and finding counts to the user in Russian.
If the verdict is "Отклонено" or "с правками", propose running `/design` to apply fixes,
then a re-review.
