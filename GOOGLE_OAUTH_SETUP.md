# 🔐 Настройка Google OAuth для TripGenie

## Что изменилось:

✅ **Новая структура сайта:**
- `/` — Страница авторизации (index.html) с Google Sign-In
- `/landing` — Продающая страница (landing.html)
- `/app` — MVP приложение с AI чатом (app.html)
- `/email` — Email capture страница (tslp.html)

После авторизации пользователь перенаправляется на `/landing.html`

---

## 🚀 Как настроить Google OAuth

### Шаг 1: Создайте проект в Google Cloud Console

1. Откройте https://console.cloud.google.com/
2. Создайте новый проект или выберите существующий
3. Название проекта: **TripGenie**

### Шаг 2: Включите Google Sign-In API

1. Перейдите в **APIs & Services → Library**
2. Найдите **Google+ API** или **Google Sign-In API**
3. Нажмите **Enable**

### Шаг 3: Создайте OAuth 2.0 Client ID

1. Перейдите в **APIs & Services → Credentials**
2. Нажмите **Create Credentials → OAuth client ID**
3. Выберите **Application type:** `Web application`
4. **Name:** `TripGenie Web Client`
5. **Authorized JavaScript origins:**
   ```
   https://tripgen-kmyk.vercel.app
   http://localhost:5000
   ```
6. **Authorized redirect URIs:**
   ```
   https://tripgen-kmyk.vercel.app
   https://tripgen-kmyk.vercel.app/landing.html
   ```
7. Нажмите **Create**
8. **Скопируйте Client ID** (выглядит как `123456789-abc.apps.googleusercontent.com`)

### Шаг 4: Добавьте Client ID в код

Откройте файл `index.html` и замените строку:

```javascript
const GOOGLE_CLIENT_ID = 'YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com';
```

На ваш реальный Client ID:

```javascript
const GOOGLE_CLIENT_ID = '123456789-abc.apps.googleusercontent.com';
```

### Шаг 5: Загрузите изменения на GitHub

```bash
cd /home/user/TRIPGEN
git add index.html
git commit -m "Add Google Client ID"
git push origin main
```

Vercel автоматически задеплоит изменения!

---

## ✅ Проверка работы

1. Откройте https://tripgen-kmyk.vercel.app/
2. Должна появиться страница с кнопкой **"Continue with Google"**
3. Нажмите кнопку — появится попап Google Sign-In
4. После авторизации вы попадёте на `/landing.html` (продающую страницу)

---

## 🎯 Альтернатива: Кнопка "Continue to TripGenie"

Если вы не хотите настраивать Google OAuth прямо сейчас:
- Пользователи могут нажать **"Continue to TripGenie →"**
- Это сразу перекинет их на `/landing.html` без авторизации

---

## 📝 Что хранится в localStorage

После успешной авторизации:
- `tripgenie_logged_in` — статус логина (`true` или `guest`)
- `tripgenie_token` — JWT токен от Google (если авторизовались)
- `tripgenie_user_email` — email пользователя
- `tripgenie_user_name` — имя пользователя

Это можно использовать для персонализации на других страницах!

---

## 🔧 Troubleshooting

**Ошибка: "Google Sign-In SDK не загрузился"**
- Проверьте что добавлен `<script src="https://accounts.google.com/gsi/client">`
- Проверьте интернет-соединение

**Ошибка: "Unauthorized"**
- Проверьте что домен добавлен в **Authorized JavaScript origins**
- Проверьте что Client ID правильный

**Попап не появляется**
- Разрешите попапы в браузере
- Проверьте что домен https:// (не http://)

---

Готово! 🎉
