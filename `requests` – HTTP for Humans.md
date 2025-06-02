# 🌐 `requests` – HTTP for Humans

```python
import requests
````

---

## 🔹 שליחת בקשות HTTP

### 🧩 requests.get(url, params=None, ...)

שליחת בקשת GET (קריאת מידע).

```python
response = requests.get("https://api.github.com/users/octocat")
print(response.status_code)
print(response.json())
```

---

### 🧩 requests.post(url, data=None, json=None, ...)

שליחת בקשת POST (יצירת מידע).

```python
payload = {"username": "dvir", "password": "1234"}
response = requests.post("https://example.com/api", json=payload)
print(response.status_code)
```

---

### 🧩 requests.put(url, data=...)

עדכון משאב קיים.

```python
response = requests.put("https://example.com/api/item/1", data={"name": "updated"})
```

---

### 🧩 requests.delete(url)

מחיקת משאב מהשרת.

```python
response = requests.delete("https://example.com/api/item/1")
```

---

### 🧩 requests.head(url)

קבלת כותרות בלבד (ללא גוף).

```python
response = requests.head("https://www.google.com")
print(response.headers)
```

---

### 🧩 requests.patch(url, data=...)

עדכון חלקי של משאב.

```python
response = requests.patch("https://example.com/api/item/1", data={"name": "partially updated"})
```

---

## 🔹 תוכן התגובה

### 🧩 response.status\_code

קוד התגובה HTTP.

```python
print(response.status_code)
```

---

### 🧩 response.text

התגובה כטקסט גולמי.

```python
print(response.text)
```

---

### 🧩 response.json()

המרת תגובה בפורמט JSON ל־Python dict.

```python
data = response.json()
print(data["name"])
```

---

### 🧩 response.content

תוכן בינארי (למשל תמונות, קבצים).

```python
with open("logo.png", "wb") as f:
    f.write(response.content)
```

---

### 🧩 response.headers

כותרות התגובה.

```python
print(response.headers["Content-Type"])
```

---

## 🔹 בקשות עם פרמטרים

### 🧩 params – פרמטרים ב־URL

```python
params = {"search": "python"}
response = requests.get("https://example.com/api", params=params)
```

---

### 🧩 data – גוף לבקשות טופס (POST/PUT)

```python
data = {"username": "dvir"}
requests.post("https://example.com", data=data)
```

---

### 🧩 json – שליחת JSON

```python
requests.post("https://api.site.com", json={"a": 1, "b": 2})
```

---

## 🔹 עבודה עם Headers

```python
headers = {"Authorization": "Bearer TOKEN"}
requests.get("https://secure.api", headers=headers)
```

---

## 🔹 ניהול חריגות

```python
try:
    response = requests.get("https://example.com", timeout=5)
    response.raise_for_status()
except requests.exceptions.HTTPError as errh:
    print("HTTP Error:", errh)
except requests.exceptions.ConnectionError as errc:
    print("Connection Error:", errc)
except requests.exceptions.Timeout as errt:
    print("Timeout:", errt)
except requests.exceptions.RequestException as err:
    print("Other Error:", err)
```
# ❓ הבדל בין HTTP ל־HTTPS ב־`requests`

## ✅ תשובה:

בספריית `requests`, אין **שום צורך או שינוי בקוד** כדי לעבוד עם HTTPS במקום HTTP.

📌 פשוט מחליפים את כתובת ה־URL:

```python
# HTTP
requests.get("http://example.com")

# HTTPS (מאובטח)
requests.get("https://example.com")
````

## 🔐 מה קורה מאחורי הקלעים?

* `requests` מבוססת על `urllib3` ו־OpenSSL.
* כאשר אתה משתמש ב־`https://`, הספרייה מטפלת אוטומטית בהצפנה, אימות TLS/SSL, ובדיקת תעודות אבטחה (SSL certificates).
* ניתן להוסיף פרמטר כמו `verify=False` כדי לדלג על אימות תעודה (לבדיקות בלבד!):

```python
requests.get("https://self-signed.badssl.com/", verify=False)
```

> ⚠️ שימוש ב־`verify=False` עלול לחשוף אותך לתקיפות MITM – יש להשתמש רק בסביבת פיתוח או בדיקות.

---

✅ בשורה התחתונה: אין צורך בפקודות אחרות – פשוט כתוב `https://` במקום `http://`.

