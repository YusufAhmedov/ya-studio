# Alif UI — DS Index
> Compact reference. Read in seconds instead of three Figma API calls.
> **Update with `/ds-sync` when the design system changes.**
> Last updated: 2026-07-19 (migrated to **alif tech team** DS: new file keys, library keys, all componentKeys re-fetched)

---

## 1. Library files and keys

| File | Figma file key | Library key (for search) |
|---|---|---|
| ⚙️ alif tech Tokens 2.0 | `WpqrOClQnvecHvCoqsNMPW` | `lk-2040c65b1300364043a8c5218953761bc7f3dd7a651606c997e0f887189a18cb1275cc45f07adaac021a5845d8306a531d7e7bd2a7b8a74c4455cc46af1b01e8` |
| 💠 alif tech Components 2.0 | `w0iCAEcFuUdpG6HaYPLtsp` | `lk-abd4a4ef9b4615eb8431a1d0f32f721e620f7c6b72831dd06acd163e923ddbfa7f2d9e53c39e999579a9d032869f1a645ff7781791aa676e6122bf03fdf60a08` |
| alif tech Organism 2.0 | `0gDtMHhglMe2ZxAkpRTPwk` | `lk-4bf4e64552ea5f760ac06725b7fb08377c821ce1177d61ed13fb336e620f97833f8bb5181344dafbc7c840ee166b77aa53fdbe8451b1e152531de1443e38c8dc` |
| Working file | — | — (создаётся при старте задачи) |

> **Миграция 2026-07-19.** Команду разделили, ДС продублировали под новой командой **alif tech team**. Все три файла получили новые file/library/component keys. Старые ключи (Tokens `bBZRxNzF…`, Components `eXWrUxFG…`, Organism `q9CAeMgz…`) — **больше не использовать**.

> ⛔ **ТОЛЬКО эти три библиотеки (alif tech).** При поиске через `search_design_system` результаты включают и СТАРЫЕ версии библиотек (💠 Components 2.0 без «alif tech», ⚙️ Tokens 2.0, 💠 Components), и чужие ДС (Material 3, iOS, Simple Design System и др.) — **игнорировать всё, кроме alif tech**. Всегда фильтровать по `includeLibraryKeys` с тремя ключами выше. Различай по имени библиотеки: должно быть «alif tech» в названии.

---

## 2. Brands and colors

### Brand collection — режимы

Collection **Brand** `652feaa179b078ecfe31e88ff2151257d08df80f`.

| Mode | modeId | Note |
|---|---|---|
| `alif` | `10502:0` | font **ALS Hauss VF** — **does NOT work in MCP** (see below) |
| `universal` | `10502:1` | **font Inter — working mode for assembly** |
| `aliftech` | `10502:2` | |
| `mobi` | `16742:1` | |
| `other Brands` | `13533:0` | Вход в подколлекцию для сторонних брендов |

**Двухуровневая система брендов:** режим `other Brands` ведёт в отдельную подколлекцию, где есть свои параметры (Brand 1, Brand 2, Brand 3, other Brands 2…). Новые бренды (например Jewelry) добавляются туда — создаётся новый набор параметров с нужными цветами/шрифтами. После добавления всё, что собрано на токенах, перекрашивается автоматически.

### 🔤 Font blocker (important)

Brand font `ALS Hauss VF` **is not available in the MCP Figma environment** → instances of
any DS components with text cannot be created under the `alif` mode. Solution — use `universal`
mode (Inter). Details and code in `figma-build-playbook.md` §0.

### Background tokens — `brand/bg/*`

#### Страничные фоны

| Token | variableKey | Usage |
|---|---|---|
| `brand/bg/pagePrimary` | `aaf2e858af4cd3a8cf33a723a42aa9283d4d1beb` | Основной фон страницы |
| `brand/bg/pageSecondary` | `141b1f969ed96510b9c21358406ba78d693f2cda` | Вторичный фон страницы |
| `brand/bg/pageTertiary` | `82b8070b97886665547f5612bfc1b239f207706c` | Третичный фон страницы |

#### Поверхности (surface)

| Token | variableKey | Usage |
|---|---|---|
| `brand/bg/surface 1` | `b09d6267c504e754c7e8b702fc9b078628940bbc` | Карточки, панели |
| `brand/bg/surface 2` | `5064be7ffda398857b020d63e72eedf2f07f3921` | Чередующийся фон секций |
| `brand/bg/surface 3` | `118ca9c007e4b796dedfdd5000091f33245aedd3` | Плейсхолдеры, неактивные зоны |
| `brand/bg/surface 1 Transparent` | `79a455e1d4789eeb67987ee3bbcb771cb9cba293` | Прозрачный вариант surface 1 |
| `brand/bg/elevated` | `b5456bbb50bc6348caf049dd2e27ca829f286e15` | Плавающие карточки, модалки |

#### Семантические фоны

| Token | variableKey | Usage |
|---|---|---|
| `brand/bg/accent` | `c63c9d3821ed348af2861175be12e8e37be7ddb2` | Акцентный фон (бренд-тинт) |
| `brand/bg/success` | `c2e14cce21a052c2ee78e04abdcdae531fe8b5c8` | Успешное состояние |
| `brand/bg/warning` | `6635a5a7ee2191d41236594fc2dfd44a11ec4094` | Предупреждение (orange) |
| `brand/bg/danger` | `c9206e805963b9ba8a6f7d80c14c3c2233a9be94` | Опасность/ошибка (red) |
| `brand/bg/footerBg` | `d6f399d13c4a11788844d5d8bbe2d2386a8a74a3` | Фон футера |

