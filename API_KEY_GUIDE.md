# Embedding Your Claude API Key

## Overview

To allow end users to use ADHD Quest without needing their own API key, you can embed your Anthropic API key directly in the application code.

## ⚠️ IMPORTANT SECURITY WARNING

**Anyone who downloads your .exe file can extract the API key!**

Even though the code is compiled, the API key will be visible in the bundled JavaScript files inside the application. With basic technical knowledge, anyone can:
1. Extract the .exe contents
2. Find the JavaScript bundle
3. Search for your API key

## How to Protect Yourself

### 1. Set Spending Limits (REQUIRED)

Before embedding your key:

1. Go to your Anthropic Console: https://console.anthropic.com/
2. Navigate to **Settings** → **Billing**
3. Set a **hard spending limit** (e.g., $5, $10, $20)
4. Enable email notifications for spending thresholds

This ensures that even if someone extracts and abuses your key, you won't be charged more than your limit.

### 2. Use a Dedicated API Key

- Create a separate API key just for this application
- Don't reuse the same key for other projects
- This way, if it's abused, you can revoke it without affecting other work

### 3. Monitor Usage

- Check your Anthropic dashboard regularly
- Watch for unexpected usage spikes
- Set up email alerts for spending thresholds

## How to Embed Your API Key

### Option 1: Direct Embedding (Simplest)

1. Open `src/services/aiService.js`
2. Find this line:
   ```javascript
   const EMBEDDED_API_KEY = 'YOUR_API_KEY_HERE';
   ```
3. Replace `'YOUR_API_KEY_HERE'` with your actual API key:
   ```javascript
   const EMBEDDED_API_KEY = 'sk-ant-api03-...';
   ```
4. Build the application:
   ```bash
   npm run electron:build:win
   ```

### Option 2: Environment Variable at Build Time (More Secure)

1. Create a `.env.production` file in the root directory:
   ```
   REACT_APP_ANTHROPIC_API_KEY=sk-ant-api03-...
   ```

2. Build the application:
   ```bash
   npm run electron:build:win
   ```

The environment variable will be baked into the build (still extractable, but slightly less obvious).

## Better Alternatives (For Future Versions)

### Option A: Backend Proxy (Most Secure)

Instead of embedding the key, create a simple backend:

1. Build a small Node.js server that holds the API key
2. Your Electron app sends requests to your server
3. Your server forwards requests to Anthropic
4. You can implement rate limiting, user authentication, etc.

**Pros:** API key stays secure on your server
**Cons:** Requires hosting a backend service

### Option B: Per-User API Keys

Let users add their own API keys in Settings:

1. Add a Settings field for "Claude API Key"
2. Store it securely in the app
3. Users who have their own key can use it
4. Users without a key see a link to sign up

**Pros:** No risk to you
**Cons:** Users need to get their own API keys

## What Happens After Embedding

Once you embed your key and build the app:

1. ✅ Users can download the .exe and use it immediately
2. ✅ No setup required on their end
3. ✅ AI task breakdown works out of the box
4. ⚠️ Your API usage/cost will increase as users use the app
5. ⚠️ Anyone can extract the key if they try

## Cost Estimation

With Claude Sonnet 4:
- ~$3 per million input tokens
- ~$15 per million output tokens

For task breakdown requests:
- Input: ~500 tokens per request
- Output: ~200 tokens per response
- Cost: ~$0.004 per task breakdown

If 100 users each create 25 tasks per month:
- 2,500 requests/month
- ~$10-15/month

**With a $5 spending limit, you'll support ~1,200 task breakdowns.**

## Recommended Approach

For a free app with embedded key:

1. **Set a $10-20/month spending limit** (supports ~2,500-5,000 tasks)
2. **Monitor usage weekly**
3. **If limit is hit too often:**
   - Increase limit if you're comfortable
   - Add a fallback mock mode when API fails
   - Consider Option A (backend proxy) or Option B (user keys)

## Current Implementation

The app already has a **fallback mode**! If the API key is missing or quota is exceeded:
- The app will use mock/generic subtask breakdowns
- Users can still use the app, just without AI-powered task breakdown
- All other features (XP, timers, notes, etc.) work normally

This means even if you hit your spending limit, the app continues to function!

## Summary

✅ **DO:**
- Set spending limits before embedding your key
- Use a dedicated API key for this app only
- Monitor usage regularly
- Build with the embedded key

❌ **DON'T:**
- Embed a key without spending limits
- Use your primary/production API key
- Assume the key is secure in the .exe

## Questions?

See the main README or ELECTRON_BUILD_GUIDE for more information about building and distributing the app.
