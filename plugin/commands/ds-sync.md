---
description: Синхронизация docs/design-system/ds-index.md с актуальными библиотеками Figma (ключи, компоненты, токены)
argument-hint: [что обновить: components | tokens | all — по умолчанию all]
---

Refresh `docs/design-system/ds-index.md` against the live Figma DS libraries.
Scope: $ARGUMENTS (default: all).

Method (main thread or a general-purpose subagent):

1. `get_libraries` — confirm the three official **alif tech** libraries are connected
   (Tokens 2.0 / Components 2.0 / Organism 2.0). If file keys differ from ds-index
   Section 1 — that's a migration: update Section 1 and flag it loudly to the user.
2. `search_design_system` filtered by `includeLibraryKeys` (keys in Section 1) — walk
   the component catalog, collect name + componentKey + variants. Update Section 6.
   Diff against the previous version: list added / removed / re-keyed components.
3. `get_variable_defs` on the Tokens file — update Section 2 (brand modes, bg/content
   tokens) and Section 3 (text styles) if changed.
4. Update the «Last updated» line with today's date and a one-line change note.
5. Also update the «Most-used component keys» quick-reference block in `CLAUDE.md`
   if any of those keys changed.

Report to the user in Russian: what changed, what broke (removed/re-keyed components
that agents may still reference), and whether builds in progress are affected.
