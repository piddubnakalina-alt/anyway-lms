# AnyWay to English - LMS Platform

Сучасна LMS платформа для приватного викладача англійської мови з повною українською локалізацією.

## 🎉 Status: Ready for Production!

✅ All database integration issues fixed  
✅ Supabase KV Store connected  
✅ Storage bucket auto-initialization  
✅ Public endpoints working  
✅ Auth system configured  
✅ **Credentials configured and ready to deploy**

---

## 🚀 ШВИДКИЙ СТАРТ

### **→ Читайте [START_HERE.md](START_HERE.md) для початку роботи!**

### Deployment за 5 хвилин:
1. **[VERCEL_QUICKSTART.md](VERCEL_QUICKSTART.md)** - Покрокові інструкції deployment
2. **[QUICK_REFERENCE.md](QUICK_REFERENCE.md)** - Швидкий доступ до credentials та commands
3. **[DOCUMENTATION_INDEX.md](DOCUMENTATION_INDEX.md)** - Повна навігація по всій документації

---

**🚀 Готово до deployment! Дивись [VERCEL_QUICKSTART.md](VERCEL_QUICKSTART.md)**

See [FIXES.md](FIXES.md) for details on recent bug fixes.

## 🎨 Особливості

- ✅ **Дашборди** для викладача та студентів
- ✅ **Управління матеріалами** з підтримкою PDF, Audio, Video, Links
- ✅ **Cloud Storage** через Supabase для завантаження файлів
- ✅ **Progress Tracking** з чекбоксами "Виконано"
- ✅ **Multi-select призначення** матеріалів студентам
- ✅ **Google Drive інтеграція** з автоконвертацією посилань
- ✅ **Inline Preview** для PDF та Video в glassmorphism модалях
- ✅ **Supabase Auth** для входу студентів
- ✅ **KV Store** для постійного збереження даних
- ✅ **Testimonials & Pricing** CMS
- ✅ **Пастельний дизайн** (#cce9ff синій, #f7d7de рожевий)

## 🚀 Deployment на Vercel

### Швидкий старт (3 кроки):

1. **Push код на GitHub**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```

2. **Deploy на Vercel**
   - Перейдіть на https://vercel.com/new
   - Import вашого GitHub репозиторію
   - Додайте environment variables (дивись нижче)
   - Deploy!

3. **Environment Variables для Vercel:**
   ```
   SUPABASE_URL=https://xukykdgkzerkeygxbmhm.supabase.co
   SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzMwNTU2NDAsImV4cCI6MjA4ODYzMTY0MH0.2G9OUYEM3gxhrIM1SzQVQvqoB-gBqOv8OkP5K3sZWlI
   SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTc3MzA1NTY0MCwiZXhwIjoyMDg4NjMxNjQwfQ.9upYM5aM1TN-MkJH0XHGYtsRvgkWX6LuEeoZgxstomE
   ```

**📖 Детальні інструкції:** [VERCEL_QUICKSTART.md](VERCEL_QUICKSTART.md)

## 🗄️ Database Architecture

Платформа використовує **Supabase KV Store** для зберігання всіх даних:

### Префікси ключів:
- `resource:*` - Навчальні матеріали
- `student:*` - Профілі студентів
- `progress:*` - Прогрес виконання завдань
- `vocabulary:*` - Словниковий запас студентів
- `testimonial:*` - Відгуки
- `settings:pricing` - Налаштування цін
- `settings:policy` - Політика платформи

### Storage:
- Bucket: `make-e9e9da7b-resources`
- Файли завантажуються в структуру: `{userId}/{filename}`

## 📊 API Endpoints

### Authentication
- `POST /auth/signup` - Реєстрація (автопідтвердження email)

### Resources
- `GET /resources` - Всі ресурси
- `GET /resources/student/:id` - Ресурси студента
- `POST /resources` - Створити ресурс
- `PUT /resources/:id` - Оновити ресурс
- `DELETE /resources/:id` - Видалити ресурс

### Students
- `GET /students` - Всі студенти
- `GET /students/:id` - Студент за ID
- `POST /students` - Створити студента
- `PUT /students/:id` - Оновити студента
- `DELETE /students/:id` - Видалити студента

### Progress
- `GET /progress` - Весь прогрес
- `GET /progress/student/:id` - Прогрес студента
- `POST /progress` - Оновити прогрес

### Vocabulary
- `GET /vocabulary/student/:id` - Словник студента
- `POST /vocabulary` - Додати слово
- `PUT /vocabulary/:id` - Оновити слово
- `DELETE /vocabulary/:id` - Видалити слово

### Settings
- `GET /pricing` - Отримати ціни
- `PUT /pricing` - Оновити ціни
- `GET /policy` - Отримати політику
- `PUT /policy` - Оновити політику
- `GET /testimonials` - Отримати відгуки
- `POST /testimonials` - Додати відгук

## 🔐 Authentication Flow

1. **Sign Up:**
```typescript
import { signUp } from './lib/supabase-auth';

const result = await signUp(email, password, {
  name: "Ім'я Прізвище",
  role: 'student' // or 'teacher'
});
```

2. **Sign In:**
```typescript
import { signIn, storeSession } from './lib/supabase-auth';

const result = await signIn(email, password);
if (result.success && result.session) {
  storeSession(result.session);
}
```

3. **Sign Out:**
```typescript
import { signOut } from './lib/supabase-auth';

await signOut();
```

## 📁 File Upload

```typescript
import { uploadFile } from './lib/storage';

const result = await uploadFile(file, userId);
if (result.success) {
  console.log('File URL:', result.url);
}
```

## 🎯 Initial Data

При першому запуску автоматично створюються:
- ✅ Pricing settings (індивідуальні та групові уроки)
- ✅ Policy settings (правила скасування, оплати, тощо)
- ✅ Sample testimonials (4 відгуки)

**Примітка:** Resources та Students потребують авторизації і мають бути додані після входу викладача.

## 🛠️ Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS v4
- **Backend:** Supabase Edge Functions (Deno + Hono)
- **Database:** Supabase Postgres (KV Store)
- **Storage:** Supabase Storage
- **Auth:** Supabase Auth
- **Routing:** React Router v7
- **UI Components:** shadcn/ui
- **Icons:** Lucide React

## 📝 Next Steps

1. ✅ Отримати `SUPABASE_SERVICE_ROLE_KEY` з Dashboard
2. ✅ Додати environment variables у Vercel
3. ✅ Deploy на Vercel
4. ✅ Створити акаунт викладача через `/login`
5. ✅ Додати студентів та матеріали
6. ✅ Налаштувати ціни та політику (якщо потрібно змінити дефолтні)

## 🎨 Design System

- **Primary Blue:** `#cce9ff` (світло-блакитний)
- **Accent Pink:** `#f7d7de` (ніжно-рожевий)
- **Glassmorphism:** `backdrop-blur-xl bg-white/80`
- **Rounded:** `rounded-3xl` для карток, `rounded-xl` для інпутів
- **Shadows:** `shadow-xl` для модалів

## 📞 Support

Для питань та підтримки: [Контактна інформація]

---

**Зроблено з ❤️ для AnyWay to English**