#### Тинты (для фонов состояний с пониженной насыщенностью)

| Token | variableKey |
|---|---|
| `brand/bg/successTint 10` | `989873aa5cac2fcfb7460194d7341afd5f108966` |
| `brand/bg/successTint 20` | `2fbba8a88fe42f311f84ac268b0198759ba0b30d` |
| `brand/bg/successTint 40` | `b6c7aa0d5ffe6ab12f2225ade5b49cc4832f8d48` |
| `brand/bg/warningTint 10` | `6ea675b1b00f91eda584fd499eb56169ba3d230f` |
| `brand/bg/warningTint 20` | `02b2de0e1269a244ed768d5f41a1482ba28a422d` |
| `brand/bg/warningTint 40` | `f9202896aa3a760db0ad1f4731e4976933ab1348` |
| `brand/bg/dangerTint 10` | `bb97db37aa66bb7b51796e20bab33e392f5ff835` |
| `brand/bg/dangerTint 20` | `068d0062078120f46a1d852fd7b0a577ca7395e1` |
| `brand/bg/dangerTint 40` | `1dc43d1a40108b2ce8333aceb3673babde02aa72` |

### Text/icon colors — content tokens (Brand, Tokens 2.0)

**Rule: ALL text nodes and icon fills must use a `brand/content/*` variable. Never hardcode a color.**
Variables resolve automatically per Brand mode — no manual color decisions needed.

| Token | variableKey | Usage |
|---|---|---|
| `brand/content/default` | `d67feacf5fb58c2c03aba7733092935a0231d97e` | **Primary text and icons** — headlines, product names, nav labels, footer text |
| `brand/content/secondary` | `6db647786dd9f9cbde1a16fe200382d31d0e8b96` | **Secondary / muted text** — subtitles, placeholder labels, old price, meta |
| `brand/content/tertiary` | `76b57b8ab0cd1582f5fe41bb0c3c3638e640f96e` | Tertiary text — disabled labels, captions |
| `brand/content/accent` | `5ed341c1228a85243d8291f4d244b93f36d4f886` | **Brand-colored text/icons** — active tab, accent CTA label, highlighted value |
| `brand/content/link` | `8c2a2dd44b34d04e0149cc659a831ea46448c51b` | Hyperlinks, "See all →" function-button label |
| `brand/content/danger` | `913a12780bc878596d15502d84c94c67fffd62bc` | **Warning / orange** — предупреждения, не критичные состояния |
| `brand/content/error` | `c795444d68ee999265f044855e656a1ec5b8ff96` | Validation errors, destructive state labels |
| `brand/content/success` | `b57fd28d79a2cb602a181dbe12116ffa54fd15e3` | Success state labels |
| `brand/content/alwaysBlack` | `20e7e49c033bcab59b20ebe0ce1a4f2027f48843` | Text that must stay black in dark mode too |
| `brand/content/alwaysWhite` | `31d9d57fbe22b3cab2bf5bc766ffdcf069952945` | Text on dark/colored backgrounds (promo banner) |

### Quick decision: which content token?

| Context | Token |
|---|---|
| Page title, section heading, product name, nav link | `brand/content/default` |
| Price (main) | `brand/content/default` |
| Old/strikethrough price, installment caption, placeholder | `brand/content/secondary` |
| Disabled text | `brand/content/tertiary` |
| Active tab label, brand accent value | `brand/content/accent` |
| "See all →", footer links, breadcrumbs | `brand/content/link` |
| **Предупреждения (warning), не критичные** | `brand/content/danger` (orange) |
| Ошибки валидации, деструктивные действия | `brand/content/error` (red) |
| Скидка "−15%", акционный лейбл | `brand/content/error` или `brand/content/accent` |
| Text on promo banner (dark bg) | `brand/content/alwaysWhite` |
| All icons | same token as surrounding text context |


### Raw brand palette — `brand/brand` (Brand collection)

Базовые брендовые цвета. Используются внутри компонентных токенов. Меняются при смене режима (alif → jewelry).

| Token | variableKey | Usage |
|---|---|---|
| `brand/default` | `a7b04fb01937b610edfea5db30b9e85c087025a3` | **Основной бренд-цвет** — кнопки, активные состояния |
| `brand/hover` | `06543c66244f6256de0a73bb872188315d52782f` | Hover-состояние бренд-элементов |
| `brand/active` | `821a72424a1db0e9c4ca30411d5319d4e85c564c` | Active/pressed состояние |
| `brand/pale` | `6120fca2d3ad40cbb5c2ce792f8ea1b5bd97b9c7` | Очень светлый тинт бренда |
| `brand/tint 5` | `d529915aad01c703e82fecbe6286c7bdba8498ab` | 5% тинт |
| `brand/tint 10` | `0e03574242675b10a4f332a0f542f4239e7a8750` | 10% тинт |
| `brand/tint 20` | `b99343764f21c74572ea98951a9281973d8b1ab5` | 20% тинт |
| `brand/tint 40` | `4a19329d4dfef320bc8c83b4c36ac5dee02aaf1e` | 40% тинт |

### Border and semantic colors

