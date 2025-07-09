# Deployment Troubleshooting Guide

## Python 3.12 Optimization

### Benefits of Python 3.12
Since FAISS has been removed and replaced with sentence-transformers' semantic_search(), we can now use Python 3.12 which offers:
- Better performance and faster execution
- Improved error messages and debugging
- Native support for latest pydantic versions
- Better compatibility with modern ML libraries

### Solutions Implemented

#### 1. Updated Python Version
- **runtime.txt**: Specifies Python 3.12.0
- **Dockerfile**: Uses `python:3.12-slim` base image
- **Dockerfile.render**: Render-specific version with Python 3.12

#### 2. Modern Compatible Dependencies
Updated `requirements.txt` with Python 3.12 optimized versions:
```
fastapi>=0.104.1
uvicorn[standard]>=0.24.0
sentence-transformers>=2.2.2
requests>=2.31.0
pydantic>=2.5.0          # Latest stable version
python-multipart>=0.0.6
torch>=2.1.0            # Modern PyTorch
transformers>=4.35.0     # Latest transformers
numpy>=1.24.0           # Stable numpy
typing-extensions>=4.8.0 # Python 3.12 compatibility
```

#### 3. Optimized Docker Build
- Uses `--prefer-binary` flag to avoid compilation
- Minimal system dependencies
- Specific pip version (23.3.1) known to work well

### Deployment Options

#### Option A: Use Dockerfile.render (Recommended)
The `render.yaml` now points to `Dockerfile.render` which is optimized for Render's platform.

#### Option B: Manual Render Setup
1. Go to Render Dashboard
2. Create new Web Service
3. Connect GitHub repository
4. Use these settings:
   - **Runtime**: Docker
   - **Dockerfile Path**: `./Dockerfile.render`
   - **Build Command**: (leave empty)
   - **Start Command**: (leave empty, uses CMD from Dockerfile)

### If Issues Persist

#### Alternative 1: Use Python Runtime Instead of Docker
Change `render.yaml` to:
```yaml
services:
  - type: web
    name: kkh-nursing-chatbot-api
    runtime: python
    plan: starter
    buildCommand: pip install -r requirements.txt
    startCommand: uvicorn backend:app --host 0.0.0.0 --port $PORT
```

#### Alternative 2: Minimal Requirements
If compilation still fails, try this minimal `requirements.txt`:
```
fastapi==0.104.1
uvicorn[standard]==0.24.0
sentence-transformers==2.2.2
requests==2.31.0
pydantic==2.4.2
python-multipart==0.0.6
```

### Testing Locally

Test the Docker build locally:
```bash
docker build -f Dockerfile.render -t kkh-nursing-chatbot .
docker run -p 8000:8000 kkh-nursing-chatbot
```

### Common Error Messages and Solutions

1. **"maturin failed"** → Use pre-compiled wheels with `--prefer-binary`
2. **"pydantic-core compilation failed"** → Downgrade to pydantic 2.4.2
3. **"ForwardRef._evaluate() missing argument"** → Use Python 3.10.12
4. **"Rust compilation failed"** → Use `--only-binary=all` flag

### Environment Variables for Render

Set these in your Render dashboard:
- `PORT`: 8000 (auto-set by Render)
- `PYTHONPATH`: /app
- `PYTHON_VERSION`: 3.10.12 (if using Python runtime)

### Health Check

The API includes a health check at `/` that returns:
```json
{"message": "KKH Nursing Chatbot API is running."}
```

This helps Render determine if your service is healthy.
