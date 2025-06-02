# 🔐 `google-auth` – רשימת פונקציות ומחלקות מרכזיות עם הסברים

```python
# ================================
# 📌 google.auth – פונקציות עיקריות
# ================================

import google.auth

# 🔹 google.auth.default(scopes=None, request=None)
# - תפקיד: מחזירה את ההרשאות (credentials) וה־project_id המוגדר כברירת מחדל בסביבת הריצה.
# - שימוש:
creds, project = google.auth.default()
# Example:
#   creds, project = google.auth.default(scopes=["https://www.googleapis.com/auth/drive"])

# 🔹 google.auth.load_credentials_from_file(filename, scopes=None, quota_project_id=None)
# - תפקיד: טוענת credentials מקובץ JSON (יכולים להיות חשבונות שירות או גולשים מורשים).
# - שימוש:
creds_from_file, project = google.auth.load_credentials_from_file(
    "path/to/credentials.json",
    scopes=["https://www.googleapis.com/auth/drive"]
)

# 🔹 google.auth.load_credentials_from_info(info, scopes=None, quota_project_id=None)
# - תפקיד: טוענת credentials מתוך מילון (dict) שמכיל מידע על האישורים.
# - שימוש:
info = {
    # דוגמה למידע שמתקבל מקובץ JSON המיובא כמילון
    "client_id": "CLIENT_ID",
    "client_secret": "CLIENT_SECRET",
    "refresh_token": "REFRESH_TOKEN",
    "token": "ACCESS_TOKEN",
    "token_uri": "TOKEN_URI"
}
creds_from_info, project = google.auth.load_credentials_from_info(
    info,
    scopes=["https://www.googleapis.com/auth/spreadsheets"]
)

# ================================
# 📌 google.oauth2.credentials – OAuth 2.0 Credentials למשתמשים
# ================================
from google.oauth2.credentials import Credentials

# 🔹 Credentials(token, refresh_token, client_id, client_secret, token_uri, scopes=None)
# - תפקיד: בונה אובייקט credentials עבור משתמש לפי נתוני OAuth2.
# - שימוש:
creds_user = Credentials(
    token="ACCESS_TOKEN",
    refresh_token="REFRESH_TOKEN",
    client_id="CLIENT_ID",
    client_secret="CLIENT_SECRET",
    token_uri="TOKEN_URI",
    scopes=["https://www.googleapis.com/auth/drive"]
)

# ================================
# 📌 google.oauth2.service_account – חשבונות שירות (Service Accounts)
# ================================
from google.oauth2.service_account import Credentials as SACredentials

# 🔹 SACredentials.from_service_account_file(filename, scopes=None, subject=None, quota_project_id=None)
# - תפקיד: טוען credentials מחשבון שירות מקובץ JSON.
# - שימוש:
sa_creds = SACredentials.from_service_account_file(
    "service_account.json",
    scopes=["https://www.googleapis.com/auth/cloud-platform"]
)

# 🔹 SACredentials.from_service_account_info(info, scopes=None, subject=None, quota_project_id=None)
# - תפקיד: טוען credentials מחשבון שירות מקובץ נתונים בפורמט מילוני.
# - שימוש:
info_service = {
    "type": "service_account",
    "project_id": "PROJECT_ID",
    "private_key_id": "PRIVATE_KEY_ID",
    "private_key": "-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n",
    "client_email": "service-account@example.com",
    "client_id": "CLIENT_ID",
    "auth_uri": "https://accounts.google.com/o/oauth2/auth",
    "token_uri": "https://oauth2.googleapis.com/token",
    "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
    "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/service-account%40example.com"
}
sa_creds_info = SACredentials.from_service_account_info(
    info_service,
    scopes=["https://www.googleapis.com/auth/drive"]
)

# ================================
# 📌 google.auth.transport.requests – ניהול תעבורה ושדרוג טוקנים
# ================================
from google.auth.transport.requests import Request

# 🔹 Request()
# - תפקיד: אובייקט Request המשתמש בבקשות HTTP (מבוסס על requests.Session) לצורך רענון ואימות טוקנים.
# - שימוש:
request_obj = Request()

# דוגמה לשימוש ברענון:
if creds_user and creds_user.expired and creds_user.refresh_token:
    creds_user.refresh(request_obj)

# ================================
# 📌 פונקציות עזר נוספות
# ================================
import google.auth.credentials

# 🔹 google.auth.credentials.with_scopes_if_required(credentials, scopes)
# - תפקיד: בודקת אם credentials כוללים את הטווחים הדרושים, ואם לא, היא מעדכנת אותם.
# - שימוש:
creds_scoped = google.auth.credentials.with_scopes_if_required(
    creds_user, ["https://www.googleapis.com/auth/drive"]
)

# ================================
# 📌 טיפול בשגיאות
# ================================
from google.auth.exceptions import RefreshError

# 🔹 RefreshError
# - תפקיד: חריגה המתעוררת בעת כשל ברענון הטוקן.
# - שימוש:
try:
    creds_user.refresh(request_obj)
except RefreshError as e:
    print("שגיאה ברענון הטוקן:", e)
````

---

📘 **תמצית:**

* **google.auth** מספקת כלים לטעינת הרשאות ממקורות שונים (קבצים, סביבות, מידע מילוני).
* **google.oauth2.credentials** מיועדת להטענת הרשאות משתמש.
* **google.oauth2.service\_account** מטפלת בהרשאות חשבון שירות.
* **google.auth.transport.requests.Request** משמש לאימות, רענון הטוקנים ולעבודה עם HTTP.

💡 זהו סקירה מקיפה של כל הפונקציות והמחלקות המרכזיות ב־`google-auth` עם דוגמאות קוד והסברים.
ניתן להשתמש בדף זה כ-reference לכל פעילות שקשורה לאימות והרשאות בפרויקט שלך.

