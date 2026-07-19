# Figma → alif-ui map

Замена Code Connect (недоступен на тарифе Professional). Маппинг компонентов Figma DS
на компоненты npm-пакета `alif-ui` (2.0 alpha). **design-engineer читает этот файл перед
генерацией кода и дополняет после каждой задачи.**

Формат: одна строка = один компонент. Props указываем только неочевидные.

| Figma-компонент (Components/Organism 2.0) | alif-ui | Ключевые props / нюансы |
|---|---|---|
| Button (current version) | `Button` | Function-вариант в Figma = текстовая ссылка → `variant`-проп уточнить по `.d.ts` |
| Tab / Chip | `Tab` / `Tabs` | в Figma один компонент и для вкладок, и для чипов-фильтров |
| Badge | `Badge` | |
| Search | `Search` | |
| Divider | `Divider` | |
| Pagination | `Pagination` | |
| Quantity button [Org] | — | [уточнить: нет прямого аналога в alif-ui 2.0 — проверить при первом использовании] |

## Незакрытые маппинги / кандидаты в DS-backlog

- (пусто — пополнять по мере работы)
