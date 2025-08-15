# Action Command Language (ACL) v1.1.0

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
| `{Room}` | `LczStraight` | Текущая комната игрока |
| `{Zone}` | `HeavyContainment` | Текущая зона игрока |
| `{CurrentItem}` | `Flashlight` | Текущий предмет игрока |
| `{ServerTime}` | `14:55:21` | Время сервера |
| `{GroupColor}` | `#FF0000` | Цвет группы (HEX) |

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

| Фильтр | Синтаксис | Пример | Результат |
|--------|-----------|--------|-----------|
| `Substring` | `{var:Substring(start,length)}` | `{Name:Substring(0,3)}` | `Joh` (из `John`) |
| `Remove` | `{var:Remove(text)}` | `{Text:Remove(bad)}` | Удаляет подстроку |
| `Replace` | `{var:Replace(old,new)}` | `{Role:Replace(Sci,Dr)}` | `Dr` вместо `Sci` |

</details>

---

## ⚡ Примеры

**1. Выдача случайного предмета:**
```
give {PlayerId} item_{RandomInt}
```

**2. Объявление для всех:**
```
broadcast 5 "{PlayerName} has joined the game!"
```

**3. Использование функции:**
```
broadcast 5 "PLAYER: {PlayerName:Upper}"
```

---

## 🛠 Рекомендации
- Лишние пробелы в начале и конце будут автоматически удалены.
- Пустые команды игнорируются.
- Плейсхолдеры можно комбинировать в одной команде.
- Если нужно использовать `{` и `}` как символы, экранируйте их: `\{` и `\}`.

---

## 📅 История изменений

| Версия | Изменения |
|--------|-----------|
| 1.0.0 | Базовые плейсхолдеры: PlayerId, PlayerName, SteamId, DisplayName, CustomInfo, Role, Health, MaxHealth, ArtificialHealth, Room, Zone, CurrentItem, ServerTime |
