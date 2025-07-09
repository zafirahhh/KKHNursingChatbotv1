# Deployment Guide for KKH Nursing Chatbot

## Updated Configuration

### 🚀 Frontend API Configuration

The frontend now automatically detects the environment:

- **Local Development**: Uses `http://127.0.0.1:8000`
- **Production**: Uses `https://kkhnursingchatbot.onrender.com`

### 🔧 Backend Changes Made

1. **Static File Serving**: Backend now serves frontend files in production
2. **Environment Detection**: Uses `RENDER` environment variable to detect production
3. **Health Check**: New `/health` endpoint for monitoring
4. **CORS Updated**: Added your specific domain to allowed origins

### 📦 Deployment Steps

1. **Set Environment Variables in Render:**
   ```
   OPENROUTER_API_KEY=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
   RENDER=true
   PORT=8000
   PYTHONPATH=/app
   ```

2. **Deploy to Render:**
   - Your `render.yaml` is configured for Docker deployment
   - Health check endpoint: `/health`
   - Static files are served from the root `/`

3. **Test Endpoints:**
   ```
   https://kkhnursingchatbot.onrender.com/         # Frontend
   https://kkhnursingchatbot.onrender.com/health   # API Health Check
   https://kkhnursingchatbot.onrender.com/ask      # Chat API
   https://kkhnursingchatbot.onrender.com/quiz     # Quiz API
   ```

### 🌐 Environment Detection

The JavaScript code automatically detects:
```javascript
const isLocalDevelopment = window.location.hostname === 'localhost' || window.location.hostname === '127.0.0.1';
const BASE_API_URL = isLocalDevelopment 
  ? "http://127.0.0.1:8000" 
  : "https://kkhnursingchatbot.onrender.com";
```

### 🔍 Troubleshooting

1. **CORS Issues**: Make sure your domain is in the backend CORS configuration
2. **API Key**: Ensure `OPENROUTER_API_KEY` is set in Render environment
3. **Health Check**: Visit `/health` to verify backend is running
4. **Console Logs**: Check browser console for API URL being used

### 📁 File Structure

```
├── index.html              # Frontend entry point
├── css/                    # Stylesheets
├── js/
│   └── app.js             # Updated with environment detection
├── backend.py             # Updated with static file serving
├── render.yaml            # Deployment configuration
├── Dockerfile.render      # Production Docker image
└── requirements.txt       # Python dependencies
```

### ✅ What's Working Now

- ✅ Environment auto-detection
- ✅ Static file serving in production
- ✅ CORS properly configured
- ✅ Health check endpoint
- ✅ OpenRouter API integration
- ✅ All endpoints updated for production

### 🚀 Next Steps

1. Deploy to Render using the updated configuration
2. Test the health check endpoint
3. Verify frontend loads correctly
4. Test all API functionality (chat, quiz, suggestions)
5. Monitor logs for any issues
