# OpenRouter API Migration

This project has been updated to use OpenRouter's Zephyr-7B-Beta API instead of a local LM Studio instance.

## Setup Instructions

1. **Get an OpenRouter API Key:**
   - Visit [OpenRouter.ai](https://openrouter.ai/)
   - Create an account and generate an API key

2. **Configure Environment Variables:**
   - Copy `.env.example` to `.env`
   - Replace `your_openrouter_api_key_here` with your actual API key
   
   ```bash
   cp .env.example .env
   # Edit .env and add your API key
   ```

3. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the Application:**
   ```bash
   python backend.py
   ```

## API Changes Made

- **Endpoint:** Changed from `http://100.96.212.48:1234/v1/chat/completions` to `https://openrouter.ai/api/v1/chat/completions`
- **Authentication:** Added Bearer token authentication using `OPENROUTER_API_KEY`
- **Model:** Updated to use `openrouter/zephyr-7b-beta`
- **Error Handling:** Updated error messages to reflect OpenRouter API instead of LM Studio

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `OPENROUTER_API_KEY` | Your OpenRouter API key | Yes |

## Features Unchanged

- Embedding-based knowledge retrieval using sentence-transformers
- Chunk-based context generation
- Quiz generation and evaluation logic
- CORS configuration
- All existing endpoints and functionality
