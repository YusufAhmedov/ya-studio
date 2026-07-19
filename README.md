# YA Studio

Среда дизайн-команды для Claude Code: один дизайнер работает как целая студия.
Команда агентов ведёт задачу от анализа ТЗ до React-кода на дизайн-системе **alif-ui**.

## Структура репозитория

```
.claude-plugin/marketplace.json   ← маркетплейс (для /plugin marketplace add)
plugin/                           ← плагин ya-design: агенты + команды (общий слой)
│   ├── .claude-plugin/plugin.json
│   ├── agents/                    · 7 агентов (tz-analyst … design-lint)
│   └── commands/                  · /brief /design /review /code /lint /retro …
project-template/                 ← шаблон проекта (копируется под каждую задачу)
│   ├── CLAUDE.md                  · правила координатора
│   ├── docs/                      · ds-index, playbook, правила ДС, token-economy
│   ├── templates/  inputs/  outputs/
examples/                         ← заполненный пример артефактов
```

## Установка (каждый дизайнер, один раз)

```
/plugin marketplace add <GITHUB_USER>/ya-studio
/plugin install ya-design@ya-studio
```

После установки команды доступны в любом проекте:
`/design`, `/review`, `/wireframe`, `/copy`, `/code`, `/lint`, `/tz`, `/retro`, `/ds-sync`.

## Новый проект

1. Скопируй `project-template/` под новую задачу.
2. Положи идею/ТЗ в `inputs/`.
3. Открой папку в Claude Code → `/start`.

## Как устроено обучение среды

- Дизайнер после задачи запускает `/retro` → уроки пишутся в его проектные доки.
- Куратор (Юсуф) переносит стоящие уроки в этот репозиторий (playbook / token-economy /
  агенты) → версия плагина растёт → `/plugin update ya-design` у всей команды.
- Прямые правки агентов в обход репозитория запрещены — иначе процессы разъедутся.

## Обновление ДС

После изменений в Figma-библиотеках: `/ds-sync` в проекте → перенести обновлённый
`ds-index.md` в `project-template/docs/design-system/` в этом репозитории.
