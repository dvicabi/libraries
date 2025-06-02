```python
# 🔁 כל הפונקציות והמחלקות המרכזיות של google-auth-oauthlib עם הסברים #

from google_auth_oauthlib.flow import InstalledAppFlow, Flow

# ================================
# 📌 InstalledAppFlow – לשימוש ביישומי דסקטופ/לוקאלי
# ================================

# 🔹 InstalledAppFlow.from_client_secrets_file(filename, scopes, redirect_uri=None)
# # יוצר זרימת OAuth2 מקובץ client_secrets.json
flow = InstalledAppFlow.from_client_secrets_file(
    "client_secrets.json",                    # קובץ שמכיל client_id ו־client_secret
    scopes=["https://www.googleapis.com/auth/youtube.upload"]
)

# 🔹 InstalledAppFlow.from_client_config(config_dict, scopes, redirect_uri=None)
# # כמו הקודם – אך מקונפיג (dict) במקום קובץ
flow = InstalledAppFlow.from_client_config(
    {
        "installed": {
            "client_id": "123.apps.googleusercontent.com",
            "client_secret": "SECRET",
            "auth_uri": "https://accounts.google.com/o/oauth2/auth",
            "token_uri": "https://oauth2.googleapis.com/token",
            "redirect_uris": ["http://localhost"]
        }
    },
    scopes=["https://www.googleapis.com/auth/drive"]
)

# 🔹 flow.run_local_server(port=0, ...)
# # פותח את הדפדפן, מאזין לתשובה ומחזיר את ה־Credentials
creds = flow.run_local_server(port=0)

# 🔹 flow.run_console()
# # מבצע את אותו התהליך – אך דרך קוד במסך (CLI)
creds = flow.run_console()

# ================================
# 📌 Flow – לשימוש באפליקציות Web
# ================================

# 🔹 Flow.from_client_secrets_file(filename, scopes, redirect_uri=None)
# # יוצר זרימה מבוססת Web (כולל redirect_uri)
flow = Flow.from_client_secrets_file("client_secrets.json", scopes=["..."], redirect_uri="https://your.app/callback")

# 🔹 Flow.from_client_config(config_dict, scopes, redirect_uri=None)
# # אותו דבר, רק מקונפיג dict

# 🔹 flow.authorization_url(prompt='consent', access_type='offline')
# # יוצר URL שבו המשתמש צריך לבקר כדי לאשר גישה
auth_url, state = flow.authorization_url()

# 🔹 flow.fetch_token(code=...)
# # לאחר קבלת הקוד מהמשתמש – שולף את הטוקן
flow.fetch_token(code="CODE_FROM_GOOGLE")

# 🔹 flow.credentials
# # מחזיר את ה־Credentials שנוצרו לאחר התחברות
creds = flow.credentials
```

