# Troubleshooting Guide - JSON Parse Error

## Issue
Error: "Failed to reach server: Failed to execute 'json' on 'Response': Unexpected end of JSON input"

## Debugging Steps

### 1. Open Browser Console
Press `F12` or right-click → "Inspect" → "Console" tab

### 2. Check API Configuration
In the console, run:
```javascript
window.debugAPI.getCurrentConfig()
```

This will show:
- Current API URLs being used
- Whether it detected local vs production environment
- Active session information

### 3. Test API Health
In the console, run:
```javascript
await window.debugAPI.testHealth()
```

Expected response: `true` with health check data in console

### 4. Test Ask Endpoint
In the console, run:
```javascript
await window.debugAPI.testAsk("Hello")
```

Expected response: JSON object with a response field

### 5. Check Console Logs
Look for these logs in the console:
- `[CONFIG] Using API base URL: ...` - Shows which URL is being used
- `[API TEST] Testing connection to: ...` - Shows health check results
- `[Session Info]` - Shows session type and URL being called
- `[Response Status]` - Shows HTTP status codes
- `[Error Response Text]` or `[Non-JSON Response]` - Shows what the server actually returned

## Common Issues & Solutions

### 1. Wrong API URL
**Symptoms:** Connection errors, 404 responses
**Check:** Console shows `[CONFIG] Using API base URL: https://kkhnursingchatbot.onrender.com`
**Solution:** Verify your Render deployment URL is correct

### 2. Server Not Running
**Symptoms:** Network errors, timeout
**Check:** `window.debugAPI.testHealth()` returns false
**Solution:** Check Render deployment status, logs

### 3. Server Returns HTML Instead of JSON
**Symptoms:** "Unexpected end of JSON input" or "Failed to execute 'json'"
**Check:** Console shows `[Non-JSON Response]` with HTML content
**Common Causes:**
- Backend is serving static files but API routes aren't working
- Wrong deployment configuration
- Backend crashed and Render is showing error page

### 4. CORS Issues
**Symptoms:** CORS policy errors in console
**Check:** Network tab shows preflight OPTIONS requests failing
**Solution:** Update backend CORS configuration

### 5. Environment Detection Issues
**Symptoms:** Using wrong API URL
**Check:** `window.debugAPI.getCurrentConfig()` shows unexpected `isLocalDevelopment` value
**Solution:** Check if `window.location.hostname` matches expected values

## Environment Expectations

### Local Development
- URL: `http://localhost:5500` or `http://127.0.0.1:5500`
- API: `http://127.0.0.1:8000`
- Backend running locally with `python backend.py`

### Production (Render)
- URL: `https://kkhnursingchatbot.onrender.com`
- API: `https://kkhnursingchatbot.onrender.com`
- Backend deployed on Render

## Quick Fix Attempts

### 1. Force Production API URL
If environment detection is wrong, temporarily hardcode in `app.js`:
```javascript
const BASE_API_URL = "https://kkhnursingchatbot.onrender.com";
```

### 2. Test Individual Endpoints
Try accessing these URLs directly in browser:
- `https://kkhnursingchatbot.onrender.com/health` - Should return JSON
- `https://kkhnursingchatbot.onrender.com/` - Should return HTML (your frontend)

### 3. Check Render Logs
- Go to Render dashboard
- Check deployment logs for errors
- Look for FastAPI startup messages
- Check for any Python errors

## Report Back
When asking for help, please provide:
1. Output of `window.debugAPI.getCurrentConfig()`
2. Output of `window.debugAPI.testHealth()`
3. Any error messages from console
4. Current URL where you're accessing the app
5. Render deployment status
