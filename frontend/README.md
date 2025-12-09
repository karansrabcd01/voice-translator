# 🎨 Frontend - Real-Time Voice Translator

Modern, responsive web interface for real-time multilingual voice translation.

## 📁 Structure

```
frontend/
├── index.html    # Main UI
├── app.js        # Client-side logic & WebSocket
└── styles.css    # Styling
```

## ✨ Features

- 🎤 **Voice Input** - Real-time speech recognition
- 🔊 **Voice Output** - Text-to-speech playback
- 💬 **Text Chat** - Type and translate
- 🌍 **Multi-Language** - English, Hindi, Telugu, Tamil, Kannada
- 🎨 **Modern UI** - Glassmorphism design
- 📱 **Responsive** - Works on all devices
- 🔄 **Real-Time** - WebSocket communication

## 🚀 Quick Start

### Option 1: Simple HTTP Server (Development)

From the project root:
```bash
python serve_frontend.py
```

Then open: http://localhost:3000

### Option 2: Live Server (VS Code)

1. Install "Live Server" extension
2. Right-click `index.html`
3. Select "Open with Live Server"

### Option 3: Python HTTP Server

```bash
cd frontend
python -m http.server 3000
```

## ⚙️ Configuration

### Backend API URL

Update the API URL in `app.js`:

**For Local Development:**
```javascript
const API_URL = 'http://localhost:8000';
```

**For Production:**
```javascript
const API_URL = 'https://your-backend.onrender.com';
```

## 🎯 Usage

### 1. Open the Application

Open two browser windows at http://localhost:3000

### 2. Join a Room

- Enter the same room code in both windows
- Example: `room123`

### 3. Select Languages

- Window 1: Select "English"
- Window 2: Select "Hindi"

### 4. Start Chatting

**Text Mode:**
- Type your message
- Click "Send" or press Enter
- See translation in real-time

**Voice Mode:**
- Click the microphone button
- Speak clearly
- See transcription and translation
- Hear audio in target language

## 🎨 UI Components

### Language Selector
```html
<select id="language">
  <option value="en">English</option>
  <option value="hi">Hindi</option>
  <option value="te">Telugu</option>
  <option value="ta">Tamil</option>
  <option value="kn">Kannada</option>
</select>
```

### Message Display
- **Your messages** - Right-aligned, blue
- **Translated messages** - Left-aligned, purple
- **System messages** - Center, gray

### Voice Controls
- 🎤 **Microphone** - Click to start/stop recording
- 🔊 **Speaker** - Auto-plays translated audio

## 🔧 Customization

### Change Colors

Edit `styles.css`:

```css
:root {
  --primary-color: #667eea;
  --secondary-color: #764ba2;
  --accent-color: #f093fb;
}
```

### Add New Language

1. Update language selector in `index.html`
2. Add language code to `app.js`
3. Ensure backend supports the language

### Modify Layout

Edit `index.html` structure and `styles.css` for custom layouts.

## 📱 Responsive Design

The UI adapts to different screen sizes:

- **Desktop** - Full layout with sidebar
- **Tablet** - Compact layout
- **Mobile** - Stacked layout

Breakpoints:
- Mobile: < 768px
- Tablet: 768px - 1024px
- Desktop: > 1024px

## 🌐 Deployment

### Deploy to Vercel

1. **Install Vercel CLI**
   ```bash
   npm install -g vercel
   ```

2. **Deploy**
   ```bash
   cd frontend
   vercel
   ```

3. **Configure**
   - Follow prompts
   - Set root directory to `frontend`
   - Deploy!

### Deploy to Netlify

1. Go to [netlify.com](https://netlify.com)
2. Drag and drop `frontend` folder
3. Update API URL in `app.js`
4. Done!

### Deploy with GitHub Pages

1. Push to GitHub
2. Go to repository settings
3. Enable GitHub Pages
4. Select `frontend` folder
5. Access at: `https://username.github.io/repo-name`

## 🔌 WebSocket Connection

### Connection Flow

```javascript
// Connect to WebSocket
const ws = new WebSocket(`ws://localhost:8000/ws/${roomId}`);

// Send message
ws.send(JSON.stringify({
  type: 'translate',
  text: 'Hello',
  source_lang: 'en',
  target_lang: 'hi'
}));

// Receive message
ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  console.log(data.translated);
};
```

## 🎤 Speech Recognition

Uses Web Speech API:

```javascript
const recognition = new webkitSpeechRecognition();
recognition.lang = 'en-US';
recognition.start();

recognition.onresult = (event) => {
  const transcript = event.results[0][0].transcript;
  console.log(transcript);
};
```

## 🔊 Text-to-Speech

Uses Web Speech API:

```javascript
const utterance = new SpeechSynthesisUtterance(text);
utterance.lang = 'hi-IN';
speechSynthesis.speak(utterance);
```

## 🐛 Troubleshooting

### Issue: Can't connect to backend
**Solution:** 
- Check backend is running
- Verify API_URL in `app.js`
- Check CORS settings

### Issue: Microphone not working
**Solution:**
- Grant microphone permissions
- Use HTTPS (required for production)
- Check browser compatibility

### Issue: No audio playback
**Solution:**
- Check browser audio permissions
- Verify speakers are working
- Try different browser

### Issue: WebSocket disconnects
**Solution:**
- Check internet connection
- Verify backend is running
- Check room code matches

## 🌍 Browser Compatibility

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| WebSocket | ✅ | ✅ | ✅ | ✅ |
| Speech Recognition | ✅ | ❌ | ✅ | ✅ |
| Text-to-Speech | ✅ | ✅ | ✅ | ✅ |
| Responsive Design | ✅ | ✅ | ✅ | ✅ |

**Recommended:** Chrome or Edge for full feature support

## 📊 Performance

- **Initial Load:** < 1s
- **WebSocket Latency:** < 100ms
- **Translation Time:** ~500ms
- **Voice Recognition:** Real-time

## 🎨 Design System

### Colors
- Primary: `#667eea` (Purple-Blue)
- Secondary: `#764ba2` (Purple)
- Accent: `#f093fb` (Pink)
- Background: `#0f0f23` (Dark Blue)

### Typography
- Font: System fonts (San Francisco, Segoe UI, Roboto)
- Sizes: 14px - 24px
- Weights: 400, 500, 600

### Effects
- Glassmorphism backgrounds
- Smooth transitions (0.3s)
- Hover effects
- Gradient borders

## 📝 License

MIT License

## 🔗 Links

- [Web Speech API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API)
- [WebSocket API](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)
- [Vercel Deployment](https://vercel.com/docs)
