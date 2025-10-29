# Action Command Language (ACL)

**Action Command Language** - расширенный язык команд для динамической подстановки данных с поддержкой параметризованных фильтров.

---

## 📌 Синтаксис

Каждая команда - это обычная серверная команда с плейсхолдерами в фигурных скобках:
```
give {PlayerId} item_id
pbc {PlayerId}. 5 Welcome, {PlayerName}!
```

Перед выполнением, плагин заменит плейсхолдеры на их реальные значения.

---

<details>
<summary>📋 Доступные плейсхолдеры</summary>

### Player

| Плейсхолдер | Пример | Описание |
|---|---|---|
| `{PlayerId}` | `12` | Внутренний ID игрока в сессии |
| `{PlayerName}` | `Greetings` | Ник игрока (Steam) |
| `{SteamId}` | `76561198000000000` | Steam ID игрока |
| `{DisplayName}` | `Павел Техников` | Отображаемое имя игрока |
| `{CustomInfo}` | `Scientist` | Текущая команда игрока (Team) |
| `{Role}` | `Scientist` | Роль игрока |
| `{Health}` | `85` | Текущее здоровье игрока |
| `{MaxHealth}` | `100` | Максимальное здоровье |
| `{ArtificialHealth}` | `75` | Artificial здоровье (AHP) |
| `{Room}` | `LczStraight` \| `null` | Комната игрока |
| `{Zone}` | `HeavyContainment` \| `null` | Зона игрока |
| `{CurrentItem}` | `Flashlight` \| `null` | Предмет игрока в руках |
| `{GroupColor}` | `#FF0000` | Цвет группы (HEX) |
| `{HumeShield}` | `25` | Щит SCP-127 |
| `{MaxHumeShield}` | `100` | Максимальный щит SCP-127 |
| `{GameObject}` | `-` | GameObject игрока |
| `{GroupName}` | `Владелец проекта` \| `null ` | Название группы |

### Server

| Плейсхолдер | Пример | Описание |
|---|---|
| `{PlayerCount}` | `25` | Кол-во людей на сервере |
| `{MaxPlayerCount}` | `35` | Макс кол-во людей на сервере |
| `{Tps}` | `12` | Текущий TPS |
| `{MaxTps}` | `60` | Макс TPS |
| `{Port}` | `7778` | Текущий порт |
| `{ServerTime}` | `14:55:21` | Время сервера |

</details>

<details>
<summary>🔀 Булевые плейсхолдеры</summary>

| Плейсхолдер | Пример | Описание |
|---|---|---|
| `{IsFriendlyFireEnabled}` | `true` | Включен ли ФФ (Урон по своим) |
| `{IsLobbyLocked}` | `false` | Включен ли LobbyLock |
| `{IsRoundLocked}` | `true` | Включен ли RoundLock |
| `{IsRoundStarted}` | `true` | Начат ли раунд |
| `{IsRoundInProgress}` | `false` | Идет ли сейчас раунд |
| `{IsRoundEnded}` | `false` | Закончился ли раунд |
| `{IsAdmin}` | `true` | Есть ли у игрока доступ к админ панели |
| `{IsNoClipEnabled}` | `false` | Включен ли noclip |
| `{IsBypassEnabled}` | `true` | Включен ли bypass |
| `{IsGodModeEnabled}` | `true` | Включен ли godmode |
| `{IsMuted}` | `false` | Заглушен ли игрок |
| `{IsDisarmed}` | `false` | Связан ли игрок |
| `{IsInventoryFull}` | `true` | Полон ли инвентарь |
| `{IsWithoutItems}` | `true` | Пуст ли инвентарь |
| `{IsIntercomMuted}` | `true` | Заглушен ли intercom у игрока |
| `{DoNotTrack}` | `false` | Доступен ли IP игрока |
| `{HasReservedSlot}` | `true` | Имеется ли доп. слот у игрока |
| `{IsOutOfAmmo}` | `true` | Закончились ли патроны у игрока |
| `{IsSpeaking}` | `false` | Говорит ли игрок |
| `{IsUsingRadio}` | `false` | Говорит ли игрок в рацию сейчас |

</details>

<details>
<summary>📦 Переменные</summary>

ACL позволяет создавать и использовать **глобальные переменные** в рамках одной сессии выполнения команд.

**Синтаксис:** `set <имя_переменной> = <значение>`

После объявления, переменная становится доступна как плейсхолдер `{имя_переменной}`.

**Пример:**
```
set ammoCount = 150
ammo {PlayerId} {ammoCount}
```
</details>

