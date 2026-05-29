# Sprint 1 — «Играбельный скелет»

**Цель:** после спринта любой участник клонирует репо, открывает проект и может побегать по своей тестовой карте с базовым управлением.

**Длительность:** 1–2 недели  
**Рабочая ветка:** `dev`  
**Definition of Done:** все пункты в разделе «Критерии завершения» отмечены, изменения в `dev`, smoke-test пройден всеми троими.

---

## День 0 — Организация (вся команда, ~1 час)

### GitHub и доступ

- [ ] Владелец репо пригласил участников: **Settings → Collaborators**
- [ ] Все успешно клонировали репо и открыли проект в UE 5.7
- [ ] У всех работает `git lfs pull`
- [ ] Default branch на GitHub — `main`
- [ ] (Рекомендуется) Branch protection на `main`: merge только через PR

### Роли и зоны

Заполните таблицу на созвоне (замените имена):

| Участник | GitHub | Зона | Папки |
|----------|--------|------|-------|
| | @ | Геймплей | `Core/`, `Gameplay/`, `Items/` |
| | @ | Мир и персонаж | `Characters/`, `Environment/`, `Maps/` |
| | @ | UI и polish | `UI/`, `Audio/`, `VFX/` |

- [ ] Зоны назначены, пересечений по одним файлам нет
- [ ] Договорились о канале связи (Discord / Telegram) и созвоне 1 раз в неделю

### Локальная настройка каждого участника

- [ ] UE **5.7** установлен
- [ ] `git lfs install` выполнен
- [ ] Git Source Control включён в редакторе
- [ ] Прочитаны `README.md`, `COLLABORATION.md`, `NAMING.md`

---

## Задачи спринта

### A. Core — игровой фундамент

**Владелец:** участник «Геймплей»  
**Ветка:** `feature/core-gamemode`

- [ ] `Core/Blueprints/BP_GameMode_Survival` — базовый GameMode
- [ ] `Core/Blueprints/BP_GameInstance_Survival` — (опционально) GameInstance для сохранений позже
- [ ] В **Project Settings → Maps & Modes** указать `BP_GameMode_Survival` как Default GameMode
- [ ] Создать `Core/Data/DT_GameSettings` — Data Table-заготовка (можно пустую, 1–2 строки-заглушки)
- [ ] Закоммитить и создать PR в `dev`

**Подсказка:** GameMode пока без сложной логики — только правильные defaults и spawn.

---

### B. Персонаж и управление

**Владелец:** участник «Мир и персонаж»  
**Ветка:** `feature/player-character`

- [ ] `Characters/Player/BP_PlayerCharacter` — Third Person или First Person (решить на созвоне и зафиксировать здесь: _______________ )
- [ ] Enhanced Input: `IA_Move`, `IA_Look`, `IA_Jump` (+ `IMC_Default` mapping context)
- [ ] Персонаж спавнится через GameMode / Default Pawn
- [ ] Базовая камера работает
- [ ] `Maps/Prototype/Map_Prototype_Main` — новый уровень с Player Start, простым полом (BSP или Plane)
- [ ] В `Config/DefaultEngine.ini` → `GameDefaultMap` переключить на `/Game/ProjectSurvival/Maps/Prototype/Map_Prototype_Main`
- [ ] Закоммитить и PR в `dev`

**Подсказка:** используйте Third Person template logic как референс, но создавайте ассеты только в `ProjectSurvival/`.

---

### C. UI — минимальный HUD

**Владелец:** участник «UI»  
**Ветка:** `feature/hud-placeholder`

- [ ] `UI/HUD/WBP_HUD_Main` — виджет-заглушка (имя проекта, HP-bar placeholder)
- [ ] `UI/HUD/BP_HUD` или логика показа HUD в PlayerController / PlayerCharacter
- [ ] HUD отображается при Play In Editor
- [ ] Закоммитить и PR в `dev`

**Подсказка:** HP-bar может быть простым `ProgressBar` на фиксированных 100% — логику здоровья подключите в Sprint 2.

---

### D. Тестовые карты (параллельно)

Каждый создаёт **свою** карту, чтобы не конфликтовать:

| Участник | Карта |
|----------|-------|
| Геймплей | `Maps/Prototype/Map_Test_Gameplay` |
| Мир | `Maps/Prototype/Map_Prototype_Main` (основная) |
| UI | `Maps/Prototype/Map_Test_UI` |

- [ ] Карты созданы и закоммичены
- [ ] Никто не редактирует чужую карту без согласования

---

### E. Environment — заготовка мира

**Владелец:** участник «Мир и персонаж» (после персонажа)

- [ ] `Environment/Materials/M_Ground_Prototype` — простой материал земли
- [ ] На `Map_Prototype_Main` — базовое освещение (Directional Light + Sky Atmosphere)
- [ ] (Опционально) простой ландшафт или большая плоскость для тестов

---

## Порядок интеграции (важно)

Чтобы не было конфликтов, мержить PR в таком порядке:

1. `feature/core-gamemode` → `dev`
2. `feature/player-character` → `dev`
3. `feature/hud-placeholder` → `dev`

После каждого merge остальные делают:

```bash
git checkout dev
git pull
git lfs pull
```

И только потом rebase/merge своей feature-ветки на актуальный `dev`.

---

## Критерии завершения Sprint 1

Вся команда подтверждает:

- [ ] Проект открывается без ошибок у всех троих
- [ ] Play In Editor на `Map_Prototype_Main` — персонаж спавнится, WASD + мышь + прыжок работают
- [ ] HUD виден на экране
- [ ] GameMode = `BP_GameMode_Survival`
- [ ] Все изменения в `dev`, `main` обновлён через PR `dev` → `main`
- [ ] Smoke-test записан (скрин или 30-сек. видео в общий чат)

---

## Smoke-test (прогнать всем)

1. `git clone` в **новую** папку (или `git pull` + `git lfs pull`)
2. Открыть `projectSurvival.uproject`
3. Открыть `Map_Prototype_Main`
4. Play (Alt+P)
5. Проверить: движение, камера, прыжок, HUD

| Участник | Дата | OK / Проблема |
|----------|------|---------------|
| | | |
| | | |
| | | |

---

## Не входит в Sprint 1 (Sprint 2+)

- Инвентарь, крафт, голод/жажда
- AI враги
- Сохранения
- C++ модуль
- Production-карты
- Marketplace-ассеты (если не согласованы)

---

## Полезные команды

```bash
# Начать задачу
git checkout dev && git pull && git lfs pull
git checkout -b feature/имя-задачи

# Перед PR
git checkout dev && git pull
git checkout feature/имя-задачи
git rebase dev
git push -u origin feature/имя-задачи

# После merge PR — удалить локальную ветку
git checkout dev && git pull
git branch -d feature/имя-задачи
```

## Commit messages

Краткий формат:

```
feat: add BP_GameMode_Survival
feat: add player character with enhanced input
feat: add prototype main map and set as default
fix: correct spawn point on prototype map
```
