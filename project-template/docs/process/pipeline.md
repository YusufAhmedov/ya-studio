# Design pipeline

The full path of a product: **raw idea → brief → research → PRD → Figma screens →
review**. Each stage builds on the previous artifact. That is the "method": the
designer owns the whole cycle, agents do the work under the coordinator's control.

> Output language: write all artifacts and talk to the user in **Russian** (see
> AGENTS.md → Language policy).

## Stages

### Stage 0 — Init (`/start`)
The coordinator gets to know the project: reads `inputs/idea.md`, interviews the
human if needed, records first decisions in `decision-log.md`, drafts `roadmap.md`,
then proposes the first step. Protocol: `docs/process/init.md`.

### Stage 1 — Strategist (research & requirements)
Goal: turn the idea into testable requirements.
1. `/brief` — structured 5-category dialogue → `outputs/brief.md`
2. `/research` — competitive analysis via web search → `outputs/research.md`
3. `/prd` — one-page PRD with MoSCoW scope + brand visual language → `outputs/prd.md`

**Stage output:** `prd.md` with audience, problem, scenarios, MoSCoW scope, visual
language, metrics. This is the contract for everything built afterwards.

### Stage 2 — System architect (build in Figma)
Goal: assemble the Must-scope screens from the design system.
- `/design` — the builder takes the Must screens from the PRD and assembles them in
  Figma **from library components** (Components 2.0 / Organism 2.0) on tokens (Tokens 2.0).
- Build & component rules: `docs/process/design-system-rules.md`.

**Stage output:** assembled screens in the project's Figma file.

### QA — Reviewer (`/review`)
Before delivery the senior reviewer audits the screens against the PRD and the
design-system rules, and writes `outputs/review-report.md` with a verdict
(Accepted / Accepted with fixes / Rejected). The reviewer fixes nothing — the builder
applies fixes per the report, then a re-review.

### Stages 3–4 — roadmap (out of scope for now)
- **Visual engineer:** generate and process visuals (illustrations, product photos).
- **Prototyper:** turn screens into an interactive prototype / code.
When we get there — add commands and roles separately.

## Coordinator loop ("What's next? / Proceed!")

The coordinator keeps the project in a clear state and at every step says what comes
next. One pass of the loop:

1. **Sync.** Read `brief / prd / decision-log / roadmap / parking-lot`; see what's done
   and what's next on the roadmap.
2. **Propose.** Name the single next step and which agent/command does it. If it hits
   a human gate — stop and ask the human.
3. **Run.** On "Proceed!" call the right subagent (builder / reviewer) or command.
4. **Accept.** Take the result, record decisions in `decision-log.md`, loose ends in
   `follow-ups/`, update statuses in `roadmap.md`.
5. **Quality gate.** Before calling a stage done — run `/review`.
6. **Report.** Briefly: what's done, what's next, open questions.

The coordinator **does not do the work itself** — it steers and calls executors. This
keeps contexts separate and stops the project from turning into a mess.

## Traceability

Everything is chained so "why is it like this" is always answerable:

```
idea.md → brief.md → research.md → prd.md → Figma screens → review-report.md
                              ↘ decision-log.md (why we decided so)
                              ↘ roadmap.md (what and in what order)
                              ↘ parking-lot.md (what we deferred)
```
