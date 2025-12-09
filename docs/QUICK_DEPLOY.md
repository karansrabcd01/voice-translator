# 🚀 Quick Start - Render Deployment

Follow these commands in order to deploy your app to Render.

## Step 1: Configure Git (First Time Only)
```powershell
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## Step 2: Add Files to Git
```powershell
git add .
```

## Step 3: Commit Your Code
```powershell
git commit -m "Initial commit - Ready for deployment"
```

## Step 4: Create GitHub Repository
1. Go to: https://github.com/new
2. Repository name: `voice-translator`
3. Make it Public
4. Don't initialize with anything
5. Click "Create repository"

## Step 5: Push to GitHub
```powershell
git remote add origin https://github.com/YOUR-USERNAME/voice-translator.git
git branch -M main
git push -u origin main
```
**Replace YOUR-USERNAME with your GitHub username!**

## Step 6: Deploy on Render
1. Go to: https://render.com
2. Sign up with GitHub
3. Click "New +" → "Web Service"
4. Connect your repository
5. Configure:
   - Name: `voice-translator`
   - Build Command: `pip install -r requirements.txt`
   - Start Command: `uvicorn app:app --host 0.0.0.0 --port $PORT`
   - Add Environment Variable:
     - Key: `GROQ_API_KEY`
     - Value: `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`
6. Click "Create Web Service"

## Step 7: Wait for Deployment
- Watch the logs
- Wait for "Application startup complete"
- Your app is live!

## Step 8: Get Your URL
- Copy the URL from Render dashboard
- Add `/docs` to see API documentation
- Example: `https://voice-translator-xxxx.onrender.com/docs`

---

## 📝 Important Notes

⚠️ **NEVER commit your .env file to GitHub!**
✅ The .gitignore file already prevents this

⚠️ **Your GROQ_API_KEY is visible in this file**
✅ Delete this file after deployment or remove the API key

⚠️ **Free tier spins down after 15 minutes**
✅ First request after inactivity takes 30-60 seconds

---

## 🔄 Update Your Deployed App

After making changes:
```powershell
git add .
git commit -m "Description of changes"
git push
```

Render will automatically redeploy!

---

## 🆘 Troubleshooting

**Build failed?**
- Check Render logs
- Verify requirements.txt is correct
- Make sure environment variables are set

**Can't push to GitHub?**
- Check your GitHub username in the remote URL
- Make sure you're logged into GitHub
- Try: `git remote -v` to see configured remotes

**App not starting?**
- Check GROQ_API_KEY is set in Render
- Check logs for error messages
- Verify Python version matches runtime.txt

---

For detailed instructions, see: RENDER_DEPLOYMENT_STEPS.md
