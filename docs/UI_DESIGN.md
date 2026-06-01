# UI Design System — Dark Fantasy

Визуальный язык интерфейса **projectSurvival**: мрачное фэнтези, выживание, износ и ритуальная эстетика — без «космического» glow и без яркого MMO-стиля.

**Кодовое имя стиля:** `Ash & Ember`  
**Настроение:** пепел, окисленное железо, тусклый янтарный огонь, костяной пергамент, релiquary-орнамент.

---

## Решения команды

| Вопрос | Решение |
|--------|---------|
| Primary accent | **Янтарь** (огонь, воск, свеча в темноте) |
| Орнамент | **Заметный** — reliquary-углы на панелях и меню |
| Заголовки | **Cinzel** (пока без замены) |

HP, danger и урон — **отдельно от Primary**, в бордово-ржавых тонах; янтарь только для действий и «живого» света UI.

---

## Принципы

1. **Темнее мира** — UI чуть темнее геймплея, чтобы не спорить с картой.
2. **Орнамент на якорях** — заметный filigree на меню и панелях; HUD остаётся чистым.
3. **Материальность** — металл, камень, воск; не плоский flat design.
4. **Янтарь = действие** — Primary и ключевой свет UI; не путать с HP/damage.
5. **Износ** — лёгкий noise, потёртые края; орнамент слегка «сбитый», не идеальный вектор.

---

## Цветовые токены

Используйте как **Linear Color** в UMG или заведите `DA_UIStyle` / Data Table.

| Token | HEX | Назначение |
|-------|-----|------------|
| `bg.void` | `#0A090C` | Фон экрана / затемнение мира |
| `bg.panel` | `#121018` | Панели, модалки |
| `bg.elevated` | `#1A1722` | Подложка кнопок, слоты |
| `border.iron` | `#4A4540` | Рамки secondary, dividers |
| `border.ironLight` | `#6B635A` | Hover-рамки |
| `text.primary` | `#E6DDD0` | Основной текст (кость) |
| `text.secondary` | `#9A9188` | Подписи, hints |
| `text.disabled` | `#5C5650` | Disabled |
| `accent.amber` | `#A67C2E` | Primary fill |
| `accent.amberHover` | `#C9943A` | Primary hover |
| `accent.amberPressed` | `#8B6922` | Primary pressed |
| `accent.amberGlow` | `#E8B040` | Свечение (30% opacity) |
| `accent.amberBorder` | `#7A5A20` | Primary border |
| `ornament.base` | `#5C5348` | Железо орнамента |
| `ornament.highlight` | `#8B7340` | Янтарный блик на орнаменте |
| `status.danger` | `#B85C28` | Предупреждения |
| `status.health` | `#6E2228` | HP bar (не Primary!) |
| `status.stamina` | `#6B5A38` | Stamina / выносливость |

---

## Типографика

| Роль | Шрифт | Размер | Weight | Примечание |
|------|-------|--------|--------|------------|
| **Display** | **Cinzel** / Cinzel Decorative | 32–48 | Bold | Заголовки меню, название игры |
| **Heading** | **Cinzel** | 20–24 | SemiBold | Заголовки панелей |
| **Body** | Crimson Text / Source Serif 4 | 16–18 | Regular | Описания, lore |
| **UI Label** | Inter | 14–16 | Medium | Кнопки, HUD |
| **Caption** | Inter | 12 | Regular | Hotkeys, мелкие подписи |

**Кнопки Primary:** Inter Medium, **ALL CAPS**, letter-spacing +1–2 px.  
**Кнопки Secondary:** обычный регистр, Inter Medium 14–16.

> Шрифты: Google Fonts → `Content/ProjectSurvival/UI/Fonts/`.

---

## Орнамент (Reliquary)

Заметный, но не мешает читать текст. Стиль: **кованые углы**, тонкие завитки, центральная янтарная вставка.

### Где используется

| Элемент | Орнамент |
|---------|----------|
| Main Menu / Pause | **Полный** — 4 угла + верхняя центральная дуга |
| Модалки, инвентарь | **4 угла** на рамке панели |
| Primary button | **Мини-кап** на левом/правом краю (24×24) |
| Secondary button | Нет |
| HUD | **Нет** (только тонкая iron-линия) |