<details>
<summary>🎯 Функции</summary>

К плейсхолдерам можно применять **фильтры (функции)** через двоеточие `:`.
Например:
```
pbc {PlayerId}. 5 "{PlayerName:Upper} joined the game!"
```

**Доступные функции (Simple Filters):**
| Функция | Описание |
|---|---|
| `Upper` | Перевод строки в верхний регистр |
| `Lower` | Перевод строки в нижний регистр |
| `Trim` | Удаление пробелов по краям |
| `Reverse` | Разворот строки |
| `Length` | Длина строки в символах |
</details>

<details>
<summary>✨ Параметризованные функции</summary>

Эти функции принимают аргументы в скобках.
Например:
```
pbc {PlayerId}. 5 "PLAYER: {PlayerName:Remove(test)}"
```

| Функция | Синтаксис | Пример | Результат |
|---|---|---|---|
| `Substring` | `{var:Substring(start,length)}` | `{Name:Substring(0,3)}` | `Joh` (из `John`) |
| `Remove` | `{var:Remove(text)}` | `{Text:Remove(bad)}` | Удаляет подстроку |
| `Replace` | `{var:Replace(old,new)}` | `{Role:Replace(Sci,Dr)}` | Заменяет `old` на `new` |
| `Zalgo` | `{var:Zalgo}` | `{Name:Zalgo}` | Искажённый текст |
| `Contains` | `{var:Contains(text)}` | `{Text:Contains(abc)}` | Возвращает `true`/`false` |
</details>

<details>
<summary>📐 Выражения</summary>

В плейсхолдерах поддерживаются **inline математические операции**: `+`, `-`, `*`, `/`. Они вычисляются после замены всех плейсхолдеров.

**Пример математики:**
```
give {PlayerId} item_id {10 + 5}
```

Также поддерживается генерация случайных чисел как выражение:
```
pbc {PlayerId}. 5 "Ваше случайное число: {RandomInt(1,100)}"
```
</details>

<details>
<summary>⚖ Условные выражения</summary>

В ACL поддерживаются условные блоки `if (...) ... elseif (...) ... else ...`.

**Простой пример:**
```
if({IsAdmin}) pbc {PlayerId}. 5 "Welcome, mighty admin {PlayerName}!"
else pbc {PlayerId}. 5 "Welcome, {PlayerName}!"
```

**Сложный пример с `elseif`:**
```
if({Role}==Scientist) give {PlayerId} medkit
elseif({Role}==ClassD) give {PlayerId} flashlight
else pbc {PlayerId}. 5 "Default spawn for {PlayerName}"
```

**Поддерживаемые операции сравнения:**
| Оператор | Описание |
|---|---|
| `==` | Равно |
| `!=` | Не равно |
| `>` | Больше |
| `<` | Меньше |
| `>=` | Больше или равно |
| `<=` | Меньше или равно |
| `in` | Проверка вхождения (Например: `if({Role} in Scientist,ClassD) ...`) |

**Логические операторы (для сложных условий):**
| Оператор | Описание |
|---|---|
| `&&` | Логическое И (AND) |
| `||` | Логическое ИЛИ (OR) |

**Пример сложного условия:**
```
if({Health}>50 && {IsDisarmed}==false) pbc {PlayerId}. 3 "You are safe."
```
</details>

<details>
<summary>🔄 Циклы</summary>

ACL поддерживает циклы `foreach` для выполнения команд несколько раз с изменяемым счетчиком.

**Синтаксис:** `foreach <переменная> in <старт>..<конец> do <команда>`

**Пример:**
(Эта команда отправит игроку 5 сообщений с нумерацией от 1 до 5)
```
foreach i in 1..5 do pbc {PlayerId}. 1 "Сообщение {i}"
```
</details>

<details>
<summary>🧊 Методы GameObject</summary>

ACL может вызывать методы на игровых объектах (например, на объектах карты, созданных MapEditorReborn), у которых есть компонент `ActionsObject`.

**Синтаксис:** `GameObject.<Метод>(<аргументы>)`

**Пример:**
```
GameObject.Destroy(this)
```

**Доступные методы:**
| Метод | Аргументы | Описание |
|---|---|---|
| `Destroy` | `this` \| `parent` | Уничтожает **`this`** (сам объект) или **`parent`** (родительский объект). |
</details>

---

## 🛠 Рекомендации

* Если нужно использовать `{` и `}` как символы, а не для плейсхолдера, экранируйте их обратным слэшем: `\{` и `\}`.
