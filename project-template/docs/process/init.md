# Init protocol (init-flow)

Triggered by `/start` on a fresh template copy. Job: introduce the coordinator to a
new project, adapt the docs, and hand control to the working loop.

> Talk to the user and write docs (roadmap, decision-log) in **Russian** (see AGENTS.md).

## Steps

### 1. Check state
- New project or continuation? Look at `outputs/` and `docs/project/`:
  - Empty → new project, continue the protocol.
  - Has `brief.md`/`prd.md` → project already running; don't re-init, go to the
    coordinator loop (`pipeline.md`).
- If `outputs/` still holds someone else's example or a previous project — suggest the
  human clear `outputs/` and `inputs/idea.md` before starting (but don't delete `examples/`).

### 1a. Pick and record the output-folder slug (every new project, no exceptions)
This workspace may host more than one project over its lifetime — every one of them
gets its own `outputs/<slug>/` (see "Output folder convention" in `CLAUDE.md`). This
applies **regardless of entry point** — whether the project starts from `inputs/idea.md`
via this protocol, or skips straight to `/tz` on an external ТЗ, or anything else.
1. Derive `<slug>` from the working product name (kebab-case, e.g. "Sebiston" → `sebiston`).
2. **Record it immediately** as the first line of a new `docs/project/decision-log.md`
   entry for this project (e.g. "Проект: Sebiston, папка outputs/sebiston/") — don't
   rely on holding it in conversation memory only; a future session (or this one after
   context compaction) must be able to read it back instead of re-guessing.
3. From this point on, every task you hand to an agent must name this folder explicitly
   (agent prompts expect `outputs/[project]/...` and will ask if you don't say).

### 2. Read the idea
Read `inputs/idea.md`. If it's empty or a placeholder — ask the human to add an idea
(or pick one from `ideas.md`).

### 3. Short interview (only what's missing from the idea)
Don't repeat what's already clear from `idea.md`. Ask only the gaps:
1. Working product name.
2. Primary user and their pain (one sentence).
3. Platform: web / mobile / desktop.
4. What we explicitly do **not** build in v1 (non-goals).
5. Which human gates matter most in this project.
6. Existing assets: a Figma file, a design system, links, notes.

If the human doesn't know an answer — propose a conservative default and mark it as an
**assumption** in the decision-log.

> Deep 5-category discovery is done not by init but by the `/brief` command in stage 1.
> Here — just enough for the coordinator to propose a sensible first step.

### 4. Adapt the docs
- `docs/project/roadmap.md` — sketch the order: stage 1 (brief→research→prd), then the
  Must screens to build, then review.
- `docs/project/decision-log.md` — record the first decisions and interview assumptions.
- If the human named assets (e.g. a Figma file key) — record them in the roadmap, but
  **do not record secrets/tokens** (only where to paste them).

### 5. Hand off to the loop
Report briefly to the human (in Russian):
```
Проект: [name] (outputs/[slug]/)
Идея понята: yes/no
Roadmap: drafted (stages and first screens)
Допущения: [list]
Важные human gates: [list]
Следующий шаг: run /brief
```
Then hand control to the coordinator loop (`docs/process/pipeline.md`) — propose the
first step and wait for "Proceed!".

## Done when
- The idea is read; gaps are closed or marked as assumptions.
- Roadmap and decision-log are filled for this project.
- The human has been given a clear next step.
