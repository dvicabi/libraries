```python
# ✅ רשימת כל הפונקציות והמחלקות המרכזיות ב־googleapiclient עם הסברים

from googleapiclient.discovery import build           # יצירת שירות API
from googleapiclient.errors import HttpError          # טיפול בשגיאות מהשרת
from googleapiclient.http import (
    MediaFileUpload,                                  # העלאת קבצים רגילה
    MediaIoBaseDownload                               # הורדת קבצים ל־BytesIO
)
```

---

### 📦 googleapiclient.discovery

```python
build(serviceName, version, credentials=None, ...)  # יוצר חיבור API לשירות כמו YouTube, Drive וכו'
```

---

### 📦 googleapiclient.errors

```python
HttpError                                           # חריגה שמתקבלת מבקשה ל־API שנכשלה (כמו 403, 404)
```

---

### 📦 googleapiclient.http

```python
MediaFileUpload(filename, mimetype=None,            # יוצר אובייקט העלאה לקובץ מתוך דיסק
                chunksize=-1, resumable=False)

MediaIoBaseDownload(fd, request, chunksize=...)     # יוצר מנגנון להורדת קובץ מבוסס בקשות חוזרות (resumable)
```

---

### 📦 מחלקות פנימיות ואובייקטים נוספים

```python
HttpRequest                                         # כל בקשה שאתה יוצר בשירות – לדוגמה youtube.videos().insert(...) מחזירה את זה
HttpRequest.execute()                               # מפעיל את הבקשה בפועל
HttpRequest.next_chunk()                            # בשימוש בהעלאה/הורדה בקיטועים
HttpRequest.uri                                     # מחזיר את כתובת ה־API שנשלחה
HttpRequest.method                                  # מחזיר את סוג הבקשה ('GET', 'POST' וכו')
```

---

### 🧠 מתודולוגיית עבודה בסיסית

```python
# 1. יצירת חיבור
service = build("drive", "v3", credentials=creds)

# 2. יצירת בקשה
request = service.files().list()

# 3. ביצוע הבקשה
response = request.execute()
```

