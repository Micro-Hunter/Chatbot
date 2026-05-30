# BotForge Setup Guide - Groq Integration

## Overview
Your BotForge chatbot builder is now integrated with **Groq API** for free, fast AI responses. This guide walks you through setup, testing, and deployment.

---

## **1. Get Groq API Key (5 minutes)**

### Step 1a: Create Groq Account
1. Go to https://console.groq.com
2. Sign up with email (free)
3. Verify your email

### Step 1b: Generate API Key
1. Log in to Groq console
2. Navigate to **API Keys**
3. Click **Create New API Key**
4. Copy the key (you'll only see it once!)

---

## **2. Setup Backend Locally (10 minutes)**

### Step 2a: Install Node.js
- Download from https://nodejs.org/ (LTS version)
- Verify: `node --version` and `npm --version`

### Step 2b: Clone & Install
```bash
# Clone your repo
git clone https://github.com/Micro-Hunter/Chatbot.git
cd Chatbot

# Install dependencies
npm install
```

### Step 2c: Create .env File
```bash
# Create .env file in root directory
cp .env.example .env

# Edit .env and add your Groq API key
# Open .env and replace:
# GROQ_API_KEY=your_groq_api_key_here
```

**Windows users:** Create a file named `.env` in the Chatbot folder and paste:
```
GROQ_API_KEY=your_actual_groq_api_key_here
PORT=3000
```

### Step 2d: Test Locally
```bash
npm start
```

You should see:
```
BotForge backend running on http://localhost:3000
Groq API Key configured: true
```

✅ **Now your backend is running!**

---

## **3. Test the Chatbot Locally**

1. Open `index.html` in your browser (or use Live Server extension)
2. Create a new chatbot
3. Go to **Training** → **Text/Paste** → Click "Load Example"
4. Go to **Overview** → Try the chat
5. You should see responses from Groq API!

---

## **4. Deploy Backend (Choose One)**

### **Option A: Railway.app (Easiest) ⭐ Recommended**

#### Step 1: Connect GitHub
1. Go to https://railway.app
2. Sign up with GitHub
3. Click **New Project** → **Deploy from GitHub repo**
4. Select `Micro-Hunter/Chatbot`

#### Step 2: Add Environment Variable
1. In Railway dashboard, go to **Variables**
2. Click **Add Variable**
3. Key: `GROQ_API_KEY`
4. Value: Your Groq API key (paste the full key)
5. Click **Add**

#### Step 3: Deploy
1. Railway auto-deploys on push
2. Wait for "Deployment Successful" (green checkmark)
3. Go to **Deployments** → Click your deployment
4. Copy the **Public URL** (looks like `https://chatbot-production-xxxx.railway.app`)

#### Step 4: Update Frontend
Replace in `index.html` (search for line with `http://localhost:3000`):

**OLD (Line ~559 in sendMsg function):**
```javascript
fetch('http://localhost:3000/api/chat',{
```

**NEW:**
```javascript
fetch('https://your-railway-url.railway.app/api/chat',{
```

---

### **Option B: Render.com**

1. Go to https://render.com
2. Sign up with GitHub
3. Click **New** → **Web Service**
4. Select `Micro-Hunter/Chatbot`
5. Build command: (leave empty)
6. Start command: `npm start`
7. Add environment variable:
   - Key: `GROQ_API_KEY`
   - Value: Your Groq key
8. Deploy and update URL in `index.html`

---

### **Option C: Keep Running Locally**
If backend stays on `http://localhost:3000`, you can only use it locally. For public websites, you need Option A or B.

---

## **5. Final Testing**

### Test Chat in Builder
1. Open `index.html`
2. Create a bot
3. Add training data
4. Chat should work instantly

### Test Embed Code
1. Go to **Embed** section
2. Copy the embed code
3. Paste on any HTML page before `</body>`
4. The floating chatbot bubble should appear!

---

## **Troubleshooting**

| Problem | Solution |
|---------|----------|
| **"Connection error"** | Check backend is running (`npm start`) and URL is correct |
| **Groq API not working** | Verify `GROQ_API_KEY` in `.env` is correct (copy again from console.groq.com) |
| **Backend won't start** | Run `npm install` again, check Node.js version |
| **CORS error** | Make sure backend has `cors` enabled (already in server.js) |
| **Embed not working** | Check URL in `index.html` matches deployed backend URL |

---

## **Quick Commands**

```bash
# Start backend locally
npm start

# Install dependencies
npm install

# Check if backend is running
curl http://localhost:3000/health

# Test Groq API connection
curl -X POST http://localhost:3000/api/chat \
  -H "Content-Type: application/json" \
  -d '{"messages":[{"role":"user","content":"Hello"}],"system":"You are helpful"}'
```

---

## **File Structure**

```
Chatbot/
├── index.html          (Frontend - your chatbot builder UI)
├── server.js           (Backend - handles Groq API calls)
├── package.json        (Node dependencies)
├── .env                (Your Groq API key - KEEP SECRET!)
├── .env.example        (Template for .env)
├── .gitignore          (Don't push .env to GitHub!)
└── SETUP_GUIDE.md      (This file)
```

---

## **Security Notes**

⚠️ **IMPORTANT:**
- ✅ `.env` file is in `.gitignore` (won't push to GitHub)
- ✅ API key is hidden on backend (not exposed in HTML)
- ✅ Embedded widgets can't see your API key

---

## **Next Steps**

1. ✅ Add Groq key to `.env`
2. ✅ Run `npm install && npm start`
3. ✅ Test locally with `index.html`
4. ✅ Deploy to Railway/Render
5. ✅ Update URL in `index.html` for public embed code

**Questions?** Check the Groq docs: https://console.groq.com/docs

Enjoy your free AI chatbot! 🚀
