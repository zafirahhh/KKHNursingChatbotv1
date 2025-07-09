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
- **Code Structure:** Added centralized `get_llm_response()` function for all API calls with comprehensive error handling and logging

## New Functions Added

### `get_llm_response(messages, max_tokens=2000, temperature=0.7)`

A centralized function for making OpenRouter API calls with:
- Proper error handling and logging
- Support for OpenAI-compatible message format
- Configurable parameters (max_tokens, temperature)
- Detailed debug logging
- Helpful error messages for common issues

**Usage:**
```python
messages = [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "What is nursing?"}
]
response = get_llm_response(messages)
```

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
