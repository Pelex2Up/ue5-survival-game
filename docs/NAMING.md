# Naming conventions

Единые правила имён для всей команды.

## Префиксы Blueprint / ассетов

| Префикс | Тип |
|---------|-----|
| `BP_` | Blueprint Actor / Component host |
| `WBP_` | Widget Blueprint (UI) |
| `ABP_` | Animation Blueprint |
| `BPI_` | Blueprint Interface |
| `DA_` | Data Asset |
| `DT_` | Data Table |
| `E_` | Enum (Blueprint enum) |
| `ST_` | Structure |
| `M_` | Material |
| `MI_` | Material Instance |
| `T_` | Texture |
| `SM_` | Static Mesh |
| `SK_` | Skeletal Mesh |
| `NS_` | Niagara System |

## Карты

| Префикс | Назначение |
|---------|------------|
| `Map_Prototype_` | Тестовые уровни |
| `Map_` | Production-уровни |

Примеры: `Map_Prototype_Combat`, `Map_MainIsland`

## Папки

- PascalCase для папок с ассетами: `Player`, `Crafting`
- Не создавать папки с именами участников внутри `ProjectSurvival/` — для этого есть `Developers/`

## C++ (когда добавите модуль)

- Классы: `A` Actor, `U` Object, `F` Struct, `I` Interface, `E` Enum
- Файлы совпадают с именем класса: `SurvivalCharacter.h/.cpp`
