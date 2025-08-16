# Action Command Language (ACL) v1.2.0

**Action Command Language** - расширенный язык команд для динамической подстановки данных с поддержкой параметризованных фильтров.

---

## 📌 Синтаксис
Каждая команда - это обычная серверная команда с плейсхолдерами в фигурных скобках:  
```
give {PlayerId} item_id
broadcast 5 Welcome, {PlayerName}!
```

Перед выполнением, плагин заменит плейсхолдеры на их реальные значения.

---

<details>
<summary>📋 Доступные плейсхолдеры</summary>

| Плейсхолдер | Пример | Описание |
|-------------|--------|----------|
| `{PlayerId}` | `12` | Внутренний ID игрока в сессии |
| `{PlayerName}` | `Greetings` | Ник игрока |
| `{SteamId}` | `76561198000000000` | Steam ID игрока |
| `{DisplayName}` | `Павел Техников` | Отображаемое имя игрока |
| `{CustomInfo}` | `MTF` | Дополнительная информация (например, команда) |
| `{Role}` | `Scientist` | Роль игрока |
| `{Health}` | `85` | Текущее здоровье игрока |
| `{MaxHealth}` | `100` | Максимальное здоровье |
| `{ArtificialHealth}` | `75` | Artificial здоровье |
| `{Room}` | `LczStraight` \| `null` | Текущая комната игрока *(может быть `null`)* |
| `{Zone}` | `HeavyContainment` \| `null` | Текущая зона игрока *(может быть `null`)* |
| `{CurrentItem}` | `Flashlight` | Текущий предмет игрока |
| `{ServerTime}` | `14:55:21` | Время сервера |
| `{GroupColor}` | `#FF0000` | Цвет группы (HEX) |

</details>

<details>
<summary>🔀 Булевые плейсхолдеры</summary>

| Плейсхолдер | Пример | Описание |
|-------------|--------|----------|
| `{IsAdmin}` | `true` | Есть ли у игрока доступ к админ панели |
| `{IsNoClipEnabled}` | `false` | Включен ли noclip |
| `{IsBypassEnabled}` | `true` | Включен ли bypass |
| `{IsMuted}` | `false` | Заглушен ли игрок |
| `{IsDisarmed}` | `false` | Связан ли игрок |
| `{IsInventoryFull}` | `true` | Полон ли инвентарь |

</details>

<details>
<summary>🎯 Функции</summary>
К плейсхолдерам можно применять фильтры через двоеточие `:`.  
Например:
  
```
broadcast 5 "{PlayerName:Upper} joined the game!"
```

**Доступные функции:**
| Фильтр | Описание |
|--------|----------|
| `Upper` | Перевод строки в верхний регистр |
| `Lower` | Перевод строки в нижний регистр |
| `Trim` | Удаление пробелов по краям |
| `Reverse` | Разворот строки |
| `Length` | Длина строки в символах |
</details>

<details>
<summary>✨ Параметризованные функции</summary>
  
```
broadcast 5 "PLAYER: {PlayerName:Upper}"
```

| Фильтр | Синтаксис | Пример | Результат |
|--------|-----------|--------|-----------|
| `Substring` | `{var:Substring(start,length)}` | `{Name:Substring(0,3)}` | `Joh` (из `John`) |
| `Remove` | `{var:Remove(text)}` | `{Text:Remove(bad)}` | Удаляет подстроку |
| `Replace` | `{var:Replace(old,new)}` | `{Role:Replace(Sci,Dr)}` | `Dr` вместо `Sci` |

</details>

---


---

## 🛠 Рекомендации
- Лишние пробелы в начале и конце будут автоматически удалены.
- Пустые команды игнорируются.
- Плейсхолдеры можно комбинировать в одной команде.
- Если нужно использовать `{` и `}` как символы, экранируйте их: `\{` и `\}`.
- `Room` и `Zone` могут быть `null`.

---

## 📅 История изменений

| Версия | Изменения |
|--------|-----------|
| 1.0.0 | Базовые плейсхолдеры: PlayerId, PlayerName, SteamId, DisplayName, CustomInfo, Role, Health, MaxHealth, ArtificialHealth, Room, Zone, CurrentItem, ServerTime |
| 1.1.0 | Добавлены булевые плейсхолдеры (`IsAdmin`, `IsNoClipEnabled`, `IsBypassEnabled`, `IsMuted`, `IsDisarmed`, `IsInventoryFull`) |
| 1.1.1 | Добавлены фильтры (`Trim`, `Reverse`, `Length`) и параметризованные (`Substring`, `Remove`, `Replace`) |
| 1.1.2 | Добавлен синтаксис `if(...) else ...` для условных команд |
