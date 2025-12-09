# 🚀 Render Deployment Guide for Voice Translator

This guide will walk you through deploying your Voice Translator application to Render (free tier).

## 📋 Prerequisites

Before deploying, ensure you have:
- ✅ A GitHub account
- ✅ A Render account (sign up at https://render.com - it's free!)
- ✅ Your GROQ API key ready
- ✅ Git installed on your machine

## 🔧 Step 1: Prepare Your Repository

### 1.1 Check Git Status
```bash
git status
```

### 1.2 Add All Changes
```bash
git add .
```

### 1.3 Commit Your Changes
```bash
git commit -m "Prepare for Render deployment"
```

### 1.4 Create GitHub Repository
1. Go to https://github.com/new
2. Repository name: `voice-translator`
3. Description: "Real-time voice translation application"
4. Choose **Public** (required for Render free tier)
5. **DO NOT** initialize with README (you already have one)
6. Click "Create repository"

### 1.5 Link and Push to GitHub
After creating the repository, GitHub will show you commands. Use these:

```bash
# Add remote origin (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/voice-translator.git

# Verify remote was added
git remote -v

# Push to GitHub
git branch -M main
git push -u origin main
```

## 🌐 Step 2: Deploy on Render

### 2.1 Sign Up / Log In to Render
1. Go to https://render.com
2. Click "Get Started for Free"
3. Sign up using your GitHub account (recommended)

### 2.2 Create New Web Service
1. From Render Dashboard, click **"New +"** button
2. Select **"Web Service"**
3. Click **"Connect account"** to connect your GitHub (if not already connected)
4. Find and select your `voice-translator` repository
5. Click **"Connect"**

### 2.3 Configure Web Service

Fill in the following settings:

**Basic Settings:**
- **Name:** `voice-translator` (or your preferred name)
- **Region:** Choose closest to you (e.g., Oregon, Frankfurt)
- **Branch:** `main`
- **Root Directory:** `backend` ⚠️ **IMPORTANT!**
- **Runtime:** `Python 3`

**Build & Deploy Settings:**
- **Build Command:** `pip install -r requirements.txt`
- **Start Command:** `uvicorn app:app --host 0.0.0.0 --port $PORT`

**Instance Type:**
- Select **"Free"** plan

### 2.4 Add Environment Variables

Click on **"Advanced"** or scroll down to **"Environment Variables"**

Add the following:

| Key | Value |
|-----|-------|
| `PYTHON_VERSION` | `3.11.0` |
| `GROQ_API_KEY` | `your-actual-groq-api-key-here` |

⚠️ **IMPORTANT:** Replace `your-actual-groq-api-key-here` with your actual GROQ API key!

### 2.5 Deploy!
1. Click **"Create Web Service"** button
2. Render will start building your application
3. Wait 5-10 minutes for the first deployment (it needs to install all dependencies)

## 📊 Step 3: Monitor Deployment

### 3.1 Check Build Logs
- Render will show you real-time logs
- Look for "Build successful" message
- Then look for "Deploy successful" message

### 3.2 Common Issues & Solutions

**Issue: PyAudio installation fails**
- **Solution:** PyAudio requires system dependencies that aren't available on Render's free tier
- **Fix:** We'll need to remove PyAudio from requirements.txt since the backend API doesn't actually use it for recording (that's done client-side)

**Issue: Build timeout**
- **Solution:** The free tier has limited resources. If build times out, try again.

**Issue: Application error**
- **Check logs** for specific error messages
- **Verify** environment variables are set correctly

## ✅ Step 4: Test Your Deployment

### 4.1 Get Your URL
- After successful deployment, Render provides a URL like: `https://voice-translator-xxxx.onrender.com`
- Click on the URL to open your application

### 4.2 Test the API
Test the health endpoint:
```bash
curl https://your-app-name.onrender.com/health
```

You should see:
```json
{"status": "healthy"}
```

### 4.3 Test Translation Endpoint
```bash
curl -X POST https://your-app-name.onrender.com/translate \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello", "source_lang": "en", "target_lang": "hi"}'
```

## 🔄 Step 5: Update Your Frontend

After deployment, update your frontend to use the Render URL:

1. Open `frontend/script.js`
2. Find the API URL configuration
3. Replace `http://localhost:8000` with your Render URL: `https://your-app-name.onrender.com`
4. Commit and push changes
5. You can serve the frontend separately or deploy it to Netlify/Vercel

## 🔧 Step 6: Future Updates

Whenever you make changes:

```bash
# 1. Make your changes to the code
# 2. Add changes
git add .

# 3. Commit with a descriptive message
git commit -m "Description of your changes"

# 4. Push to GitHub
git push origin main

# 5. Render will automatically detect changes and redeploy!
```

## 🎯 Important Notes

### Free Tier Limitations:
- ⏰ **Spin down after 15 minutes of inactivity** - First request after inactivity takes 30-60 seconds
- 💾 **512 MB RAM** - Sufficient for this application
- ⚡ **Limited CPU** - May be slower than local development
- 🔄 **750 hours/month** - More than enough for testing

### Production Considerations:
- 🔐 **HTTPS is automatic** - Render provides SSL certificates
- 🌍 **CORS is configured** - Make sure your frontend URL is in the CORS settings
- 📝 **Logs are available** - Check them in Render dashboard
- 🔄 **Auto-deploy enabled** - Every push to main branch triggers deployment

## 🆘 Troubleshooting

### Application won't start?
1. Check logs in Render dashboard
2. Verify all environment variables are set
3. Ensure `backend` is set as root directory
4. Check that requirements.txt has all dependencies

### API not responding?
1. Check if service is "Live" in Render dashboard
2. Wait 30-60 seconds if it was sleeping
3. Check logs for errors
4. Verify GROQ_API_KEY is set correctly

### Need help?
- Check Render documentation: https://render.com/docs
- Check application logs in Render dashboard
- Review error messages carefully

## 🎉 Success!

Once deployed, your voice translator API will be accessible at:
`https://your-app-name.onrender.com`

You can now integrate this with your frontend or use it as a standalone API!

---

**Next Steps:**
1. Deploy frontend to Netlify or Vercel
2. Update frontend to use Render backend URL
3. Test end-to-end functionality
4. Share with friends! 🚀
