# 📋 Quick Reference Guide

## 🔑 Essential Credentials

### Supabase
```
Project URL: https://xukykdgkzerkeygxbmhm.supabase.co
Anon Key: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzMwNTU2NDAsImV4cCI6MjA4ODYzMTY0MH0.2G9OUYEM3gxhrIM1SzQVQvqoB-gBqOv8OkP5K3sZWlI
Service Role: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTc3MzA1NTY0MCwiZXhwIjoyMDg4NjMxNjQwfQ.9upYM5aM1TN-MkJH0XHGYtsRvgkWX6LuEeoZgxstomE
```

---

## 🔗 Important URLs

| Service | URL |
|---------|-----|
| **Supabase Dashboard** | https://supabase.com/dashboard/project/xukykdgkzerkeygxbmhm |
| **Storage Buckets** | https://supabase.com/dashboard/project/xukykdgkzerkeygxbmhm/storage |
| **Edge Functions** | https://supabase.com/dashboard/project/xukykdgkzerkeygxbmhm/functions |
| **API Base** | https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b |
| **Health Check** | https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b/health |
| **Vercel New** | https://vercel.com/new |
| **Vercel Dashboard** | https://vercel.com/dashboard |

---

## 🚀 Deployment Commands

### GitHub
```bash
git init
git add .
git commit -m "Initial deployment"
git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

### Vercel CLI
```bash
npm i -g vercel
vercel login
vercel --prod
```

---

## 🔧 Environment Variables (для Vercel)

```bash
SUPABASE_URL=https://xukykdgkzerkeygxbmhm.supabase.co

SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzMwNTU2NDAsImV4cCI6MjA4ODYzMTY0MH0.2G9OUYEM3gxhrIM1SzQVQvqoB-gBqOv8OkP5K3sZWlI

SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTc3MzA1NTY0MCwiZXhwIjoyMDg4NjMxNjQwfQ.9upYM5aM1TN-MkJH0XHGYtsRvgkWX6LuEeoZgxstomE
```

---

## 🧪 Test Commands

### Health Check
```bash
curl https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b/health
```

### Get Resources
```bash
curl https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b/resources \
  -H "Authorization: Bearer ANON_KEY"
```

### Create Teacher Account
```bash
curl -X POST https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b/auth/signup \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ANON_KEY" \
  -d '{
    "email": "teacher@test.com",
    "password": "password123",
    "metadata": {
      "name": "Teacher Name",
      "role": "teacher"
    }
  }'
```

---

## 📂 KV Store Prefixes

| Prefix | Description |
|--------|-------------|
| `resource:*` | Навчальні матеріали |
| `student:*` | Профілі студентів |
| `progress:*` | Прогрес виконання |
| `vocabulary:*` | Словниковий запас |
| `testimonial:*` | Відгуки студентів |
| `settings:pricing` | Налаштування цін |
| `settings:policy` | Політика платформи |

---

## 🎯 API Endpoints

### Auth
- `POST /auth/signup` - Реєстрація

### Resources (auth required для POST/PUT/DELETE)
- `GET /resources`
- `GET /resources/student/:id`
- `POST /resources`
- `PUT /resources/:id`
- `DELETE /resources/:id`

### Students (auth required)
- `GET /students`
- `GET /students/:id`
- `POST /students`
- `PUT /students/:id`
- `DELETE /students/:id`

### Progress (auth required для POST)
- `GET /progress`
- `GET /progress/student/:id`
- `POST /progress`

### Vocabulary (auth required для POST/PUT/DELETE)
- `GET /vocabulary/student/:id`
- `POST /vocabulary`
- `PUT /vocabulary/:id`
- `DELETE /vocabulary/:id`

### Settings (first-time setup без auth, потім auth required)
- `GET /pricing`
- `PUT /pricing`
- `GET /policy`
- `PUT /policy`
- `GET /testimonials`
- `POST /testimonials` (public)

---

## 📱 Routes

### Public
- `/` - Landing page
- `/login` - Login/Signup

### Teacher (requires auth)
- `/teacher` - Teacher Dashboard
- `/teacher/students` - Student Management
- `/teacher/materials` - Materials Library
- `/teacher/grades` - Grades & Progress
- `/teacher/finance` - Finance Tracking
- `/teacher/schedule` - Schedule
- `/teacher/calendar` - Calendar View
- `/teacher/attendance` - Attendance Log
- `/teacher/messages` - Messages
- `/teacher/cms` - CMS Settings
- `/teacher/bio` - Teacher Bio

### Student (requires auth)
- `/student` - Student Dashboard
- `/student/materials` - Materials
- `/student/vocabulary` - Vocabulary Trainer
- `/student/homework` - Homework
- `/student/path` - Learning Path

---

## 🎨 Design Tokens

### Colors
```css
Primary Blue: #cce9ff
Accent Pink: #f7d7de
```

### Common Classes
```css
/* Cards */
.card: rounded-3xl bg-white/80 backdrop-blur-xl shadow-xl

/* Buttons */
.btn-primary: bg-[#cce9ff] hover:bg-[#b3dcff]
.btn-accent: bg-[#f7d7de] hover:bg-[#ffc4d1]

/* Inputs */
.input: rounded-xl border border-gray-200
```

---

## 🐛 Debugging

### Browser Console
```
F12 → Console
```

### Check Session
```javascript
localStorage.getItem('supabase_session')
```

### Clear Session
```javascript
localStorage.clear()
```

### Supabase Logs
Supabase Dashboard → Edge Functions → make-server-e9e9da7b → Logs

### Vercel Logs
Vercel Dashboard → Your Project → Logs

---

## 📚 Documentation Files

| File | Purpose |
|------|---------|
| `README.md` | Main overview |
| `VERCEL_QUICKSTART.md` | Quick deployment |
| `DEPLOYMENT.md` | Detailed guide |
| `API_REFERENCE.md` | API docs |
| `USER_GUIDE.md` | User manual |
| `READY_TO_DEPLOY.md` | Pre-deploy checklist |
| `SETUP_COMPLETE.md` | Confirmation |
| `FINAL_SETUP_SUMMARY.md` | Complete summary |
| `QUICK_REFERENCE.md` | This file |

---

## 🔍 Common Issues

### "Unauthorized" error
```
Рішення: Перевірити localStorage session, re-login
```

### Files not uploading
```
Рішення: Перевірити Storage bucket створено, розмір < 50MB
```

### Backend not responding
```
Рішення: Перевірити SUPABASE_SERVICE_ROLE_KEY в Vercel env vars
```

### Initial data not loading
```
Рішення: Перевірити browser console, health endpoint
```

---

## ✅ Post-Deploy Checklist

- [ ] Health endpoint повертає `{"status":"ok"}`
- [ ] Storage bucket `make-e9e9da7b-resources` створено
- [ ] Initial data завантажено (pricing, policy, testimonials)
- [ ] Teacher акаунт створено
- [ ] Можна додавати студентів
- [ ] Можна завантажувати матеріали
- [ ] Студенти можуть логінитись
- [ ] Progress tracking працює

---

**Швидкий доступ до всієї інформації для deployment та troubleshooting!** 🚀
