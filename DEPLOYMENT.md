# Deployment Guide for KKH Nursing Chatbot API

## Render Deployment

### Prerequisites
- GitHub repository with your code
- Render account (free tier available)
- LM Studio server accessible from the internet

### Step 1: Prepare Your Repository
1. Ensure all files are committed and pushed to GitHub
2. Make sure your LM Studio server is accessible from the internet
3. Update the LM Studio IP address in `backend.py` if needed

### Step 2: Deploy to Render
1. Go to [Render Dashboard](https://dashboard.render.com/)
2. Click "New" → "Web Service"
3. Connect your GitHub repository
4. Choose the repository: `KKHNursingChatbotv1`
5. Configure the service:
   - **Name**: `kkh-nursing-chatbot-api`
   - **Runtime**: `Docker`
   - **Region**: Choose closest to your users
   - **Branch**: `main`
   - **Build Command**: `docker build -t kkh-nursing-chatbot .`
   - **Start Command**: `uvicorn backend:app --host 0.0.0.0 --port $PORT`

### Step 3: Environment Variables
Set these environment variables in Render:
- `PORT`: `8000` (automatically set by Render)
- `PYTHONPATH`: `/app`

### Step 4: Health Check
The Dockerfile includes a health check that pings the root endpoint (`/`) every 30 seconds.

### Step 5: Access Your API
Once deployed, your API will be available at:
`https://your-service-name.onrender.com`

## Local Docker Testing

### Build the Docker image:
```bash
docker build -t kkh-nursing-chatbot .
```

### Run the container:
```bash
docker run -p 8000:8000 kkh-nursing-chatbot
```

### Test the API:
```bash
curl http://localhost:8000/
```

## API Endpoints

Once deployed, your API will have these endpoints:

- `GET /` - Health check
- `POST /ask` - Ask a nursing question
- `GET /quiz` - Generate quiz questions
- `POST /quiz/evaluate` - Evaluate quiz answers
- `POST /suggest` - Get follow-up suggestions
- `GET /quiz/history` - View question history
- `DELETE /quiz/history/{topic}` - Clear topic history

## Configuration Notes

### LM Studio Connection
- Ensure your LM Studio server is accessible from the internet
- Update the IP address in `backend.py` if your LM Studio server changes
- The current configuration uses: `http://100.96.212.48:1234`

### CORS Settings
The backend is configured to allow requests from:
- Local development servers
- Render deployment domains
- All origins (for development - restrict in production)

### Dependencies
The Docker image includes all necessary dependencies:
- Python 3.10
- FastAPI and Uvicorn
- FAISS with CPU support
- Sentence Transformers
- All build tools (cmake, swig, OpenBLAS)

## Troubleshooting

### Common Issues:
1. **Build fails**: Check that all dependencies are correctly specified in `requirements.txt`
2. **FAISS installation fails**: The Dockerfile includes all necessary build tools
3. **LM Studio connection fails**: Ensure your LM Studio server is accessible and running
4. **CORS errors**: Check the CORS configuration in `backend.py`

### Logs:
Check Render logs for any deployment or runtime issues:
- Go to your service dashboard
- Click on "Logs" tab
- Monitor for any errors during startup

## Security Considerations

For production deployment:
1. Restrict CORS origins to specific domains
2. Add API authentication if needed
3. Use environment variables for sensitive configuration
4. Enable HTTPS (automatically handled by Render)
5. Consider rate limiting for the API endpoints

## Scaling

Render's free tier includes:
- 512MB RAM
- 0.1 CPU cores
- 750 hours/month

For production use, consider upgrading to a paid plan for better performance and reliability.
