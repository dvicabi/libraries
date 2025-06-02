# 📁 `os` – Operating System Interface

```python
import os
````

---

## 🔹 עבודה עם קבצים ותיקיות

### 🧩 os.getcwd()

מחזיר את הנתיב הנוכחי של הסקריפט.

```python
current_dir = os.getcwd()
print(current_dir)
```

---

### 🧩 os.chdir(path)

משנה את תיקיית העבודה הנוכחית.

```python
os.chdir("/home/user/documents")
```

---

### 🧩 os.listdir(path='.')

מחזיר רשימת קבצים/תיקיות בתיקייה.

```python
files = os.listdir(".")
print(files)
```

---

### 🧩 os.mkdir(path)

יוצר תיקייה חדשה.

```python
os.mkdir("my_folder")
```

---

### 🧩 os.makedirs(path, exist\_ok=False)

יוצר תיקיות מקוננות.

```python
os.makedirs("parent/child", exist_ok=True)
```

---

### 🧩 os.rmdir(path)

מוחק תיקייה ריקה.

```python
os.rmdir("my_folder")
```

---

### 🧩 os.removedirs(path)

מוחק תיקיות ריקות כולל הורים.

```python
os.removedirs("parent/child")
```

---

### 🧩 os.rename(src, dst)

שינוי שם קובץ או תיקייה.

```python
os.rename("old_name.txt", "new_name.txt")
```

---

### 🧩 os.replace(src, dst)

כמו rename אך מוחק את היעד אם קיים.

```python
os.replace("temp.txt", "data/final.txt")
```

---

### 🧩 os.remove(path)

מוחק קובץ.

```python
os.remove("unwanted.txt")
```

---

### 🧩 os.unlink(path)

כמו remove.

```python
os.unlink("temp.txt")
```

---

### 🧩 os.path.exists(path)

בודק אם נתיב קיים.

```python
if os.path.exists("data.json"):
    print("Found!")
```

---

### 🧩 os.path.isfile(path)

בודק אם הנתיב הוא קובץ.

```python
if os.path.isfile("example.txt"):
    print("It's a file!")
```

---

### 🧩 os.path.isdir(path)

בודק אם הנתיב הוא תיקייה.

```python
if os.path.isdir("my_folder"):
    print("It's a folder!")
```

---

### 🧩 os.path.getsize(path)

גודל קובץ בבתים.

```python
size = os.path.getsize("video.mp4")
print(size)
```

---

### 🧩 os.path.abspath(path)

המרת נתיב לנתיב מלא.

```python
abs_path = os.path.abspath("file.txt")
print(abs_path)
```

---

### 🧩 os.path.basename(path)

מחזיר רק את שם הקובץ מתוך נתיב.

```python
name = os.path.basename("/path/to/file.txt")
print(name)  # file.txt
```

---

### 🧩 os.path.dirname(path)

מחזיר רק את שם התיקייה.

```python
folder = os.path.dirname("/path/to/file.txt")
print(folder)  # /path/to
```

---

### 🧩 os.path.join(\*paths)

מאחד חלקי נתיב.

```python
full_path = os.path.join("folder", "file.txt")
print(full_path)
```

---

### 🧩 os.path.split(path)

מפצל נתיב לשם תיקייה וקובץ.

```python
dir_name, file_name = os.path.split("/folder/file.txt")
```

---

### 🧩 os.path.splitext(path)

מפצל לקובץ ולסיומת.

```python
name, ext = os.path.splitext("video.mp4")
print(name, ext)  # video .mp4
```

---

## 🔹 מידע על מערכת

### 🧩 os.name

שם מערכת ההפעלה.

```python
print(os.name)  # posix / nt
```

---

### 🧩 os.environ

גישה למשתני סביבה.

```python
print(os.environ["PATH"])
```

---

### 🧩 os.getenv(key, default=None)

קבלת ערך משתנה סביבה.

```python
home = os.getenv("HOME", "/home/default")
```

---

### 🧩 os.putenv(key, value)

הגדרת משתנה סביבה.

```python
os.putenv("MODE", "DEV")
```

---

### 🧩 os.cpu\_count()

מספר ליבות המעבד.

```python
print(os.cpu_count())
```

---

### 🧩 os.getlogin()

משתמש מחובר.

```python
print(os.getlogin())
```

---

### 🧩 os.getpid()

מזהה תהליך נוכחי.

```python
print(os.getpid())
```

---

### 🧩 os.getppid()

מזהה תהליך אב.

```python
print(os.getppid())
```

---

## 🔹 הרצת פקודות מערכת

### 🧩 os.system(command)

הרצת פקודת מערכת.

```python
os.system("echo Hello from shell")
```

---

### 🧩 os.startfile(path)

פתח קובץ עם תוכנה ברירת מחדל (Windows בלבד).

```python
os.startfile("example.pdf")
```

---

### 🧩 os.execv(path, args)

הפעלת תוכנית חדשה.

```python
os.execv("/bin/ls", ["ls", "-l"])
```

---

## 🔹 מתקדמים

### 🧩 os.scandir(path='.')

מחזיר generator של תוכן התיקייה.

```python
for entry in os.scandir("."):
    print(entry.name)
```

---

### 🧩 os.walk(top, topdown=True)

מעבר רקורסיבי בתיקיות.

```python
for root, dirs, files in os.walk("."):
    print(f"{root=}, {files=}")
```

