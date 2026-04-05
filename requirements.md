# Moodwave — Requirements & Setup Guide

## System Requirements

### Minimum Requirements
- **OS**: Windows, macOS, or Linux
- **Browser**: Any modern web browser released in the last 2 years
- **Internet**: Required for API calls and font loading
- **Storage**: ~50KB (single HTML file)

### Supported Browsers
- ✅ Chrome/Chromium 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

## Software & API Requirements

### 1. Groq API Access (Required)

This project requires a **free Groq API key** to function.

**Steps to get your API key:**

1. Visit [console.groq.com](https://console.groq.com/keys)
2. Create a free account (or sign in)
3. Navigate to the **API Keys** section
4. Click **Create API Key**
5. Copy the generated key (format: `gsk_...`)
6. Paste it into `index.html` line ~170: `const GROQ_API_KEY = 'your_key_here';`

**Free Tier Limits:**
- Rate limit: 30 requests per minute (RPM)
- Monthly quota: 6,000 requests
- Models available: Llama 3.3 70B (and others)

### 2. Node.js (Optional - for development/proxy only)

If you want to run a local CORS proxy, Node.js is required:

- **Version**: 16.0.0 or higher
- **Download**: [nodejs.org](https://nodejs.org/)
- **Check installation**: `node --version`

**Why a proxy might be needed:**
- Direct browser-to-Groq API calls may fail due to CORS restrictions
- A proxy server acts as an intermediary

### 3. Text Editor (Required)

To edit the API key, you need a text editor:

- **VS Code** (recommended) — [code.visualstudio.com](https://code.visualstudio.com/)
- **Sublime Text** — [sublimetext.com](https://www.sublimetext.com/)
- **Atom** — [atom.io](https://atom.io/)
- **Notepad++** — [notepad-plus-plus.org](https://notepad-plus-plus.org/)
- Or any simple text editor (Notepad, TextEdit, nano, etc.)

## Installation Steps

### Option 1: Direct File Access (Fastest)

```bash
# 1. Navigate to the project directory
cd mood-to-playlist/mood-to-playlist/

# 2. Open index.html in your browser
# On Windows:
start index.html

# On macOS:
open index.html

# On Linux:
xdg-open index.html
```

### Option 2: Local Web Server

For better compatibility and to avoid CORS issues:

**Using Python 3:**
```bash
cd mood-to-playlist/mood-to-playlist/
python -m http.server 8000

# Then open: http://localhost:8000
```

**Using Python 2:**
```bash
python -m SimpleHTTPServer 8000
```

**Using Node.js (http-server):**
```bash
npm install -g http-server
cd mood-to-playlist/mood-to-playlist/
http-server

# Then open the URL shown (usually http://localhost:8080)
```

**Using Live Server (VS Code Extension):**
1. Install "Live Server" extension in VS Code
2. Right-click `index.html` → "Open with Live Server"
3. Browser opens automatically

## Configuration Requirements

### 1. API Key Configuration

**File**: `index.html` (line ~170)

**Find:**
```javascript
const GROQ_API_KEY = 'GROQ_API_KEY_PLACEHOLDER';
```

**Replace with:**
```javascript
const GROQ_API_KEY = 'gsk_your_actual_key_here';
```

### 2. Proxy Configuration (Optional)

If you experience CORS errors, set up a proxy:

**File**: `index.html` (line ~169)

**Default (no proxy):**
```javascript
const PROXY_URL = '';
```

**With proxy:**
```javascript
const PROXY_URL = 'https://api.example.com/proxy';
```

## Dependency List

### External Dependencies

| Dependency | Type | Source | Notes |
|---|---|---|---|
| Groq API | Cloud Service | [groq.com](https://groq.com/) | Required for AI recommendations |
| Llama 3.3 70B | AI Model | Groq-hosted | Inference engine for music recommendations |
| Google Fonts | CDN | [fonts.googleapis.com](https://fonts.googleapis.com/) | Playfair Display, DM Sans fonts |

### Browser APIs Required

| API | Purpose | Support |
|---|---|---|
| Fetch API | API calls to Groq | All modern browsers |
| DOM Level 3 | UI manipulation | All modern browsers |
| CSS Grid/Flexbox | Layout | All modern browsers |
| ES6 JavaScript | Application logic | All modern modern browsers |

### Local Dependencies

None. The application is a single HTML file with embedded CSS and JavaScript. No build tools, package managers, or external libraries needed.

## Network Requirements

### Connectivity
- **Required**: Stable internet connection
- **Bandwidth**: ~50KB per request (minimal)
- **Latency**: Works best with <200ms ping

### Third-Party Connections

The application connects to:

1. **Groq API** (`api.groq.com`)
   - For music recommendations
   - Uses your API key for authentication

2. **Google Fonts** (`fonts.googleapis.com`, `fonts.gstatic.com`)
   - For typography
   - Blocked in some regions (fallback fonts included)

3. **Spotify** (optional links)
   - User clicks only; embedded in recommendations

4. **YouTube** (optional links)
   - User clicks only; embedded in recommendations

### Firewall/Proxy Settings

If behind a corporate firewall:

1. Whitelist `api.groq.com`
2. Whitelist `fonts.googleapis.com`
3. Allow CORS preflight requests (OPTIONS method)
4. If blocked, set up a corporate proxy server and configure `PROXY_URL`

## Performance Requirements

| Metric | Target | Notes |
|---|---|---|
| Initial Load | <2s | Depends on browser cache and fonts |
| API Response | 2-5s | Groq processing time |
| Recommendation Display | <500ms | Local rendering |

## Storage Requirements

| Item | Size | Notes |
|---|---|---|
| HTML file | ~15KB | Includes CSS and JavaScript |
| Google Fonts | ~40KB | Cached after first load |
| Browser Cache | ~100KB | Typical - varies |

## Security Considerations

### API Key Safety

⚠️ **Warning**: Embedding your API key directly in HTML exposes it publicly.

**For production use:**
1. Set up a backend server to handle API calls
2. Store the API key server-side (environment variable)
3. Have the frontend call your server, not Groq directly
4. This prevents API key exposure and enables rate limiting

**Example backend proxy in Node.js:**
```javascript
app.post('/api/recommendations', async (req, res) => {
  const response = await fetch('https://api.groq.com/...', {
    headers: { Authorization: `Bearer ${process.env.GROQ_API_KEY}` },
    // ...
  });
  res.json(await response.json());
});
```

### CORS Handling

- Direct Groq API calls may fail due to browser CORS restrictions
- Solution: Use a proxy server or configure CORS headers
- Local testing via `file://` protocol may have limitations

## Troubleshooting

### Issue: "API error 401"
- **Cause**: Invalid or missing API key
- **Fix**: Verify your Groq API key is correct and has quota

### Issue: "CORS error"
- **Cause**: Browser blocking cross-origin requests
- **Fix**: 
  1. Use a local web server (not `file://` protocol)
  2. Set up a CORS proxy
  3. Configure backend API endpoint

### Issue: "Cannot parse recommendations"
- **Cause**: API response format unexpected
- **Fix**: 
  1. Check browser console (F12 → Console)
  2. Verify Groq API is working
  3. Check model availability

### Issue: "Fonts not loading"
- **Cause**: No internet or blocked Google Fonts
- **Fix**: 
  1. Check internet connection
  2. Browser fallback fonts will be used
  3. Modify CSS to use system fonts only

## Deployment

### Static Hosting Options

Since this is a static HTML file, you can deploy to:

- **GitHub Pages** (free) — Push to `gh-pages` branch
- **Vercel** (free) — Drag and drop `index.html`
- **Netlify** (free) — Connect GitHub repo or drag and drop
- **AWS S3** (low cost) — Upload to CloudFront-enabled bucket
- **Firebase Hosting** (free tier available) — `firebase deploy`

### Deployment with Proxy Backend

For production, deploy with a backend server:

1. Backend: Node.js, Python, or any language
2. Frontend: Deploy to CDN
3. Backend: Deploy to your server or serverless platform (AWS Lambda, Google Cloud Functions, etc.)
4. Configure `PROXY_URL` to point to your backend

## Recommended Tech Stack for Production

```
Frontend:  HTML/CSS/JS → Netlify/Vercel
Backend:   Node.js/Express → Railway/Render
Database:  (Optional) PostgreSQL for user history
Auth:      (Optional) Firebase Auth or Auth0
```

## Version Compatibility

| Component | Minimum Version | Tested Version |
|---|---|---|
| Groq API | Latest | v1 |
| Llama Model | 3.3 | 3.3 70B Versatile |
| JavaScript | ES6 (2015) | ES2020+ |
| CSS | CSS3 | CSS3 + Grid/Flexbox |
| HTML | HTML5 | HTML5 |

## Support & Documentation

- **Groq API Docs**: [console.groq.com/docs](https://console.groq.com/docs)
- **Llama Model Info**: [llama.meta.com](https://www.llama.com/)
- **Browser Compatibility**: [caniuse.com](https://caniuse.com/)

---

**Last Updated:** April 2026

