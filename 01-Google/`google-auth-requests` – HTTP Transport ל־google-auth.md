# 🌐 `google-auth-requests` – HTTP Transport ל־google-auth

```python
from google.auth.transport.requests import Request
````

---

## 🧠 מטרת הספרייה

📡 `google-auth-requests` מספקת שכבת **תקשורת מאובטחת** בין `google-auth` ל־Google APIs,
ומשתמשת בספריית `requests` לצורך ביצוע פעולות כמו:

* רענון טוקנים (`refresh`)
* אימות טוקן (`verify_id_token`)
* תקשורת בין קריאה ל־OAuth2 לבין גוגל בפועל

---

## 🧩 מחלקות עיקריות

### 🔹 Request (transport.requests.Request)

אובייקט שמאפשר ל־google-auth לבצע בקשות HTTP באמצעות `requests.Session`.

```python
from google.auth.transport.requests import Request

request = Request()
creds.refresh(request)
```

---

## 📌 מתי משתמשים ב־Request?

| שימוש                    | דוגמה                                                         |
| ------------------------ | ------------------------------------------------------------- |
| רענון טוקן               | `creds.refresh(Request())`                                    |
| טעינת credentials מ־user | `flow.run_local_server()` ואז `build(..., credentials=creds)` |
| אימות טוקנים             | `id_token.verify_oauth2_token(..., Request())`                |

---

## 🧩 שילוב עם ספריות אחרות

```python
from google.auth.transport.requests import Request
from google.oauth2.credentials import Credentials

creds = Credentials.from_authorized_user_file("token.json")
if creds and creds.expired and creds.refresh_token:
    creds.refresh(Request())
```

---

## 🧩 אפשרות מתקדמת: שימוש ב־Session משלך

```python
import requests
from google.auth.transport.requests import Request

session = requests.Session()
req = Request(session=session)
```

---

📘 תיעוד רשמי:
[https://google-auth.readthedocs.io/en/latest/reference/google.auth.transport.requests.html](https://google-auth.readthedocs.io/en/latest/reference/google.auth.transport.requests.html)

