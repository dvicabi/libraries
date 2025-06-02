# 📂 `glob` – File Pattern Matching

```python
from glob import glob
````

---

## 🔹 מטרת הספרייה

`glob` מאפשרת למצוא קבצים ותיקיות לפי תבנית (wildcards), כמו `*.txt`, `data/*.csv`, וכדומה.

---

## 🧩 glob(pattern)

מחזירה רשימת קבצים/תיקיות שמתאימים לתבנית המבוקשת.

```python
files = glob("*.txt")
print(files)
# ['file1.txt', 'notes.txt']
```

---

### 🧩 חיפוש בתוך תיקיות

```python
csvs = glob("data/*.csv")
```

---

### 🧩 חיפוש רקורסיבי (Python 3.5+)

```python
files = glob("**/*.py", recursive=True)
```

---

### 🧩 תבניות שימושיות

| תבנית        | משמעות                                 |
| ------------ | -------------------------------------- |
| `*.txt`      | כל קובץ עם סיומת .txt                  |
| `data/*.csv` | כל קובץ csv בתיקייה `data`             |
| `*/`         | כל תיקייה נוכחית                       |
| `**/*.py`    | כל קובץ .py בכל תיקיית משנה (רקורסיבי) |

---

### 🧩 דוגמה לשימוש בפילטר שמות

```python
for path in glob("images/*.png"):
    if "logo" in path:
        print("נמצא לוגו:", path)
```

---

## 📌 הערות:

* `glob` לא מחזירה תיקיות מוסתרות (שמתחילות ב־`.`) כברירת מחדל.
* כל הנתיבים הם מחרוזות (`str`) – ניתן להשתמש עם `os.path` או `Path` להמשך עיבוד.