### Визуальная схема панели

```
    ╭──◆──╮                              ╭──◆──╮
    │ filigree                          filigree │
    │                                             │
◆───┤         З А Г О Л О В О K (Cinzel)         ├───◆
    │                                             │
    │              [ content ]                    │
    │                                             │
    ╰──◆──╯                              ╰──◆──╯

    ◆ = T_UI_Ornament_Corner (64×64, iron + amber highlight)
    верхняя дуга = T_UI_Ornament_Top (optional, только main menu)
```

### Текстуры орнамента

| Asset | Размер | Описание |
|-------|--------|----------|
| `T_UI_Ornament_Corner` | 64×64 | Угол reliquary; iron `#5C5348` + янтарная точка `#8B7340` |
| `T_UI_Ornament_Top` | 128×32 | Дуга над заголовком (main menu) |
| `T_UI_Ornament_ButtonCap` | 24×48 | Вертикальный кап для Primary-кнопки |

**UMG:** 4× `Image` с flip (Render Transform Scale X/Y = ±1) в углах `WBP_Panel_Default`.  
Padding контента от края с орнаментом: **24 px** минимум.

---

## Кнопки — обзор

```
┌─────────────────────────────────────────────────────────┐
│  PRIMARY          │  SECONDARY        │  (будущее)     │
│  янтарь + glow    │  iron контур      │  Tertiary      │
│  + ornament cap   │  тёмный фон       │  text only     │
└─────────────────────────────────────────────────────────┘
```

Общие параметры:

| Параметр | Значение |
|----------|----------|
| Высота (меню) | **48 px** |
| Высота (HUD / компакт) | **36 px** |
| Min width | **160 px** (меню), **80 px** (HUD) |
| Horizontal padding | **24 px** |
| Corner radius | **3 px** |
| Border width | **1 px** |
| Transition (hover) | **120 ms** ease-out |

---

## Primary Button (`WBP_Button_Primary`)

**Когда использовать:** Play, Continue, Confirm, Craft — главное действие на экране.

### Внешний вид (Default)

```
◆╔══════════════════════════════╗◆  ← ornament cap + border #7A5A20
 ║ ░░░ warm top highlight ░░░  ║  ← white 10% → 0%, тёплый оттенок
 ║                              ║
 ║      Н А Ч А Т Ь И Г Р У     ║  ← #E6DDD0, Inter Medium, caps
 ║                              ║
 ◆╚══════════════════════════════╝◆
      fill: #A67C2E
      shadow: 0 4px 16px rgba(0,0,0,0.55)
      outer glow: #E8B040 @ 30%, blur 8px
```

| State | Fill | Border | Text | Дополнительно |
|-------|------|--------|------|---------------|
| **Default** | `#A67C2E` | `#7A5A20` | `#E6DDD0` | glow 30%, shadow 4px |
| **Hovered** | `#C9943A` | `#8B6922` | `#F5EDD8` | glow 40%, scale 1.02 |
| **Pressed** | `#8B6922` | `#6B4E18` | `#C9C0B4` | glow 15%, scale 0.98 |
| **Disabled** | `#3D3420` | `#2A2418` | `#5C5650` | no glow, caps dim |

### UMG-структура

```
WBP_Button_Primary (Button)
└── Overlay
    ├── Image [Background]       — T_UI_Button_Primary (9-slice)
    ├── Image [Glow]             — amber, hover only
    ├── Image [Highlight]        — warm top gradient
    ├── Image [OrnamentLeft]     — T_UI_Ornament_ButtonCap
    ├── Image [OrnamentRight]    — flip horizontal
    └── TextBlock [Label]
```

**Parent class:** `WBP_Button_Base` (состояния, звук).

---

## Secondary Button (`WBP_Button_Secondary`)

**Когда использовать:** Settings, Back, Cancel.

### Внешний вид (Default)

```
┌──────────────────────────────┐  ← 1px border #4A4540
│                              │
│        Настройки             │  ← #C9C0B4
│                              │
└──────────────────────────────┘
     fill: #121018 @ 85%
     без орнамента, без glow
```

