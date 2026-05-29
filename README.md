# projectSurvival

Survival-игра на **Unreal Engine 5.7**. Репозиторий настроен для совместной работы команды из 3 человек.

## Быстрый старт

### Требования

- Unreal Engine **5.7** (та же версия у всех участников команды)
- [Git LFS](https://git-lfs.com/) — обязателен для `.uasset` / `.umap`

### Первый клон

```bash
git clone <url-репозитория>
cd projectSurvival
git lfs install
git lfs pull
```

Открыть `projectSurvival.uproject` в Unreal Editor.

### Ежедневный цикл

```bash
git pull                    # перед началом работы
# ... работа в редакторе ...
git status
git add .
git commit -m "описание изменений"
git push
```

## Структура Content

Весь игровой контент лежит в `Content/ProjectSurvival/`:

| Папка | Назначение |
|-------|------------|
| `Core/` | GameMode, GameInstance, общие BP, DataTables, интерфейсы |
| `Characters/` | Игрок, AI, общие анимации/скелеты |
| `Gameplay/` | Механики: здоровье, голод, компоненты, подсистемы |
| `Items/` | Предметы, экипировка, пикапы |
| `Crafting/` | Рецепты и логика крафта |
| `Environment/` | Мир: материалы, меши, foliage, landscape |
| `UI/` | HUD, меню, виджеты |
| `Audio/` | SFX и музыка |
| `VFX/` | Niagara, партиклы |
| `Maps/` | `Prototype/` — черновые уровни, `Production/` — финальные |
| `ThirdParty/` | Ассеты из Marketplace (с лицензией) |

Личные эксперименты — в `Content/Developers/<ваше_имя>/` (не попадает в git).

Подробнее: [docs/COLLABORATION.md](docs/COLLABORATION.md)

## Ветки

| Ветка | Назначение |
|-------|------------|
| `main` | Стабильная сборка, только проверенный контент |
| `dev` | Интеграция фич команды |
| `feature/*` | Отдельная задача одного разработчика |

## Важно

- Не редактировать один и тот же `.uasset` одновременно — git не умеет мержить бинарники
- Перед push: закрыть редактор или хотя бы сохранить и не держать ассет открытым
- Все участники на **одной версии UE 5.7**
