# 🎯 Швидкий старт для Vercel Deployment

## ✅ Система повністю готова до deployment!

Всі налаштування бази даних, API endpoints та авторизації вже виконані.

---

## 📦 Крок 1: Завантажте код на GitHub

```bash
# Ініціалізуйте git репозиторій (якщо ще не зроблено)
git init
git add .
git commit -m "Initial commit: AnyWay to English LMS"

# Створіть репозиторій на GitHub і завантажте код
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git branch -M main
git push -u origin main
```

---

## 🚀 Крок 2: Deploy на Vercel

### Варіант A: Через Vercel Dashboard (Рекомендується)

1. **Перейдіть на** https://vercel.com/new
2. **Import Git Repository** - виберіть ваш GitHub репозиторій
3. **Configure Project:**
   - Framework Preset: **Vite**
   - Root Directory: **.**
   - Build Command: `npm run build`
   - Output Directory: `dist`

4. **Add Environment Variables:**
   Натисніть "Add Environment Variable" і додайте:

   ```
   SUPABASE_URL
   https://xukykdgkzerkeygxbmhm.supabase.co

   SUPABASE_ANON_KEY
   eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzMwNTU2NDAsImV4cCI6MjA4ODYzMTY0MH0.2G9OUYEM3gxhrIM1SzQVQvqoB-gBqOv8OkP5K3sZWlI

   SUPABASE_SERVICE_ROLE_KEY
   eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTc3MzA1NTY0MCwiZXhwIjoyMDg4NjMxNjQwfQ.9upYM5aM1TN-MkJH0XHGYtsRvgkWX6LuEeoZgxstomE

   SUPABASE_DB_URL
   postgresql://postgres.xukykdgkzerkeygxbmhm:YOUR_PASSWORD@aws-0-eu-central-1.pooler.supabase.com:6543/postgres
   ```

5. **Натисніть Deploy** 🚀

### Варіант B: Через Vercel CLI

```bash
# Встановіть Vercel CLI
npm i -g vercel

# Увійдіть в акаунт
vercel login

# Deploy у production
vercel --prod

# Під час деплою додайте environment variables коли система запитає
```

---

## 🎉 Крок 3: Перевірте deployment

1. **Frontend:** Відкрийте ваш Vercel URL (наприклад, `https://your-app.vercel.app`)

2. **Backend API Health Check:**
   ```bash
   curl https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b/health
   ```
   Повинно повернути: `{"status":"ok"}`

3. **Storage Bucket:** 
   - Перейдіть на https://supabase.com/dashboard/project/xukykdgkzerkeygxbmhm/storage/buckets
   - Переконайтеся що bucket `make-e9e9da7b-resources` створено автоматично

4. **Початкові дані:**
   - Відкрийте браузерну консоль (F12)
   - Перевірте чи є повідомлення: "Data initialization: Sample data initialized successfully"

---

## 👥 Крок 4: Створіть Teacher акаунт

1. Відкрийте ваш сайт
2. Перейдіть на `/login`
3. Зареєструйте викладача через форму Sign Up (якщо є UI)

**АБО використайте API напряму:**

```bash
curl -X POST https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b/auth/signup \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzMwNTU2NDAsImV4cCI6MjA4ODYzMTY0MH0.2G9OUYEM3gxhrIM1SzQVQvqoB-gBqOv8OkP5K3sZWlI" \
  -d '{
    "email": "teacher@example.com",
    "password": "secure-password-123",
    "metadata": {
      "name": "Ваше Ім'\''я",
      "role": "teacher"
    }
  }'
```

---

## 📚 Крок 5: Додайте контент

### Додати студентів:
1. Увійдіть як Teacher
2. Перейдіть в Teacher Dashboard
3. Натисніть "Додати студента"
4. Заповніть форму (ім'я, email, рівень, цілі)

### Завантажити матеріали:
1. Перейдіть в "Бібліотека матеріалів"
2. Натисніть "Додати матеріал"
3. **Варіанти:**
   - Вставте Google Drive link (автоконвертація)
   - Завантажте PDF/Audio/Video файл
   - Додайте YouTube відео
4. Призначте студентам або "Усім студентам"

### Налаштувати Pricing & Policy:
1. Перейдіть в Teacher Dashboard > Settings
2. Оновіть ціни та умови за потреби
3. За замовчуванням вже встановлено розумні значення

---

## 🔒 Важливі нотатки безпеки

⚠️ **НІКОЛИ не комітьте `.env` або `.env.local` файли в Git!**

Переконайтеся що у вас є `.gitignore`:
```
.env
.env.local
.env*.local
node_modules/
dist/
```

---

## 🐛 Troubleshooting

### "Unauthorized" помилки
- Перевірте чи ви увійшли в систему
- Очистіть localStorage: `localStorage.clear()`
- Перезавантажте сторінку і увійдіть знову

### Файли не завантажуються
- Перевірте що Storage bucket створено в Supabase Dashboard
- Перевірте розмір файлу (максимум 50MB)
- Подивіться консоль браузера на помилки

### Backend не відповідає
- Перевірте що Edge Function задеплоєно в Supabase
- Перевірте чи є `SUPABASE_SERVICE_ROLE_KEY` в environment variables
- Перевірте логи в Supabase Dashboard > Edge Functions

---

## 📊 Моніторинг після deployment

### Frontend (Vercel):
- Dashboard: https://vercel.com/dashboard
- Logs: Project > Logs tab
- Analytics: Project > Analytics

### Backend (Supabase):
- Dashboard: https://supabase.com/dashboard/project/xukykdgkzerkeygxbmhm
- Edge Functions Logs: Functions > make-server-e9e9da7b > Logs
- Storage Usage: Storage > Buckets

---

## ✅ Success Checklist

Після deployment перевірте:

- [ ] ✅ Frontend доступний на Vercel URL
- [ ] ✅ Health endpoint повертає `{"status":"ok"}`
- [ ] ✅ Storage bucket `make-e9e9da7b-resources` створено
- [ ] ✅ Початкові дані завантажено (pricing, policy, testimonials)
- [ ] ✅ Teacher акаунт створено
- [ ] ✅ Можна додавати студентів
- [ ] ✅ Можна завантажувати матеріали
- [ ] ✅ Студенти можуть увійти і бачити матеріали
- [ ] ✅ Progress tracking працює (checkboxes)
- [ ] ✅ Google Drive links конвертуються правильно

---

## 🎓 Додаткові ресурси

- **Повна документація:** [README.md](README.md)
- **API Reference:** [API_REFERENCE.md](API_REFERENCE.md)
- **User Guide:** [USER_GUIDE.md](USER_GUIDE.md)
- **Changelog:** [CHANGELOG.md](CHANGELOG.md)
- **Detailed Deployment:** [DEPLOYMENT.md](DEPLOYMENT.md)

---

## 🚀 Готово!

Ваша LMS платформа "AnyWay to English" повністю налаштована та готова до використання!

**Production URL:** Ваш Vercel URL  
**Supabase Dashboard:** https://supabase.com/dashboard/project/xukykdgkzerkeygxbmhm  
**API Base:** https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b

---

**Успішного викладання! 🎉📚✨**
