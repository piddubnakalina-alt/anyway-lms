# 🔑 How to Get Supabase Service Role Key

## ⚠️ Critical: You Need This Key for Deployment!

The `SUPABASE_SERVICE_ROLE_KEY` is required for:
- Creating/updating/deleting resources
- Managing students
- Creating user accounts
- Storage operations

Without this key, the backend will not work properly.

---

## 📝 Step-by-Step Instructions

### 1. Go to Supabase Dashboard

Open this link in your browser:
```
https://supabase.com/dashboard/project/xukykdgkzerkeygxbmhm/settings/api
```

Or manually:
1. Go to https://supabase.com
2. Sign in to your account
3. Select your project: `xukykdgkzerkeygxbmhm`
4. Click "Settings" in the sidebar
5. Click "API" section

### 2. Find the Service Role Key

On the API settings page, you'll see several keys:

- ❌ **anon/public key** - Already configured, public-facing
- ✅ **service_role key** - This is what you need!

The service_role key will look like:
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inh1a...
```

### 3. Copy the Key

1. Find the row labeled **"service_role"** or **"secret"**
2. Click the "Copy" button or select and copy the entire key
3. **⚠️ Keep this key secret!** Never commit it to git or share publicly

### 4. Add to Vercel

#### Option A: Vercel Dashboard
1. Go to https://vercel.com/dashboard
2. Select your project
3. Go to "Settings" → "Environment Variables"
4. Click "Add New"
5. Name: `SUPABASE_SERVICE_ROLE_KEY`
6. Value: Paste the copied key
7. Select environments: Production, Preview, Development
8. Click "Save"

#### Option B: Vercel CLI
```bash
vercel env add SUPABASE_SERVICE_ROLE_KEY
# Paste the key when prompted
```

### 5. Redeploy

After adding the environment variable:

```bash
vercel --prod
```

Or trigger a redeploy from Vercel Dashboard:
1. Go to "Deployments"
2. Click "..." on latest deployment
3. Click "Redeploy"

---

## 🔒 Security Best Practices

### ✅ DO:
- Store in environment variables only
- Use Vercel's encrypted environment variables
- Keep it secret and secure
- Rotate the key if compromised

### ❌ DON'T:
- Commit to git
- Share publicly
- Use in frontend code
- Log in console
- Include in screenshots

---

## 🧪 Verify It Works

After deployment, test the API:

```bash
# Health check (no auth needed)
curl https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b/health

# Should return: {"status":"ok"}
```

If you get errors:
1. Check Vercel logs for "SUPABASE_SERVICE_ROLE_KEY" errors
2. Verify the key was copied correctly (no extra spaces)
3. Make sure you redeployed after adding the variable

---

## 🆘 Troubleshooting

### "Missing SUPABASE_SERVICE_ROLE_KEY" Error

**Solution:**
1. Double-check the key is in Vercel environment variables
2. Ensure the name is exactly `SUPABASE_SERVICE_ROLE_KEY`
3. Redeploy the project

### "Invalid service_role key" Error

**Solution:**
1. Go back to Supabase Dashboard
2. Copy the key again (ensure no extra characters)
3. Update in Vercel
4. Redeploy

### "Cannot create bucket" Error

**Solution:**
1. The service_role key gives admin access
2. If bucket creation fails, check Supabase Storage quotas
3. Try creating bucket manually in Supabase Dashboard → Storage

---

## 📸 Screenshot Guide

### Step 1: Supabase Dashboard
![API Settings](https://supabase.com/docs/img/guides/api/api-settings.png)

Look for the "Project API keys" section.

### Step 2: Find Service Role
The key will be labeled:
- **service_role** or
- **secret** or
- **Service Role (secret)**

It's usually below the `anon` key.

### Step 3: Vercel Environment Variables
Add the key in the format:
```
Name: SUPABASE_SERVICE_ROLE_KEY
Value: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

---

## ✅ Checklist

Before deploying, ensure:

- [ ] Found service_role key in Supabase Dashboard
- [ ] Copied the entire key (no truncation)
- [ ] Added to Vercel environment variables
- [ ] Name is exactly `SUPABASE_SERVICE_ROLE_KEY`
- [ ] Selected all environments (Production, Preview, Development)
- [ ] Saved the environment variable
- [ ] Redeployed the project
- [ ] Tested API health endpoint
- [ ] Backend is responding correctly

---

## 🎉 Success!

Once configured, your backend will have full access to:
- ✅ Create/update/delete resources
- ✅ Manage student accounts
- ✅ Handle authentication
- ✅ Upload files to Storage
- ✅ Read/write KV store data

**You're ready to deploy! 🚀**
