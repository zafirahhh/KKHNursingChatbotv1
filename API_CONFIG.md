# API Configuration Documentation

## Environment Detection

The frontend automatically detects whether it's running locally or in production:

- **Local Development**: `http://127.0.0.1:8000`
- **Production (Render)**: `https://kkhnursingchatbot.onrender.com`

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/ask` | POST | Submit a question and get an AI response |
| `/quiz` | GET | Generate a nursing quiz with parameters |
| `/quiz/evaluate` | POST | Evaluate quiz answers and get results |
| `/suggest` | POST | Get follow-up question suggestions |
| `/` | GET | Health check endpoint |

## Frontend Configuration

The frontend uses these JavaScript constants defined in `js/app.js`:

```javascript
const BASE_API_URL = isLocalDevelopment 
  ? "http://127.0.0.1:8000" 
  : "https://kkhnursingchatbot.onrender.com";

const BACKEND_URL_FINAL = `${BASE_API_URL}/ask`;
const QUIZ_URL_FINAL = `${BASE_API_URL}/quiz`;
const QUIZ_EVAL_URL_FINAL = `${BASE_API_URL}/quiz/evaluate`;
const SUGGEST_URL_FINAL = `${BASE_API_URL}/suggest`;
```

## CORS Configuration

The backend allows requests from:
- `http://127.0.0.1:5500` (Local development)
- `http://localhost:5500` (Local development)  
- `https://kkhnursingchatbot.onrender.com` (Production frontend)
- `https://*.onrender.com` (Render deployment wildcard)

## Deployment Notes

1. **Frontend**: Deployed to `https://kkhnursingchatbot.onrender.com`
2. **Backend**: Should be deployed to the same domain or a separate backend service
3. **Environment Variables**: Make sure `OPENROUTER_API_KEY` is set in Render environment
4. **Build Commands**: Ensure both frontend and backend are properly deployed

## Testing

- **Local**: Access `http://localhost:5500` or `http://127.0.0.1:5500`
- **Production**: Access `https://kkhnursingchatbot.onrender.com`
- **API Health**: Check `https://kkhnursingchatbot.onrender.com/` for backend status