| Token | variableKey | Hex (alif) | Usage |
|---|---|---|---|
| `brand/border/color/accent` | — | #00af66 | Accent border (green) |
| `brand/border/color/error` | `4c93d9b4b00b27aeb872de185a03fe23399df3e3` | #ec3d45 | Errors, danger states |
| `brand/border/color/link` | `7665f4ed458139c3c520e8bf966cb21a9f7ccf25` | #336bfd | Links |
| `brand/border/color/danger` | — | #ff9e00 | Warnings |

### Neutral scale reference values

| Primitive | Hex | Usage |
|---|---|---|
| solid/neutral/1000 | #ffffff | White |
| solid/neutral/920 | #f7f8f9 | Near-white background |
| solid/neutral/900 | #f0f2f4 | Light gray background |
| solid/neutral/~500 | ~#9e9e9e | Placeholder text, disabled |
| solid/neutral/~200 | ~#2d2d2d | Primary text |
| solid/neutral/0 | #000000 | Black |

> Exact values for 200–500 need to be verified via `/ds-sync`.

---

## 3. Typography

**Font: Inter** (confirmed from system)

| Style | Figma style name |
|---|---|
| Regular | `Inter, Regular` |
| Medium | `Inter, Medium` |
| Semi Bold | `Inter, Semi Bold` ← with a space! |
| Bold | `Inter, Bold` |

> In Figma Plugin API: `{ family: 'Inter', style: 'Semi Bold' }` — NOT `SemiBold`.

### Published text styles (⚙️ Tokens 2.0) — USE THESE, not raw Inter

All styles are from **⚙️ Tokens 2.0** library. Apply: `await node.setTextStyleIdAsync(style.id)`.
All are bound to variables → resolve per Brand mode (under `universal` = Inter).

**Style hierarchy (largest to smallest):**

```
display  →  heading (h1–h6)  →  body (l/m/s/xs)  →  description (l/m/s)
```

