# 🔐 `google-auth` – Google Authentication Core

```python
import google.auth
from google.auth.transport.requests import Request
from google.oauth2.credentials import Credentials
from google.oauth2.service_account import Credentials as ServiceAccountCredentials
from google.auth.exceptions import RefreshError
````

---

## 🧠 מטרת הספרייה

`google-auth` היא ספריית **הליבה של האימות בגוגל**.
היא אחראית על:

* 🔐 ניהול טוקנים (`access_token`, `refresh_token`)
* 📜 יצירת אובייקטי הרשאה (`Credentials`)
* 🔁 רענון טוקן אוטומטי
* 🛠️ התממשקות עם שירותים (YouTube, Drive וכו')

---

## 🧩 סוגי Credentials (הרשאות)

### ✅ OAuth 2.0 למשתמשים

```python
from google.oauth2.credentials import Credentials
creds = Credentials(token, refresh_token, client_id, client_secret, token_uri)
```

---

### ✅ Service Accounts (שרתים/בקראונד)

```python
from google.oauth2.service_account import Credentials
creds = Credentials.from_service_account_file("service_account.json")
```

---

### ✅ ברירת מחדל (מתוך הסביבה או GCP)

```python
import google.auth
creds, project = google.auth.default()
```

---

## 🧩 התחברות עם רענון טוקן

```python
from google.auth.transport.requests import Request

if creds and creds.expired and creds.refresh_token:
    creds.refresh(Request())
```

---

## 🧩 שמירת הטוקן בצורה מאובטחת

```python
import pickle

with open("token.pickle", "wb") as f:
    pickle.dump(creds, f)
```

---

## 📌 מבני המידע המרכזיים

| מחלקה                       | תיאור                         |
| --------------------------- | ----------------------------- |
| `Credentials`               | ממשק אבסטרקטי לטוקנים של גוגל |
| `UserCredentials`           | OAuth 2.0 רגיל (משתמשים)      |
| `ServiceAccountCredentials` | חשבון שירות                   |
| `IDTokenCredentials`        | למזהה זהות בלבד               |
| `google.auth.default()`     | ניחוש אוטומטי של credentials  |

---

## 📌 זרימת עבודה טיפוסית

```python
from google.oauth2.credentials import Credentials
from google.auth.transport.requests import Request

creds = Credentials.from_authorized_user_file("token.json")

if creds and creds.expired and creds.refresh_token:
    creds.refresh(Request())
```

---

📘 תיעוד רשמי:
[https://google-auth.readthedocs.io/en/latest/](https://google-auth.readthedocs.io/en/latest/)

