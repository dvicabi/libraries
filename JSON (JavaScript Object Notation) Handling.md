# 📁 `json` – JSON (JavaScript Object Notation) Handling

```python
import json
````

---

## 🔹 המרת Python ↔ JSON

### 🧩 json.dump(obj, file, ...)

שומר אובייקט JSON לקובץ.

```python
data = {"name": "Dvir", "score": 100}
with open("data.json", "w", encoding="utf-8") as f:
    json.dump(data, f, indent=2, ensure_ascii=False)
```

---

### 🧩 json.dumps(obj, ...)

המרת אובייקט JSON למחרוזת.

```python
text = json.dumps(data, indent=4, ensure_ascii=False)
print(text)
```

---

### 🧩 json.load(file)

טוען JSON מקובץ → לאובייקט Python.

```python
with open("data.json", "r", encoding="utf-8") as f:
    loaded = json.load(f)
print(loaded["name"])
```

---

### 🧩 json.loads(string)

טוען JSON ממחרוזת → לאובייקט Python.

```python
json_str = '{"level": 5, "passed": true}'
parsed = json.loads(json_str)
print(parsed["level"])
```

---

## 🔹 פרמטרים נפוצים

* `indent=4` – עיצוב JSON בקובץ/מחרוזת.
* `sort_keys=True` – ממיין את המפתחות באובייקט JSON.
* `ensure_ascii=False` – שמירת תווים בעברית/Unicode כרגיל (ללא קידוד).
* `default=str` – טיפוס ברירת מחדל להמרה עבור טיפוסים לא נתמכים.

---

### 🧩 שימוש בפרמטרים:

```python
json.dumps(data, indent=2, sort_keys=True, ensure_ascii=False)
```