**Available weights:** Thin · Extra Light · Light · Regular · Medium · Semi Bold · Bold · Extra Bold · Black
(not all weights exist for every category — use what's available)

---

#### display — largest text (hero, promo headings)

| Style | styleKey |
|---|---|
| `Typography/display/l/Thin` | `a82309811c96424e0a6bb09e59ee8a723f30896e` |
| `Typography/display/l/Light` | `2b568f71ac8666f0f3612dbd8a01309d2263d8ca` |
| `Typography/display/l/Bold` | `71dd907447318eaef65ccd2a9a7b8718186fd157` |
| `Typography/display/l/Extra Bold` | `0c07d1007ac7aedc721efe727b71f3406c525d01` |
| `Typography/display/l/Black` | `437e62df4f5afb0bc7dae9dfa075d0a068d06f2d` |
| `Typography/display/m/Thin` | `ea838b53ddfed8dd4cb2b32c91305a0fc7b39605` |
| `Typography/display/m/Light` | `d504f07db1238234f31871665bae91d887c844d2` |
| `Typography/display/m/Medium` | `e20a5c12471d62090f966a376c9288fdc6e0591d` |
| `Typography/display/m/Bold` | `79405ffdd1dce791f73472816a40894324f332c9` |
| `Typography/display/m/Black` | `9f33d6108dbb504dcd6eaf5cfebb3959c5004b07` |
| `Typography/display/s/Thin` | `25a1410ec3adadbd17f1746377a08337e7f4b46e` |
| `Typography/display/s/Light` | `a8f39eff51cfa0607e52be8682f33e40fd39c567` |
| `Typography/display/s/Medium` | `95dfced6c839367a832679bba4639436f275f919` |
| `Typography/display/s/Bold` | `69df74a7108a00b6e162e4942c75a4cb39edd643` |
| `Typography/display/s/Black` | `d23d3179697c6a0d35dc7ec57c6627cb79d9981f` |

---

#### heading h1–h6 — section headings

| Style | styleKey |
|---|---|
| `Typography/heading/h1/Thin` | `cb976aa15d0db579bd890b735380247556f2249d` |
| `Typography/heading/h1/Light` | `53e8fc302f8c6ffb604b279ef76162c52b032813` |
| `Typography/heading/h1/Regular` | `7882206010db58411884106820015b980c5d013d` |
| `Typography/heading/h1/Medium` | `24197c8ddcd0a80d409e3e89a8e939024337f40c` |
| `Typography/heading/h1/Semi Bold` | `e85f3eea8df8c9f3d629db07b0c0d1227fd13736` |
| `Typography/heading/h1/Bold` | `acfe537754bb09c22a252cd76eaf59e267d39279` |
| `Typography/heading/h1/Extra Bold` | `34085f7e64170945f79d84886c217f3bf9996b85` |
| `Typography/heading/h1/Black` | `9f072a2524a84f887cd2e8866bebd9701bd23325` |
| `Typography/heading/h2/Thin` | `ee30d59ada81e79bbb4c1490cf4127776aa36de4` |
| `Typography/heading/h2/Light` | `f221a1ad0b5b7f5a3d27ec7f8960d55b80ee4e08` |
| `Typography/heading/h2/Semi Bold` | `03ae4268a7ee95a029d6cb6f8c7860b1bb6b2c0e` |
| `Typography/heading/h2/Bold` | `4ed76282dc8d7fa3a88977d64fcc012c3c17e94b` |
| `Typography/heading/h3/Thin` | `666a8714e58db48bf92b266022b81f120b94b03e` |
| `Typography/heading/h3/Semi Bold` | `4057b6018d0fdaf0439ef5172c5c76c78c31ef10` |
| `Typography/heading/h3/Bold` | `90e89d8860911d3fec3a2543f603776b02781e51` |
| `Typography/heading/h4/Thin` | `d6af8f16192a455d6f20eb8db395dc115472450b` |
| `Typography/heading/h4/Semi Bold` | `cb9fe5b7e30819f16ee821ff29cf69550f1f9c54` |
| `Typography/heading/h4/Bold` | `557db3845c7c465c354763b6d9b18e28b8a0adec` |
| `Typography/heading/h5/Thin` | `a43429834ac6bc7bc452ce6bbac6e74c95bd2f3c` |
| `Typography/heading/h5/Semi Bold` | `3e6232ee7fde354ea03936b11757c1d295f9629b` |
| `Typography/heading/h5/Bold` | `5a8f994170494ccca65a9a68cdd3c6961ec5ed69` |
| `Typography/heading/h6/Thin` | `a4d62c415c2cd42a7629dc3c406f86f214b7d377` |
| `Typography/heading/h6/Semi Bold` | `d9f4c7b918eec1527f78aad0b54c46889e11196e` |
| `Typography/heading/h6/Bold` | `7058d939918ac092b43bb84b91f701f9e4b41add` |

---

#### body — main UI text (l / m / s / xs)

| Style | styleKey |
|---|---|
| `Typography/body/l/Extra Light` | `b37474d7b73f2ca3ea61d419ae65d3a786e7f4ed` |
| `Typography/body/l/Semi Bold` | `e7109308f3291b87e05beec68cbc593074fdd762` |
| `Typography/body/l/Bold` | `8e91cf0937ae206aaacfc010a335bd8124b6698a` |
| `Typography/body/l/Extra Bold` | `a2fe61e466293e6a2db98cdaedb2ef8d9e66bde1` |
| `Typography/body/m/Regular` | `243b651cd9b9c7c1782e211169868e47f594bea2` |
| `Typography/body/m/Medium` | `8600c03a71b1921c831ab29dd1142b6e3e58b452` |
| `Typography/body/m/Semi Bold` | `cefb6e15b5d57d588639730cfb4f4b9a1dfa9bd3` |
| `Typography/body/m/Bold` | `f916854092690bda303fba0988ade00da606edee` |
| `Typography/body/m/Extra Bold` | `d13a2e43bd55ff1bc459e1edf8476de3d47990c6` |
| `Typography/body/m/Extra Light` | `d8b72d6736df96aec7bd72365ca3f9b4ece4584f` |
| `Typography/body/s/Regular` | `da476d343161a0f3524d926ee653262035c3cf41` |
| `Typography/body/s/Semi Bold` | `450cdd1e7b11bb6352febc0fafecda81c74eaa8a` |
| `Typography/body/s/Bold` | `abb61d04768b8cbd81253e69d61a0cceabfe8a03` |
| `Typography/body/s/Extra Bold` | `4b5ea6a1f4fda29bd6337cb475f74eb20ea11422` |
| `Typography/body/s/Extra Light` | `e61f99b4bfa82b122cb8c403aab8bd8593d4af5f` |
| `Typography/body/xs/Regular` | `309fa95224dd830947baddd585d97eb16888ff51` |
| `Typography/body/xs/Bold` | `b40c7bfde3c179ffc0fdb0b7be552eea409c14d9` |
| `Typography/body/xs/Extra Bold` | `8dc02e744bc7f19b13203fdbf16dadcb4fc5efa3` |
| `Typography/body/xs/Extra Light` | `c701612705e80cdb15fdad7a4451d7dd89dfd610` |

---

#### description — captions, small auxiliary text (l / m / s)

| Style | styleKey |
|---|---|
| `Typography/description/l/Thin` | `11f3ff57e6727e4038bd27b06cbcc14d4ee307e5` |
| `Typography/description/l/Light` | `f15c70ce2143c0e56f3a7d0045e01a0e1b224185` |
| `Typography/description/l/Medium` | `42464ab24bb3b70dbf8c45f2ebc04f2f00acc9e7` |
| `Typography/description/l/Bold` | `b160a508b2ca5eaa302552b7d362ef3b8bccc9fc` |
| `Typography/description/l/Extra Bold` | `e8b0473cbd394775b7d955b595f18410d1d3f6ba` |
| `Typography/description/l/Black` | `55e8d45c9708c102583a77452e59bdad24545571` |
| `Typography/description/m/Thin` | `c88f3d8e2ba67155a0f8db86c5d5384221c5d4f6` |
| `Typography/description/m/Light` | `c71dd0125b0d259eaeaf4ec5dea1f3b9098f8301` |
| `Typography/description/m/Medium` | `a52464ad7245c8bbce7685ef3f38f1bb94facb39` |
| `Typography/description/m/Bold` | `770e4c364a40dfa13617b5c84d292a6865031b95` |
| `Typography/description/m/Black` | `ff1447e0b4d446ea2068513fad82013d86e43226` |
| `Typography/description/s/Thin` | `68f267814abe737854902502fabda35615ffe6f5` |
| `Typography/description/s/Light` | `c4e7d64eefeaaf4e9bb9c86d2895457dfb99ace9` |
| `Typography/description/s/Bold` | `2f093d4370b34ad0409ab9173004ce49c4ba5470` |
| `Typography/description/s/Black` | `75a783a379e8a9019ce58b25dcbe3b37eb689deb` |

---

#### Quick cheat sheet — when to use what

| UI location | Recommended style |
|---|---|
| Hero banner, promo heading | `display/l` or `display/m` · Bold / Extra Bold |
| Page / section heading | `heading/h1` or `heading/h2` · Semi Bold / Bold |
| Card / block subheading | `heading/h3` – `heading/h4` · Semi Bold |
| Product name in card | `body/m/Medium` |
| Price (accent) | `body/m/Bold` or `body/m/Extra Bold` |
| Main text, description | `body/m/Regular` |
| Secondary text, labels | `body/s/Regular` |
| Strikethrough old price | `body/s/Regular` (+ strikethrough) |
| Installment caption, meta text | `body/xs/Regular` |
| Trust strip icon captions | `description/m/Regular` or `description/s` |

> Search styles: `search_design_system "typography heading h2"` (exact query).
> Apply: `await node.setTextStyleIdAsync(style.id)`. Clipping rules — figma-build-playbook.md §2,§5.

---

## 4. Spacing and grid

| Parameter | Value |
|---|---|
| Desktop width | 1440px |
| Side margins | 80px |
| Content area | 1280px |
| Column gap | 24px |
| Section gap | ~40–80px |

---

## 5. Border radius, width and shadows

### Border radius (`brand/border/radius/*`)

| Token | variableKey | Button/input size | Value (alif) |
|---|---|---|---|
| `brand/border/radius/grapefruit` | — | L (h=56px) | **12px** |
| `brand/border/radius/apple` | `e0bb4e14b5ac6a2ea6bbebe9020dec987a606cd7` | M (h=48px) | **12px** |
| `brand/border/radius/peach` | — | S (h=36px) | **12px** |
| `brand/border/radius/full` | `9a6628f9c551a7c9c95fbba1192176d0acca50fb` | Pill / badge / chip | 999px |
| `brand/border/radius/none` | `6373336331d7c96379a6edcc856e9dc41df89664` | No rounding | 0px |

> alif mode: grapefruit/apple/peach are all **12px**. Cards also 12px. Use `full` for badges, chips, avatar.

### Border width (`brand/border/width/*`, FLOAT → STROKE_FLOAT)

| Token | variableKey |
|---|---|
| `brand/border/width/none` | `afb64ebb0d5a564cb7c3bcaa73081922683d619a` |
| `brand/border/width/xxs` | `30220a2bd657ad8a1804c6a086219e2dcd26254a` |
| `brand/border/width/xs` | `5e39c0e2129cb8b9d421aba425216d05afcdc878` |
| `brand/border/width/s` | `7657e1fb9579d6ecfeada8bb3e3cdacf8f985872` |
| `brand/border/width/m` | `408327541c599783d5f5387b55f2f124e3d5f168` |
| `brand/border/width/l` | `b58b8079b3186159214fb4190c7e8e7ee7547fe4` |
| `brand/border/width/xl` | `1144241e8721d907bc7ff6127501da0fa5b20fd1` |
| `brand/border/width/2xl` | `bd1e6ee293a50aa7d6086a6c89dbb77b423f7ffc` |
| `brand/border/width/3xl` | `8162c0ff364e14a194711d58d5aedfebd633a62b` |

### Shadow styles (⚙️ Tokens 2.0, EFFECT type)

Apply: `await node.setEffectStyleIdAsync(style.id)`.

| Style | styleKey | When to use |
|---|---|---|
| `shadow/xs` | `89d927c603125c09163f239502c46cd9a35b63ce` | Минимальная тень — чипы, теги |
| `shadow/s` | `349ae0a1da485611c167a1d0da032f32f62fdb23` | Карточки товаров, плитки |
| `shadow/m` | `fa7fd90564f9763c0a4320766c1aab189ecd9e14` | Дропдауны, выпадающие меню |
| `shadow/l` | `64e094bf8abde58364ac5db8dcdba373ea680862` | Модалки, модальные шторы |
| `shadow/xl` | `e2342f510ecd9f0391cf92194441a564479a440f` | Floating panels, tooltips |

---

## 6. Components — catalog with keys

**Rule: ALWAYS check this catalog before building anything custom.**
Keys for `figma.importComponentByKeyAsync(key)`. All from **alif tech Components 2.0** unless marked [Org].
> 🔄 All keys below re-fetched 2026-07-19 from the alif tech libraries.

---

### Form / Input

| Component | componentKey | Variants |
|---|---|---|
| **Button** | `0e4cb5644de54c3f459d599ffcbf8bac207d4d29` | ⚠️ имя в новой ДС — «Button (current version)». Variant=Main/Outline/Ghost/FAB/Function · Color=Primary/Secondary/Tertiary/Success/Warning/Danger/Highlight · Size=L/M/S/Xs · State=Default/Hover/Pressed/Disabled/Loading/Focus |
| **Input** | `8c7b0ea4579432ab0d7a1e9568e34bf5ae674655` | Size=L/M/S · State=Default/Hover/Active/Filled Correct/Error/Disabled/Disabled Filled |
| **Select** | `4c10e0dcda7710c69cae6e542f046c3ffa53190b` | Size=L/M/S · State=Default/Hover/Active/Filled/Error/Disabled |
| **Search** | `28295f84a91dee39ecb1e9a132d4a61581c5208f` | Variant=Main/Accent/Filled · State=Default/Hover/Active/Filled/Disabled/DisabledFilled · Size=L/M/S · Button=True/False |
| **Checkbox** | `b0a158d28b38005bc237bf5798a3a7b5eb499522` | — use search_design_system for variant details |
| **Radiobutton** | `397358e3af2ce640934fa876ca4d06646087477d` | Label position=Right/Left · State=Default/Hover/Active/Disabled/Disabled Filled · Size=M/S |
| **switch** | `d417b39fb746d7b86d8ce8a968189500a40054dc` | Label position=Right/Left · Checked=Yes/No · State=Default/Hover/Disabled · Size=M/S |
| **textArea** | `f77a492181a6109aed8e5f5cbd8abb2889f64cfa` | — use search_design_system for variant details |
| selectMultiple | `aca77ede813e2a197540d7dca9b6c601eaaaa619` | — |
| selectorInput | `f35f9aa8b90158e0068994db3d3a491863cdb923` | — |
| selector | `3fc1e9cfcffe988f018d3110bdb10fe8badeac35` | — |
| Number input | `2845ae3c266055c390c1ea0b2459439fa8c9f95f` | — |
| InputOtp | `234fc9e253484ba3fde66bb446289dba38e8847f` | — |
| fieldItem (internal) | `aec0eee351bab48ac5673f656c2d58ceb3b569a9` | — |
| inputDate | `b0975bf8fe4c266e518c3eec8f63172aacc51338` | — |
| inputDateTime | `ab676dad5c991a964f9d36b80ab79acbc1e8f3a9` | — |
| inputTime | `7383f4b7f309e157e35afb39caecf8974bcd40b1` | — |
| PickerDate | `43bcfda7e386e97f2edf8681b505a7bb64aa672a` | — |
| rangeSlider | `c4e787655cc2ab9f038a5049edfb68dd560a380e` | — |
| Thumb (slider knob) | `[уточнить]` | Не найден в ре-синке — искать `search_design_system "Thumb"` при необходимости |

> **Button variants:**
> - `Main` — primary CTA (hero, card)
> - `Outline` — secondary with border
> - `Ghost` — tertiary, no bg, has padding
> - `Function` — text-link, no padding, no bg. Use for "See all →", breadcrumb links.
> - ⚠️ BOOLEAN prop IDs (`Label#…` · `Icon right#…` · `Icon left#…`) при дублировании ДС меняются — уточнять через `get_design_context` на инстансе, не хардкодить старые.

---

### Navigation / Structure

| Component | componentKey | Notes |
|---|---|---|
| **tab** | `d05ff76f8e024ba5183b3f38ce51b0b19bdedf4d` | ⚠️ Use for BOTH nav tabs AND chips (size/filter selectors). Never build custom chips. |
| **tabsMenu** | `1ddf9d758b9b7230313576efcea8980e33c5f936` | Container wrapping multiple tab instances |
| segmented control | `9f9865a9344f23eaf6f142b95b8581b7b326a370` | Сегментированный переключатель |
| **breadcrumbs** | `a9c9824037f866ed3668224029f34d9b04c86958` | Full breadcrumb trail |
| breadcrumb (item) | `4d0171157d8079be74dff949256b673b30f7a6ab` | Single item |
| breadcrumbDivider | `88d119f5b86b86acdd3268304005b8c8747f374f` | Separator between items |
| **Divider** | `49a428d22a6dc699eff747241075df0a69e5caae` | Replaces 1px separator rectangles |
| **Accordion** | `9ebaf653d14a3ca9c523ac581b7b050cc699ad83` | Collapsible content panel |
| **Pagination** | `c387c31ea70675d3a6a6d261c1f75f3b42ba59fa` | Full pagination control |
| Pagination v2 | `f0cdaa84de54067f23162b61708b774321cdf12a` | Updated version |
| Pagination items | `604b1090b456955222614970b9310ec43d4765c9` | Individual page number cell |
| Pagination Select | `f91215070ad899c45c3c7c76961d4d908950cec3` | Page-size dropdown in pagination |
| Next button | `4fceb5572fafde3f6cd73f7e668048be5344d4e0` | Prev/Next arrow button |
| backButton | `44dc82b68486458a57b7ce30e2c5607d1c489018` | Кнопка «назад» |

---

### Display / Badges / Tags

| Component | componentKey | Variants |
|---|---|---|
| **Badge** | `425772e7b740268a3c2221e175ec2e845bae7579` | Size=M/S/XS · Type=Primary/Secondary · State=info/success/neutral/warning/error/status-01..07 |
| Badge 2 | `5e6e78564db74d210e3ae8305b2dcaca86b785f1` | Alternative badge style |
| **tag** | `31683f25e7f9abc97ebb882e97485d31399c3d0f` | For labels, categories, status |
| tagss | `[уточнить]` | Не найден в ре-синке — искать по запросу при необходимости |
| **indicator** | `0291a368dfaff81a9166fad56f198f401fe85569` | Status dot / notification indicator |

---

### Avatar

| Component | componentKey | Notes |
|---|---|---|
| **Avatar** | `5cce6d2a21365fde4c73384b12c7f911d3c92478` | Profile picture / initials |
| avatarBadge | `99c866d6690c83629ce142c6ea73d8e331a75fc0` | Avatar + notification count |
| avatarGroup | `3cb5e1510f2c760512d54736613c6b690504c521` | Stacked avatars (multiple users) |
| avatarStatus | `6f7f80884f29637890afacacd2117ed39182b0bd` | Avatar + online/offline status dot |

---

### Rating

| Component | componentKey | Notes |
|---|---|---|
| **ratingIconGroup** | `c8d6da07861b78dc8f93a065484f5d6789dce96a` | Star group — use for product ratings |
| RatingIconContainer | `ef55a7a33a73014a08b6dd8f8a87c90619abc612` | Single star container |

---

### Loading / Progress

| Component | componentKey | Variants |
|---|---|---|
| **Loader** | `1348ec9f0516dc4f8b026827bf97cc41c8673cfd` | Color=Primary/Secondary/Contrast/Color · Size=XL(64)/L(48)/M(36)/S(24)/XS(16) |
| **Skeleton** | `1255ef6e14936e8c69d92581f843ace543781a9b` | Loading placeholder |
| skeletonAnimation | `8015ce587a7683a24529fd75749acf2520aaca5a` | Shimmer animation |
| **ProgressBar** | `cf042cf03f80d078796fad08db0e6fc52d65894c` | Progress bar |
| scrollBar | `5af8110147fc6be9c8ed0377fae92762a5198894` | Scrollbar |

---

### Overlays / Notifications

| Component | componentKey | Notes |
|---|---|---|
| **alert** | `0888a4f41cd375534d0c8b8e90d24043cab1e333` | Info/success/warning/error banner |
| **modal** | `82d8af6e3789b70efeb48653628194ffc8c92489` | General dialog |
| modalStatus | `baa4d90a796b6f8d66eff35da3d252054f864656` | Dialog with status icon |
| **tooltip** | `ab9540fae4e2a3bfd22ff86dc2d996de31d33efe` | Hover tooltip |
| **hint** | `95d653eb1bbfe9817abf66a485cf5dd6743ecb5a` | Inline hint text |
| **snackbar** | `[уточнить]` | [Org] Не найден в ре-синке — искать `search_design_system "snackbar"` при необходимости |
| **Drawer** | `997d7f015c4d0129ed53ad541b2e4abedeb15e5f` | [Org] Slide-in side panel |

---

### Lists / Menus / Data

| Component | componentKey | Notes |
|---|---|---|
| **List** | `8c0aa3623603d14992d1f0cfed96c1b98fa13738` | List container |
| List item | `94647e0ae2a3a545559c94062a870b1aa4730048` | Single list row |
| **Menu** | `5d16a5fd84b3bd43a729f9f982d24331ff4fb703` | Dropdown/context menu |
| menuItem | `3619bcb3d9723dc493ff095fc1dadccda9078191` | Single menu row |
| menuList | `070f335a7aa3e18a3bdd4c950f26786e32469a87` | Menu container |
| tableDetails | `6c10d153a4acfe80c2a84816e598e96c4e351818` | [Org] Detail table |

---

### Organism 2.0 — полный список

> ⚠️ Organism 2.0 содержит в основном табличные примитивы и несколько UI-организмов. Header/Footer/Hero/ProductCard — в этой библиотеке отсутствуют (строим из Components 2.0).

| Component | componentKey | Когда использовать |
|---|---|---|
| **headerSection** | `f7a166ad54e1a4fd974d62462dc8a1d2837dc608` | Шапка страницы с навигацией |
| **Quantity button** | `e3162853483e1e625c6136aede69450e3fb4c97d` | ⚠️ имя в новой ДС — «Quantity button (previous Button group)». +/− стeppер количества |
| **Drawer** | `997d7f015c4d0129ed53ad541b2e4abedeb15e5f` | Слайд-панель (фильтры, детали) |
| **fileUpload** | `51b3669defac99b1676b19b9c537f37b28e6cf37` | Зона загрузки файлов/изображений |
| fileUploader | `ab586381f683c3d3ae82b2b8fa297ba10f448c78` | Загрузчик файлов (расширенный) |
| **timer** | `d62b0d9688a3ea8068b38b2b2f6b2f8c441c1ae5` | Таймер обратного отсчёта (акция, OTP) |
| **Time** | `cb915c0a3672d03c99adc4ca98114d6f9224e4c7` | Отображение времени/метки |
| tableDetails | `6c10d153a4acfe80c2a84816e598e96c4e351818` | Детальная таблица (key-value) |
| Thead | `2dc790703cf1d82f10104924e119bb32c562ee00` | Заголовок таблицы |
| th | `e0bfc15dd4c84cafa819ba4cf5c986aba6635d8f` | Ячейка заголовка столбца |
| Tr | `b699b4d825219a34bbb6ca95cba69a3d971e6272` | Строка таблицы |
| td | `[уточнить]` | Не найден: таблица переработана — вместо td теперь `DataRow csd` (`57c12e003e0d6c86bb1ef5b871d5669989bc1d7a`) / `ColumnBase` (`8eda512530e14103e4455494c1466e61cbdbd4b3`) |
| textComponentForSlot | `939b017d44d90230ee64eb757f74fa984106d235` | Текстовый слот внутри organism-лейаута |
| sidebarItem | `8e50f55bdf688a60b4bd6d217ec136a1c1822f04` | Пункт бокового меню (новый в alif tech) |

> ⚠️ **Organism переработан** (2026-07-19). Табличные примитивы частично заменены: `td` → `DataRow csd` / `ColumnBase`; добавились `TableHeaderAlt`, `Y Label`, `Reply`, `fileView`, `uploading`. Для любых таблиц сверяйся с файлом через `search_design_system` перед сборкой.

---

### Icons — quick reference

All icons: `search_design_system` with icon name. Two styles: `Outline` and `solid`.
> 🔄 Перепроверенный набор (alif tech Components 2.0, 2026-07-19). Остальные иконки — искать по запросу.

| Icon | Style | componentKey |
|---|---|---|
| ShoppingBasket | Outline/System | `1edab68c1abda9b5200889baf5b8fb34f3606d7b` |
| CheckCircle | Outline/System | `984f72cd1aa74d2d0cde2b82780e46bd7fe92bce` |
| search | Outline/System | `546ce19177b9b1e49850e9d1c6b16b405f614fb2` |
| UploadCloud | Outline/System | `db30171d44fca2e2a90bda51f74aa48e5b1fe494` |
| ListView | Outline/System | `95e8bba9ecda7c83ea5d77f0e0b3156ecf462ae8` |
| GridView | Outline/System | `b30239577ce00968a752ee5eb2b67c2680671f85` |
| SideBar | Outline/System | `a37477e53529ce9880c1b838e6fcd94c2bdcb180` |
| User | Outline/System | `0048118290d13ecffe7ef736dab0f484685e3bcf` |
| MoreHorizontal | Outline/System | `2c2971c3f02d380d4f258ab6e9610aae1beea2d1` |
| Bell | Outline/System | `aed99a9ba1e65dfa3e09f4c9857efd600120a955` |
| Lock | solid/System | `1d786e08a403db6f8c0abde00cd861d3e07b6b50` |
| Menu (hamburger) | solid/System | `2d133e46982e81126823b594a7aa863f7af79c9d` |
| UploadCloud | solid/System | `f49dc84db3e1dbe1a5921e67e17e776aca182d29` |
| ListView | solid/System | `bd8c66beb0caea34fcba9c04b6c495e16ecf7817` |
| SideBar | solid/System | `6aab617dcb1d4c2c242fb19907d54d029fbcae0b` |
| MoreHorizontal | solid/System | `2dfdfe433e687ad368e53f98bca78b397fd06be2` |
| Check | solid/System | `b4611cc74be61d99230fb8563c0a64ac88975c58` |
| Star | solid/System | `71e86f4d1f73aa11fbe948cab8358e9f2098c7d6` |
| Calendar | solid/System | `4e5f18509e48e32f5f13595cc4f951b6357055b1` |
| ChevronLeft | solid/Navigation | `88b9e4ad9fc4ffb03b64a4ddcd75cf54acbd7982` |
| ChevronDown | solid/Navigation | `010a60e7274d6fc19fca3daab2a7eef576e518fa` |
| ChevronUp | solid/Navigation | `290eed76532e0dcac6ab9cb2db2a25ee780c5bbb` |
| DoubleLeft | solid/Navigation | `3550e2e36c03b0bb7494983bcbbe4e501729aeda` |

> For any icon not listed: `search_design_system "Outline / System / {IconName}"` or `"solid / System / {IconName}"` (фильтруй по alif tech Components 2.0).

---

## 7. Variable naming — structure

```
{component}.{element}.{property}.{variant}.{state}

Examples:
  button.main.bg.color.primary.default
  button.fab.bg.color.primary.hover
  button.ghost.border.color.primary.focus
  brand.bg.surface 1
  brand.border.radius.apple
  mode-bg.pagePrimary
```

### Token architecture — 4 levels

```
Global Tokens (Base)  →  Semantic Tokens (Mode)  →  Brand Tokens (Brand)  →  Component Tokens
solid.green-50           mode.solid.green-50          brand.brandValue-default   button-bg-color-primary-default
```

| Level | Collection | Modes | What's inside |
|---|---|---|---|
| **Global** | Base | — | Примитивы: solid, tint, size, borderRadius, borderWidth |
| **Semantic** | Mode | `light` / `dark` | Контекстные цвета (свет/темнота) |
| **Brand** | Brand | `alif` / `alifshop` / `aliftech` / `other Brands`¹ | brand/*, brand/content/*, brand/bg/*, brand/border/* |
| **Component** | — (inline) | — | Токены конкретных компонентов: button-bg-color-primary-default и т.д. |

¹ `other Brands` — вход в подколлекцию для внешних брендов (Brand 1/2/3…). Новый продукт (Jewelry и др.) добавляется туда как новый набор параметров — тогда весь UI перекрашивается при смене режима.

> **Правило:** никогда не брать значения из Global/Semantic напрямую. Всегда использовать **Brand**-токены — тогда при смене бренда всё перекрасится автоматически.

---

## 8. Icons

Icons in Components 2.0 are available in two styles:
- `Outline / System / {Name}` — e.g. `Outline / System / search`
- `Solid / System / {Name}` — e.g. `solid / System / Check`

Search via `search_design_system` with query = icon name.

---

## 9. Jewelry niche — specifics

| Parameter | Value |
|---|---|
| Brand color | `#ec3d45` (solid/red/500) |
| Accent (gold) | `#D0A954` — non-standard, add manually |
| Brand switching | Variable mode "jewelry" in Brand collection (to be confirmed) |
| Default mode during assembly | Use solid/red/500 as hardcode until the mode is added |

---

## 10. Updating the index (`/ds-sync`)

When the design system changes:
1. Run `search_design_system` for new components → update Section 6
2. Run `use_figma` + `importVariableByKeyAsync` → update Section 2
3. Update the date at the top of the file

**What NOT to read every time:** the contents of all Figma file pages — only this index.
