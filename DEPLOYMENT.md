# 🚀 Deployment Instructions for AnyWay to English

## Prerequisites

1. **Supabase Service Role Key** ✅ **ГОТОВО**
   - Project URL: https://xukykdgkzerkeygxbmhm.supabase.co
   - Service Role Key: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTc3MzA1NTY0MCwiZXhwIjoyMDg4NjMxNjQwfQ.9upYM5aM1TN-MkJH0XHGYtsRvgkWX6LuEeoZgxstomE
   - Anon Key: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzMwNTU2NDAsImV4cCI6MjA4ODYzMTY0MH0.2G9OUYEM3gxhrIM1SzQVQvqoB-gBqOv8OkP5K3sZWlI

2. **Vercel Account**
   - Sign up at https://vercel.com if you don't have an account
   - Connect your GitHub account

## Step-by-Step Deployment

### 1. Setup Environment Variables in Vercel

Go to your Vercel project settings and add these variables:

```bash
SUPABASE_URL=https://xukykdgkzerkeygxbmhm.supabase.co

SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzMwNTU2NDAsImV4cCI6MjA4ODYzMTY0MH0.2G9OUYEM3gxhrIM1SzQVQvqoB-gBqOv8OkP5K3sZWlI

SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a3lrZGdremVya2V5Z3hibWhtIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTc3MzA1NTY0MCwiZXhwIjoyMDg4NjMxNjQwfQ.9upYM5aM1TN-MkJH0XHGYtsRvgkWX6LuEeoZgxstomE

SUPABASE_DB_URL=postgresql://postgres.xukykdgkzerkeygxbmhm:YOUR_DB_PASSWORD@aws-0-eu-central-1.pooler.supabase.com:6543/postgres
```

⚠️ **Security Note:** Service Role Key має доступ до всіх даних - тримайте його в секреті!

### 2. Deploy to Vercel

**Option A: Using Vercel CLI**
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Deploy to production
vercel --prod
```

**Option B: Using Vercel Dashboard**
1. Push your code to GitHub
2. Go to https://vercel.com/new
3. Import your repository
4. Add environment variables (from step 1)
5. Click "Deploy"

### 3. Verify Deployment

After deployment, check:

1. **Frontend:** Visit your Vercel URL
2. **Backend API:** Test health endpoint:
   ```bash
   curl https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b/health
   ```
   Should return: `{"status":"ok"}`

3. **Storage:** Check if bucket was created:
   - Go to Supabase Dashboard > Storage
   - Look for bucket: `make-e9e9da7b-resources`

4. **Initial Data:** Check browser console for:
   ```
   Data initialization: Sample data initialized successfully
   ```

## Post-Deployment Setup

### 1. Create Teacher Account

1. Go to your deployed site
2. Navigate to `/login`
3. Click "Sign Up" (you'll need to create this UI or use signup endpoint)
4. Create account with:
   - Email: your-email@example.com
   - Password: strong-password
   - Metadata: `{ name: "Your Name", role: "teacher" }`

### 2. Add Students

Use the Teacher Dashboard to add students with their:
- Name
- Email
- Level (A0-C2)
- Goals
- Next lesson date

### 3. Upload Materials

1. Go to "Бібліотека матеріалів"
2. Click "Додати матеріал"
3. Either:
   - Paste Google Drive link, OR
   - Upload file directly to Supabase Storage
4. Assign to specific students or "Усім студентам"

### 4. Customize Pricing & Policy (Optional)

The system comes with default pricing and policy. To customize:

1. **Pricing:** Use Teacher Dashboard > Settings > Pricing
2. **Policy:** Use Teacher Dashboard > Settings > Policy

Default values are already set for:
- Individual lessons: 300-500 грн
- Group lessons: 250-300 грн
- Cancellation policy: 24 hours advance
- Payment methods: Cash, Card transfer, PayPal

## 🔍 Troubleshooting

### Issue: "Failed to create storage bucket"
**Solution:** 
- Check if `SUPABASE_SERVICE_ROLE_KEY` is set correctly in Vercel
- Verify the key from Supabase Dashboard

### Issue: "Unauthorized" errors
**Solution:**
- Make sure you're logged in
- Check if session is stored in localStorage
- Try logging out and back in

### Issue: "Resource not found" 
**Solution:**
- Run data initialization: Open browser console
- Check if error messages show in console
- Verify API endpoints are responding

### Issue: File upload fails
**Solution:**
- Check Storage bucket exists in Supabase Dashboard
- Verify file size is under 50MB
- Check browser console for detailed error

## 📊 Monitoring

### Check API Health
```bash
curl https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b/health
```

### View Server Logs
1. Go to Supabase Dashboard
2. Navigate to Edge Functions
3. Click on `make-server-e9e9da7b`
4. View logs for errors

### View Frontend Logs
1. Go to Vercel Dashboard
2. Select your project
3. Click "Logs" tab
4. Filter by deployment

## 🎉 Success Checklist

- [ ] Environment variables set in Vercel
- [ ] Frontend deployed and accessible
- [ ] Backend API responding (health check passes)
- [ ] Storage bucket created
- [ ] Initial data loaded (pricing, policy, testimonials)
- [ ] Teacher account created
- [ ] Students added
- [ ] Materials uploaded
- [ ] Students can log in and see materials
- [ ] Progress tracking works (checkboxes)
- [ ] File upload works

## 📞 Need Help?

- **Supabase Docs:** https://supabase.com/docs
- **Vercel Docs:** https://vercel.com/docs
- **React Router Docs:** https://reactrouter.com

---

**Готово до запуску! 🚀**