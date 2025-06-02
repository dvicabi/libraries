```python
# 📦 google-auth-requests – כל הפונקציות והמתודות של המחלקה Request עם הסבר #

from google.auth.transport.requests import Request

# ================================
# 📌 מחלקה: Request
# ================================
# אובייקט Request פועל כ-wrapper סביב requests.Session, עבור רענון ואימות טוקנים.

req = Request()  # יצירת אובייקט ברירת מחדל (עם requests.Session פנימי)

# ================================
# 📌 מאפיינים (Attributes)
# ================================

# 🔹 req.session
# # אובייקט requests.Session שמשמש לשליחת הבקשות בפועל
session = req.session

# 🔹 req.headers
# # (deprecated) – היה בשימוש פנימי לתמיכה ב־headers

# ================================
# 📌 מתודות (Methods)
# ================================

# 🔹 req.__call__(url, method="GET", body=None, headers=None, timeout=None)
# # קריאה ישירה לאובייקט Request תבצע בקשת HTTP ל־url המבוקש
response = req(
    url="https://oauth2.googleapis.com/token",  # כתובת
    method="POST",                              # שיטת הבקשה
    body=b"data",                               # תוכן (ב־bytes)
    headers={"Content-Type": "application/x-www-form-urlencoded"}  # כותרות
)

# 🔹 req.request(method, url, body=None, headers=None, timeout=None)
# # מתודה זהה ל־__call__, רק בשם אחר – מבצעת את אותה פעולה.
response = req.request("POST", "https://...", body=b"...", headers={...})

# 🔹 req.credentials.refresh(req)
# # לא פונקציה של Request – אבל זוהי הדרך להשתמש באובייקט הזה.
#   היא מעבירה את הבקשה ל־google-auth לצורך רענון הטוקן:
creds.refresh(req)

# ================================
# 📌 שימוש נפוץ מאוד:
# ================================

from google.oauth2.credentials import Credentials
from google.auth.transport.requests import Request

creds = Credentials.from_authorized_user_file("token.json")
if creds and creds.expired and creds.refresh_token:
    creds.refresh(Request())  # ← כאן פועל כל המנגנון בפועל

# ================================
# 📌 דוגמה למקרה מתקדם:
# ================================

import requests
from google.auth.transport.requests import Request

my_session = requests.Session()
req = Request(session=my_session)
creds.refresh(req)
```

