# 🔧 Environment Variables Setup - Quick Fix

## ✅ What Just Happened

I've created the necessary `.env` files with placeholder values so your app won't crash. However, you need to add your actual Clerk keys to make authentication work.

## 🚀 Quick Setup (5 minutes)

### Step 1: Get Your Clerk Keys

1. Go to [Clerk Dashboard](https://dashboard.clerk.com/)
2. Sign up or log in to Clerk
3. Create a new application or select an existing one
4. Go to **API Keys** section
5. Copy both keys:
   - **Publishable Key** (starts with `pk_test_...`)
   - **Secret Key** (starts with `sk_test_...`)

### Step 2: Update Your Environment Files

#### Frontend `.env` (in project root):

```env
VITE_CLERK_PUBLISHABLE_KEY=pk_test_your_actual_key_here
```

Replace `pk_test_your_actual_key_here` with your actual Publishable Key from Clerk.

#### Backend `backend/.env`:

```env
MONGODB_URI=mongodb://localhost:27017/agrismart
PORT=5000
NODE_ENV=development
JWT_SECRET=your_jwt_secret_key_change_this_in_production
CLERK_SECRET_KEY=sk_test_your_actual_key_here
CORS_ORIGIN=http://localhost:5173
```

Replace `sk_test_your_actual_key_here` with your actual Secret Key from Clerk.

### Step 3: Configure Clerk Application Settings

In your Clerk Dashboard:

1. **Enable Email/Password Authentication:**
   - Go to **User & Authentication** → **Email, Phone, Username**
   - Enable **Email address**
   - Enable **Password**

2. **Set Redirect URLs:**
   - Go to **Paths**
   - Set the following:
     - Sign-in URL: `/login`
     - Sign-up URL: `/signup`
     - After sign-in URL: `/`
     - After sign-up URL: `/`

3. **Enable User Metadata:**
   - This is enabled by default, no action needed

### Step 4: Restart Your Application

After updating the `.env` files:

```bash
# Stop the app if it's running (Ctrl+C)

# Restart frontend (if you're running it separately)
npm run dev

# Restart backend (in a new terminal)
cd backend
npm start
```

## 📝 Files Created

✅ `/.env` - Frontend environment variables (with placeholder)
✅ `/.env.example` - Frontend environment template
✅ `/backend/.env` - Backend environment variables (with placeholder)
✅ `/backend/.env.example` - Backend environment template
✅ `/.gitignore` - Prevents committing sensitive files

## 🔒 Security Notes

- ⚠️ **NEVER** commit `.env` files to Git (they're now in `.gitignore`)
- ⚠️ The placeholder keys won't work for real authentication
- ⚠️ Change `JWT_SECRET` to a secure random string for production
- ⚠️ Keep your Clerk Secret Key private

## 🧪 Testing Without Clerk (Optional)

If you want to test the UI before setting up Clerk:

1. The app will now load without errors
2. You'll see a demo/placeholder mode
3. Some authentication features won't work until you add real Clerk keys

## ❓ Need Help?

- [Clerk Documentation](https://clerk.com/docs)
- [Clerk React Quickstart](https://clerk.com/docs/quickstarts/react)
- Check `CLERK_SETUP_GUIDE.md` for detailed setup instructions
- Check `QUICK_START.md` for full application setup

## 🎯 Next Steps

1. ✅ Environment files created (done)
2. 🔲 Get Clerk keys from dashboard
3. 🔲 Update `.env` files with real keys
4. 🔲 Restart application
5. 🔲 Test authentication flow

---

**Your app should now run without the environment variable error!** 🎉

Just remember to add your actual Clerk keys when you're ready to test authentication.
