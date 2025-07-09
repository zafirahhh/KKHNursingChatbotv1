# KKH Nursing Chatbot with Zephyr-7B-Beta + Semantic Search + Quiz System

## Objective
A fully functional nursing education chatbot for **KK Women's and Children's Hospital** that:
- Answers medical questions using a local knowledge base and Zephyr-7B-Beta LLM
- Supports an interactive quiz system with MCQs and detailed explanations
- Features a modern web interface with session management
- Uses semantic similarity search with sentence-transformers for accurate context retrieval
- Connects to LM Studio server for AI-powered responses

## Features
### Backend (FastAPI)
- **Knowledge Base**: Processes `nursing_guide_cleaned.txt` for medical knowledge
- **Semantic Search**: Uses sentence-transformers' semantic_search for context retrieval
- **AI Integration**: Connects to LM Studio server running Zephyr-7B-Beta
- **Session Management**: Tracks quiz sessions and chat history
- **Endpoints**:
  - `/ask`: Answer user questions with context-aware responses
  - `/quiz`: Generate topic-specific quiz questions
  - `/quiz/evaluate`: Evaluate answers and provide explanations
  - `/suggest`: Provide follow-up question suggestions

### Frontend (HTML/CSS/JS)
- **Modern UI**: ChatGPT-like interface with KKH branding
- **Responsive Design**: Mobile-friendly with sidebar navigation
- **Chat Sessions**: Separate chat and quiz session management
- **Interactive Quiz**: Multiple choice questions with instant feedback
- **Voice Input**: Microphone support for accessibility

## Setup
### Prerequisites
- Python 3.8+
- LM Studio running Zephyr-7B-Beta model
- Modern web browser

### Backend Setup
1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

2. Configure LM Studio:
   - Install and run LM Studio
   - Load the Zephyr-7B-Beta model
   - Ensure the server is accessible at your network IP
   - Update `backend.py` if needed to point to your LM Studio server

3. Run the FastAPI server:
   ```bash
   python backend.py
   ```
   Server will start at: `http://127.0.0.1:8000`

### Frontend Setup
1. Open `index.html` in a web browser
2. Or serve via local server:
   ```bash
   python -m http.server 5500
   ```
   Then visit: `http://127.0.0.1:5500`

## Project Structure
```
├── backend.py              # FastAPI server with all endpoints
├── index.html             # Main web interface
├── css/
│   ├── styles.css         # Styling for the web UI
│   └── KKH Logo.jpg       # Hospital logo
├── js/
│   ├── app.js            # Main frontend JavaScript
│   └── session-manager.js # Session management logic
├── data/
│   └── nursing_guide_cleaned.txt  # Medical knowledge base
├── requirements.txt       # Python dependencies
└── README.md             # This file
```

## Configuration
### LM Studio Connection
The backend is configured to connect to LM Studio server. Update the IP address in `backend.py` if your LM Studio is running on a different machine:

```python
# Current configuration (update as needed)
LM_STUDIO_URL = "http://100.96.212.48:1234/v1/chat/completions"
```

### CORS Settings
The backend allows requests from `http://127.0.0.1:5500`. Update the CORS origins in `backend.py` if serving from a different URL.

## Data Sources
- **Knowledge Base**: `data/nursing_guide_cleaned.txt` - Comprehensive nursing guide
- **Quiz Generation**: Dynamic quiz creation using LM Studio
- **Embeddings**: Uses `paraphrase-MiniLM-L3-v2` for semantic search

## Technologies Used
- **Backend**: FastAPI, Python
- **AI/ML**: LM Studio (Zephyr-7B-Beta), Sentence Transformers
- **Frontend**: HTML5, CSS3, Vanilla JavaScript
- **Dependencies**: See `requirements.txt`

## Features in Detail
### Chat Functionality
- Context-aware responses using semantic search
- Maintains conversation history
- Suggests follow-up questions
- Voice input support

### Quiz System
- Topic-specific quiz generation
- Multiple choice questions with 4 options
- Instant feedback and explanations
- Session management for multiple quizzes
- Question history to avoid duplicates

### UI/UX
- Modern, responsive design
- KKH hospital branding
- Mobile-friendly interface
- Sidebar navigation for chat/quiz sessions
- Real-time message updates

## Goal
Create a fast, accurate, and educational nursing chatbot specifically for KK Women's and Children's Hospital that helps nursing students and staff with:
- Quick access to nursing knowledge and procedures
- Interactive learning through dynamic quizzes
- Context-aware medical guidance
- 24/7 availability for nursing support

## Contributing
This project was developed for KKH nursing education. Contributions are welcome for:
- Additional nursing knowledge content
- UI/UX improvements
- New quiz topics and question types
- Performance optimizations

## License
Educational use for KK Women's and Children's Hospital nursing programs.
