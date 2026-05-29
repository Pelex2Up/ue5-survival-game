# projectSurvival

Survival-игра на **Unreal Engine 5.7**. Команда из 3 человек.

**Репозиторий:** https://github.com/Pelex2Up/ue5-survival-game

## Статус проекта

| Готово | В работе (Sprint 1) |
|--------|---------------------|
| Git + Git LFS + GitHub | Игровой скелет (GameMode, персонаж, карта) |
| Структура `Content/ProjectSurvival/` | Распределение зон между участниками |
| Документация и workflow | Базовое управление и камера |
| Ветки `main` / `dev` | Прототипный уровень |

→ Чеклист первого спринта: [docs/SPRINT_01.md](docs/SPRINT_01.md)

## Быстрый старт

### Требования

- Unreal Engine **5.7** — одна и та же версия у всех
- [Git](https://git-scm.com/) + [Git LFS](https://git-lfs.com/)
- Доступ к репозиторию на GitHub (collaborator)

### Первый клон

```bash
git clone git@github.com:Pelex2Up/ue5-survival-game.git
cd ue5-survival-game
git lfs install
git lfs pull
git checkout dev
```

HTTPS-вариант:

```bash
git clone https://github.com/Pelex2Up/ue5-survival-game.git
```

Открыть `projectSurvival.uproject` в Unreal Editor. При первом запуске согласиться на rebuild, если редактор попросит.

### Настройка редактора (один раз)

1. **Edit → Plugins → Git Source Control** — включить, перезапустить редактор
2. **Edit → Source Control → Connect to Git** — выбрать репозиторий
3. Убедиться, что Content Browser открывается в `/Game/ProjectSurvival`

### Ежедневный цикл

```bash
git checkout dev
git pull
git lfs pull
# ... работа в редакторе ...
git status
git add .
git commit -m "feat: краткое описание"
git push
```

Для отдельной задачи — feature-ветка (см. [docs/COLLABORATION.md](docs/COLLABORATION.md)).

## Структура Content

Весь игровой контент — в `Content/ProjectSurvival/`:

| Папка | Назначение |
|-------|------------|
| `Core/` | GameMode, GameInstance, общие BP, DataTables, интерфейсы |
| `Characters/` | Игрок, AI, анимации |
| `Gameplay/` | Механики: здоровье, голод, компоненты, подсистемы |
| `Items/` | Предметы, экипировка, пикапы |
| `Crafting/` | Рецепты и логика крафта |
| `Environment/` | Мир: материалы, меши, foliage, landscape |
| `UI/` | HUD, меню, виджеты |
| `Audio/` | SFX и музыка |
| `VFX/` | Niagara, партиклы |
| `Maps/` | `Prototype/` — тестовые уровни, `Production/` — финальные |
| `ThirdParty/` | Ассеты из Marketplace |

Личные эксперименты — `Content/Developers/<ваше_имя>/` (не коммитится).

## Документация

| Файл | Описание |
|------|----------|
| [docs/SPRINT_01.md](docs/SPRINT_01.md) | Чеклист первого спринта |
| [docs/COLLABORATION.md](docs/COLLABORATION.md) | Workflow, зоны, конфликты |
| [docs/NAMING.md](docs/NAMING.md) | Префиксы и именование ассетов |

## Ветки

| Ветка | Назначение |
|-------|------------|
| `main` | Стабильная сборка |
| `dev` | Интеграция — **основная рабочая ветка** |
| `feature/*` | Отдельная задача одного разработчика |

## Правила

- Один `.uasset` — один человек за раз (git не мержит бинарники)
- Работать из `dev` или `feature/*`, не пушить напрямую в `main`
- Перед push — сохранить проект в редакторе
- Все на **UE 5.7**
- Имена ассетов — на английском, с префиксами (`BP_`, `WBP_`, `Map_`)

## Git LFS

Проект использует LFS для `.uasset`, `.umap`, текстур, аудио и FBX.

```bash
git lfs install    # один раз на машине
git lfs pull       # после каждого pull
```

Free-план GitHub: ~10 GiB storage + 10 GiB bandwidth/мес. Следите за объёмом в **Settings → Billing** на GitHub.
