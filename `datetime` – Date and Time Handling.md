# 📅 `datetime` – Date and Time Handling

```python
from datetime import datetime, timedelta, date, time
````

---

## 🔹 יצירת תאריכים ושעות

### 🧩 datetime.now(tz=None)

זמן נוכחי (עם אפשרות לאזור זמן).

```python
now = datetime.now()
print(now)
```

---

### 🧩 datetime.utcnow()

זמן נוכחי ב־UTC.

```python
utc_now = datetime.utcnow()
```

---

### 🧩 datetime(year, month, day, hour=0, minute=0, ...)

יצירת אובייקט `datetime` מותאם אישית.

```python
dt = datetime(2025, 6, 1, 14, 30)
```

---

### 🧩 date.today()

תאריך נוכחי בלבד (ללא שעה).

```python
today = date.today()
```

---

### 🧩 time(hour, minute, second)

יצירת שעה בלבד.

```python
t = time(14, 0)
```

---

## 🔹 חישובים עם זמנים

### 🧩 timedelta(days=0, hours=0, minutes=0, ...)

הפרש זמן.

```python
delta = timedelta(days=2, hours=3)
future = datetime.now() + delta
```

---

### 🧩 datetime + timedelta

חיבור זמן + הפרש.

```python
tomorrow = datetime.now() + timedelta(days=1)
```

---

### 🧩 datetime - datetime

הפרש בין תאריכים.

```python
diff = datetime(2025, 6, 1) - datetime(2025, 5, 30)
print(diff.days)  # 2
```

---

## 🔹 המרה בין מחרוזת ל־datetime

### 🧩 datetime.strptime(str, format)

המרת מחרוזת ל־datetime לפי תבנית.

```python
dt = datetime.strptime("2025-06-01", "%Y-%m-%d")
```

---

### 🧩 datetime.strftime(format)

המרת datetime למחרוזת פורמט.

```python
formatted = datetime.now().strftime("%d/%m/%Y %H:%M")
print(formatted)
```

---

## 🔹 תכונות של datetime

| תכונה          | דוגמה             |
| -------------- | ----------------- |
| `dt.year`      | `2025`            |
| `dt.month`     | `6`               |
| `dt.day`       | `1`               |
| `dt.hour`      | `14`              |
| `dt.minute`    | `0`               |
| `dt.second`    | `0`               |
| `dt.weekday()` | יום בשבוע (0=שני) |
| `dt.date()`    | מחזיר `date`      |
| `dt.time()`    | מחזיר `time`      |

---

## 🔹 אזורי זמן (Python 3.9+)

```python
from zoneinfo import ZoneInfo

dt = datetime.now(ZoneInfo("Asia/Jerusalem"))
```

