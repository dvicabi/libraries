# 🌐 `google-auth-oauthlib` – OAuth 2.0 Authentication Flow

```python
from google_auth_oauthlib.flow import InstalledAppFlow, Flow
````

---

## 🧠 מטרת הספרייה

הספרייה `google-auth-oauthlib` מרחיבה את `google-auth` ומאפשרת:

* יצירה של **OAuth 2.0 Flow אינטראקטיבי** (למשתמשים)
* תמיכה במצב **Desktop**, **Web Server**, **Console**, ו־**localhost**
* קבלת `Credentials` באמצעות התחברות אמיתית עם חשבון Google

---

## 🧩 זרימת עבודה טיפוסית

```python
from google_auth_oauthlib.flow import InstalledAppFlow

flow = InstalledAppFlow.from_client_secrets_file(
    "client_secrets.json",
    scopes=["https://www.googleapis.com/auth/youtube.upload"]
)

creds = flow.run_local_server(port=0)
```

🔁 לאחר התחברות בדפדפן, מתקבל אובייקט `Credentials` תקף.

---

## 🧩 אפשרויות זרימה – זרמי OAuth נתמכים

| זרם             | מחלקה              | שימוש                     |
| --------------- | ------------------ | ------------------------- |
| **Desktop App** | `InstalledAppFlow` | הפעלה מקומית עם localhost |
| **Web App**     | `Flow`             | הפניה ל־Redirect URI      |
| **Console**     | `run_console()`    | ללא דפדפן, במסוף CLI      |

---

## 🧩 שיטות קיימות במחלקות

### 📌 InstalledAppFlow

```python
# from_client_secrets_file()
# - קורא קובץ JSON עם client_id ו־client_secret.
InstalledAppFlow.from_client_secrets_file(filename, scopes, redirect_uri=None)

# from_client_config()
# - מגדיר את המידע כ־dict במקום קובץ.
InstalledAppFlow.from_client_config(config, scopes, redirect_uri=None)

# run_local_server()
# - פותח שרת מקומי בדפדפן ומשלים את ההתחברות.
creds = flow.run_local_server(port=0)

# run_console()
# - למי שמריץ קוד ללא דפדפן (למשל ב־SSH).
creds = flow.run_console()
```

---

### 📌 Flow (לשימוש ב־Web Server)

```python
# Flow.from_client_config() or from_client_secrets_file()
# מתחיל זרימת OAuth בסיסית כמו ב־InstalledAppFlow

flow.authorization_url()
# מחזיר URL שבו המשתמש מתחבר לחשבון Google

flow.fetch_token(code=...)
# מקבל את הטוקן לאחר שהמשתמש התחבר עם הקוד שהתקבל
```

---

## 📄 מבנה client\_secrets.json לדוגמה

```json
{
  "installed": {
    "client_id": "xxxxxxxxxxxx.apps.googleusercontent.com",
    "project_id": "my-project",
    "auth_uri": "https://accounts.google.com/o/oauth2/auth",
    "token_uri": "https://oauth2.googleapis.com/token",
    "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
    "client_secret": "GOCSPX-xxxxxxx",
    "redirect_uris": ["http://localhost"]
  }
}
```

---

## 📌 שילוב עם google-auth

לאחר השלמת ה־Flow, אתה מקבל:

```python
creds = flow.run_local_server()
```

ואז אפשר להשתמש ב־`creds` עם:

```python
from googleapiclient.discovery import build
youtube = build("youtube", "v3", credentials=creds)
```

---

📘 תיעוד רשמי:
[https://google-auth-oauthlib.readthedocs.io/](https://google-auth-oauthlib.readthedocs.io/)

