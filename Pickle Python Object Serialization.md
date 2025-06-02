# 📁 `pickle` – Python Object Serialization

```python
import pickle
````

---

## 🔹 שימושים עיקריים

### 🧩 pickle.dump(obj, file, protocol=...)

שומר אובייקט לפורמט בינארי בקובץ.

```python
data = {"username": "Dvir", "score": 99}
with open("data.pkl", "wb") as f:
    pickle.dump(data, f)
```

---

### 🧩 pickle.load(file)

טוען אובייקט מקובץ `pkl`.

```python
with open("data.pkl", "rb") as f:
    loaded_data = pickle.load(f)
print(loaded_data["score"])
```

---

### 🧩 pickle.dumps(obj)

ממיר אובייקט למחרוזת בינארית בזיכרון.

```python
binary_data = pickle.dumps(data)
```

---

### 🧩 pickle.loads(bytes\_obj)

משחזר אובייקט ממחרוזת בינארית.

```python
original_data = pickle.loads(binary_data)
```

---

## 🔹 קבועים שימושיים

| קבוע                      | שימוש                        |
| ------------------------- | ---------------------------- |
| `pickle.HIGHEST_PROTOCOL` | שימוש בפרוטוקול המתקדם ביותר |
| `pickle.DEFAULT_PROTOCOL` | שימוש בפרוטוקול ברירת המחדל  |

```python
pickle.dump(data, f, protocol=pickle.HIGHEST_PROTOCOL)
```

---

## 🔹 מחלקות מתקדמות (שימוש נדיר)

### 🧩 pickle.Pickler

שומר אובייקט באמצעות אובייקט Pickler.

```python
with open("data.pkl", "wb") as f:
    pickler = pickle.Pickler(f)
    pickler.dump(data)
```

---

### 🧩 pickle.Unpickler

טוען אובייקט באמצעות Unpickler.

```python
with open("data.pkl", "rb") as f:
    unpickler = pickle.Unpickler(f)
    data = unpickler.load()
```

---

## 🧨 אזהרות אבטחה

* ✖️ אל תשתמש בקבצי Pickle ממקורות לא מהימנים.
* ✖️ Pickle עלול להריץ קוד בעת הטעינה – מהווה סיכון אבטחתי.

