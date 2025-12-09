# 🔧 Backend - Real-Time Voice Translator API

FastAPI backend for real-time multilingual voice translation.

## 📁 Structure

```
backend/
├── app.py                  # Main FastAPI application
├── translation_graph.py    # Translation engine (LangChain + Groq)
├── audio_handler.py        # Audio processing (STT/TTS)
├── requirements.txt        # Python dependencies
├── runtime.txt            # Python version (3.11.0)
├── render.yaml            # Render deployment config
└── .env                   # Environment variables (NOT in git)
```

## 🚀 Quick Start

### Local Development

1. **Create virtual environment**
   ```bash
   python -m venv venv
   ```

2. **Activate virtual environment**
   - Windows:
     ```bash
     .\venv\Scripts\Activate
     ```
   - Mac/Linux:
     ```bash
     source venv/bin/activate
     ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**
   
   Create `.env` file:
   ```env
   GROQ_API_KEY=your_groq_api_key_here
   PORT=8000
   ```

5. **Run the server**
   ```bash
   uvicorn app:app --host 0.0.0.0 --port 8000 --reload
   ```

6. **Access the API**
   - API Root: http://localhost:8000
   - API Docs: http://localhost:8000/docs
   - OpenAPI: http://localhost:8000/openapi.json

## 📚 API Endpoints

### `GET /`
Health check and API information

**Response:**
```json
{
  "message": "Multilingual Real-time Translation API",
  "endpoints": {
    "websocket": "/ws/{room_id}",
    "translate": "/translate",
    "audio_translate": "/audio/translate"
  }
}
```

### `POST /translate`
Translate text between languages

**Request:**
```json
{
  "text": "Hello, how are you?",
  "source_lang": "en",
  "target_lang": "hi"
}
```

**Response:**
```json
{
  "translation": "नमस्ते, आप कैसे हैं?",
  "source_lang": "en",
  "target_lang": "hi"
}
```

### `POST /audio/translate`
Translate audio between languages

**Parameters:**
- `audio_file`: Audio file (multipart/form-data)
- `source_lang`: Source language code (default: "en")
- `target_lang`: Target language code (default: "hi")

**Response:**
```json
{
  "original_text": "Hello",
  "translated_text": "नमस्ते",
  "audio_base64": "base64_encoded_audio"
}
```

### `WebSocket /ws/{room_id}`
Real-time translation WebSocket

**Connect:**
```javascript
const ws = new WebSocket('ws://localhost:8000/ws/room123');
```

**Send Message:**
```json
{
  "type": "translate",
  "text": "Hello",
  "source_lang": "en",
  "target_lang": "hi"
}
```

**Receive Message:**
```json
{
  "type": "translate",
  "original": "Hello",
  "translated": "नमस्ते",
  "source_lang": "en",
  "target_lang": "hi"
}
```

## 🔑 Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `GROQ_API_KEY` | Groq API key for AI translation | Yes |
| `PORT` | Port number (auto-set by Render) | No |

## 📦 Dependencies

- **fastapi** - Web framework
- **uvicorn[standard]** - ASGI server
- **websockets** - WebSocket support
- **python-multipart** - File upload support
- **langchain** - LLM orchestration
- **langchain-core** - LangChain core
- **langchain-groq** - Groq integration
- **langgraph** - Graph-based workflows
- **python-dotenv** - Environment variables
- **SpeechRecognition** - Speech-to-text
- **gTTS** - Text-to-speech
- **pydub** - Audio processing
- **PyAudio** - Audio I/O

## 🌐 Deployment

### Deploy to Render

1. Push code to GitHub
2. Create new Web Service on Render
3. Connect GitHub repository
4. Set root directory to `backend`
5. Configure:
   - Build Command: `pip install -r requirements.txt`
   - Start Command: `uvicorn app:app --host 0.0.0.0 --port $PORT`
6. Add environment variable: `GROQ_API_KEY`
7. Deploy!

### Render Configuration

The `render.yaml` file is pre-configured for deployment:

```yaml
services:
  - type: web
    name: voice-translator
    env: python
    buildCommand: pip install -r requirements.txt
    startCommand: uvicorn app:app --host 0.0.0.0 --port $PORT
```

## 🧪 Testing

### Test with cURL

**Translate Text:**
```bash
curl -X POST http://localhost:8000/translate \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello", "source_lang": "en", "target_lang": "hi"}'
```

**Health Check:**
```bash
curl http://localhost:8000/
```

### Test with Python

```python
import requests

response = requests.post(
    "http://localhost:8000/translate",
    json={
        "text": "Hello, world!",
        "source_lang": "en",
        "target_lang": "hi"
    }
)
print(response.json())
```

## 🔧 Development

### Code Structure

- **app.py** - FastAPI app, routes, WebSocket handling
- **translation_graph.py** - LangChain graph for translation
- **audio_handler.py** - Audio processing utilities

### Adding New Languages

Edit `translation_graph.py` and add language codes to supported languages.

### CORS Configuration

CORS is configured to allow all origins. For production, update in `app.py`:

```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=["https://your-frontend-domain.com"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

## 📊 Performance

- **Response Time:** ~500ms average
- **Concurrent Connections:** Unlimited (WebSocket)
- **Rate Limits:** Based on Groq API limits

## 🆘 Troubleshooting

### Issue: Module not found
**Solution:** Install dependencies: `pip install -r requirements.txt`

### Issue: GROQ_API_KEY not set
**Solution:** Create `.env` file with your API key

### Issue: Port already in use
**Solution:** Change port: `uvicorn app:app --port 8001`

### Issue: CORS errors
**Solution:** Check CORS configuration in `app.py`

## 📝 License

MIT License

## 🔗 Links

- [FastAPI Documentation](https://fastapi.tiangolo.com)
- [LangChain Documentation](https://python.langchain.com)
- [Groq API](https://groq.com)