| State | Fill | Border | Text |
|-------|------|--------|------|
| **Default** | `#121018` 85% | `#4A4540` | `#C9C0B4` |
| **Hovered** | `#1A1722` | `#6B635A` | `#E6DDD0` |
| **Pressed** | `#0A090C` | `#3A3530` | `#9A9188` |
| **Disabled** | `#0A090C` 50% | `#2A2824` | `#5C5650` |

### Отличие от Primary

- Iron-рамка, без янтарной заливки.
- **Без орнамента** — контраст с «священным» Primary.
- Hover светлеет рамку, не fill.

---

## Текстуры (9-slice)

`Content/ProjectSurvival/UI/Textures/`:

| Asset | Размер | Описание |
|-------|--------|----------|
| `T_UI_Button_Primary` | 64×64 | Янтарная заливка, warm noise, 9-slice 16px |
| `T_UI_Button_Secondary` | 64×64 | Тёмная заливка + iron border |
| `T_UI_Panel_Background` | 128×128 | Камень / потемневший пергамент |
| `T_UI_Noise` | 256×256 | Tileable overlay, 5–8% |
| `T_UI_Ornament_Corner` | 64×64 | Reliquary corner |
| `T_UI_Ornament_Top` | 128×32 | Дуга над title |
| `T_UI_Ornament_ButtonCap` | 24×48 | Боковой кап Primary |

Пока нет арта — **Solid Color + Border + placeholder Image** для углов; текстуры подставить позже.

---

## Звук и motion

| Событие | Feedback |
|---------|----------|
| Hover | тихий metallic tick |
| Click Primary | warm thud + wax/ember crackle |
| Click Secondary | iron click |
| Disabled click | muted knock |

**Animation:** Primary hover scale **1.02**, pressed **0.98**, 100ms.

---

## Расположение в проекте

```
Content/ProjectSurvival/UI/
├── Fonts/
├── Textures/
├── Widgets/
│   ├── WBP_Button_Base
│   ├── WBP_Button_Primary
│   ├── WBP_Button_Secondary
│   ├── WBP_Panel_Default      ← орнамент 4 угла
│   └── WBP_ProgressBar
├── Menus/
│   ├── WBP_MainMenu           ← panel + ornament top arc
│   └── WBP_PauseMenu
└── HUD/
    └── WBP_HUD_Main           ← без орнамента
```

---

## Пример: главное меню

```
┌───────────────────────────────────────────── bg.void + vignette ─┐
│         ╭──◆── PROJECT SURVIVAL ──◆──╮              Cinzel Display │
│         ╰────────────────────────────╯                             │
│                                                                  │
│              ◆╔════════════════════════╗◆                        │
│               ║    Н А Ч А Т Ь       ║  ← Primary (amber)      │
│              ◆╚════════════════════════╝◆                        │
│              ┌────────────────────────┐                          │
│              │      Продолжить        │  ← Secondary             │
│              └────────────────────────┘                          │
│              ┌────────────────────────┐                          │
│              │      Настройки         │                          │
│              └────────────────────────┘                          │
│              ┌────────────────────────┐                          │
│              │        Выход           │                          │
│              └────────────────────────┘                          │
└──────────────────────────────────────────────────────────────────┘
```

Spacing между кнопками: **12 px**.  
Заголовок в ornated frame: `WBP_Panel_Default` + `T_UI_Ornament_Top`.

---

## Чеклист для UI-разработчика

- [ ] Импорт **Cinzel** + **Inter**
- [ ] `WBP_Button_Base` — состояния, звук
- [ ] `WBP_Button_Primary` — янтарь + ornament caps
- [ ] `WBP_Button_Secondary` — iron, без орнамента
- [ ] `WBP_Panel_Default` — 4 corner ornaments + padding 24px
- [ ] Placeholder-текстуры орнамента (серые блоки → финальный арт)
- [ ] Тест на `Map_Test_UI` — все states + скриншот команде

---

## Разделение accent vs status

| UI элемент | Цветовая группа |
|------------|-----------------|
| Primary button, menu glow | `accent.amber.*` |
| HP bar | `status.health` |
| Low HP pulse, damage | `status.danger` / `status.health` |
| Stamina | `status.stamina` |

Янтарь = «можно нажать / живой огонь». Красный = «тело / боль / урон».
