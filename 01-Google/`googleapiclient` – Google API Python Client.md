# 📡 `googleapiclient` – Google API Python Client

```python
from googleapiclient.discovery import build
from googleapiclient.http import MediaFileUpload, MediaIoBaseDownload
from googleapiclient.errors import HttpError
````

---

## 📌 מטרת הספרייה

ספריית `googleapiclient` מאפשרת ליצור ולבצע בקשות ל־Google APIs (כמו YouTube API, Drive API, Sheets API וכו') בצורה דינמית, מבוססת REST, ללא קוד מותאם מראש לכל שירות.

---

## 🧩 1. מודול discovery – יצירת שירות API

```python
from googleapiclient.discovery import build
```

### 🔹 build(serviceName, version, credentials, ...)

יוצר אובייקט שירות (Service Resource) שמייצג את ה־API הספציפי.

```python
youtube = build("youtube", "v3", credentials=creds)
drive = build("drive", "v3", credentials=creds)
```

| פרמטר             | הסבר                                        |
| ----------------- | ------------------------------------------- |
| `serviceName`     | שם ה־API – לדוגמה: `"youtube"`              |
| `version`         | גרסת API – לדוגמה: `"v3"`                   |
| `credentials`     | טוקן OAuth2 מאומת                           |
| `cache_discovery` | ברירת מחדל `True`. ניתן לבטל ב־Google Colab |

---

## 🧩 2. שיטות לפי שירות (Service Methods)

כל שירות מציע **אובייקטים פנימיים** – לדוגמה:

### ▶️ דוגמה: `youtube` API

```python
youtube.videos().insert()
youtube.playlists().insert()
youtube.thumbnails().set()
youtube.commentThreads().list()
```

### 📁 דוגמה: `drive` API

```python
drive.files().list()
drive.files().create()
drive.files().get_media()
```

כל שיטה כזו מחזירה אובייקט מסוג `HttpRequest`, וצריך לבצע:

```python
response = request.execute()
```

---

## 🧩 3. מודול http – ניהול העלאות והורדות קבצים

```python
from googleapiclient.http import MediaFileUpload, MediaIoBaseDownload
```

### 🔹 MediaFileUpload

משמש להעלאת קובץ מקומי.

```python
media = MediaFileUpload("file.txt", mimetype="text/plain", resumable=True)
```

| פרמטר       | הסבר               |
| ----------- | ------------------ |
| `filename`  | נתיב לקובץ         |
| `mimetype`  | סוג MIME           |
| `resumable` | תומך בהעלאה בקטעים |

---

### 🔹 MediaIoBaseDownload

משמש להורדת קבצים מ־Drive:

```python
from io import BytesIO

request = drive.files().get_media(fileId=FILE_ID)
fh = BytesIO()
downloader = MediaIoBaseDownload(fh, request)

done = False
while not done:
    status, done = downloader.next_chunk()
```

---

## 🧩 4. מודול errors – טיפול בשגיאות

```python
from googleapiclient.errors import HttpError
```

### 🔹 HttpError – תופס חריגות HTTP

```python
try:
    response = request.execute()
except HttpError as e:
    print(e.status_code)
    print(e.reason)
```

---

## 🧩 5. מאפיינים של אובייקט בקשה (HttpRequest)

| מתודה           | תיאור                          |
| --------------- | ------------------------------ |
| `.execute()`    | מבצע את הבקשה                  |
| `.next_chunk()` | בשימוש עם העלאות/הורדות רזומות |
| `.uri`          | URL הבקשה                      |
| `.method`       | סוג הבקשה: GET, POST וכו'      |

---

## ⚙️ יכולות מיוחדות מתקדמות

* תמיכה ב־batch requests
* החלפת transport למימוש מותאם אישית (למשל `google.auth.transport`)
* תיעוד אוטומטי לשירות (מבוסס discovery)

---

## 📌 שירותים נפוצים שתומכים בספרייה זו:

| שירות      | גרסה | שימוש                         |
| ---------- | ---- | ----------------------------- |
| `youtube`  | v3   | ניהול ערוצים, סרטונים, תגובות |
| `drive`    | v3   | קבצים, שיתוף, תיקיות          |
| `sheets`   | v4   | ניהול טבלאות Google           |
| `calendar` | v3   | פגישות ויומנים                |
| `gmail`    | v1   | שליחה/קריאה של מיילים         |
| `docs`     | v1   | מסמכי Google Docs             |

---

📘 למידע נוסף:

* [📚 תיעוד רשמי של google-api-python-client](https://github.com/googleapis/google-api-python-client)
* [🧠 רשימת APIs זמינים](https://developers.google.com/api-client-library/python/apis/)



