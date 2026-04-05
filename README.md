# Moodwave — AI Music Recommender

> AI-powered music recommendations for every feeling

Moodwave is a web application that uses artificial intelligence to generate personalized music recommendations based on your current mood and language preference. Simply describe how you're feeling, select your preferred music language, and let AI find the perfect songs for you.

## Features

- 🎵 **AI-Powered Recommendations** — Uses Llama 3.3 via Groq API for intelligent mood-to-music matching
- 🌍 **Multi-Language Support** — Get recommendations in English, Bengali, Hindi, and more
- 💝 **Emotion-Aware Matching** — Analyzes mood across dimensions (energy, valence, tempo, themes)
- 🎨 **Modern, Responsive Design** — Sleek interface that works on desktop and mobile
- 🔗 **Direct Music Links** — Spotify and YouTube links for each recommendation
- ⚡ **Fast & Lightweight** — Vanilla JavaScript, no build steps required

## How It Works

1. Select your preferred **music language**
2. Describe your current **mood** (use suggestions or type your own)
3. Click **"Get 5 Songs"** to generate recommendations
4. Click on **Spotify** or **YouTube** links to listen

The AI analyzes your mood across multiple dimensions and recommends authentic, culturally significant songs that match your emotional state.

## Setup

### Prerequisites

- **Groq API Key** — Sign up for free at [console.groq.com](https://console.groq.com)
- **Web Browser** — Any modern browser (Chrome, Firefox, Safari, Edge)
- **No installation required** — Just open `index.html`

### Configuration

1. Get a free Groq API key from [console.groq.com](https://console.groq.com)
2. Open `index.html` in a text editor
3. Find this line (around line 170):
   ```javascript
   const GROQ_API_KEY = 'GROQ_API_KEY_PLACEHOLDER';
   ```
4. Replace `'GROQ_API_KEY_PLACEHOLDER'` with your actual API key:
   ```javascript
   const GROQ_API_KEY = 'gsk_your_actual_key_here';
   ```
5. Save the file and open it in your browser

### Optional: CORS Proxy

If you encounter CORS errors, you can set up a proxy server:

1. Configure the `PROXY_URL` variable in `index.html`:
   ```javascript
   const PROXY_URL = 'https://your-proxy-url.com/groq';
   ```
2. The application will route API requests through your proxy instead of calling Groq directly

## Project Structure

```
mood-to-playlist/
├── index.html          # Main application file (HTML + CSS + JavaScript)
├── README.md           # This file
└── requirements.md     # Setup and dependency requirements
```

## Technology Stack

- **Frontend**: HTML5, CSS3, Vanilla JavaScript
- **AI API**: [Groq](https://groq.com/) with Llama 3.3 70B model
- **Fonts**: Google Fonts (Playfair Display, DM Sans)
- **Deployment**: Static HTML — works on any web server

## Supported Languages

- English
- Bengali
- Hindi
- *(More languages can be added to the language selector)*

## API Details

- **Model**: `llama-3.3-70b-versatile`
- **Endpoint**: `https://api.groq.com/openai/v1/chat/completions`
- **Max Tokens**: 1200
- **Temperature**: 0.6 (balanced creativity)

## Customization

### Add More Languages

Edit the language dropdown in `index.html` (around line 125):

```html
<option value="Your Language">Your Language</option>
```

### Customize Mood Suggestions

Edit the mood chips (around line 135):

```html
<button type="button" class="chip" data-mood="Your Mood">Your Mood</button>
```

### Style Customization

All colors, fonts, and spacing are defined in the CSS variables at the top of the `<style>` tag:

```css
:root {
  --ink: #0d0d12;
  --accent: #6c47ff;
  /* ... more variables ... */
}
```

## Error Handling

The application includes error handling for:
- Missing form inputs
- API errors (with specific error messages)
- Invalid API responses
- CORS issues (with proxy fallback)

## Browser Compatibility

- Chrome/Chromium (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Performance

- **Load Time**: <2 seconds
- **API Response**: 2-5 seconds (depends on Groq API)
- **Bundle Size**: ~15KB (single HTML file)

## Future Enhancements

- Playlist export to Spotify/Apple Music
- Mood history and analytics
- Genre-based filtering
- Collaborative recommendations
- Offline mode with cached recommendations

## License

This project is open source and available for personal and educational use.

## Support

For issues or questions:
1. Check that your Groq API key is correctly configured
2. Verify you have a valid API key with sufficient quota
3. Check browser console (F12 → Console) for detailed error messages
4. Ensure your browser allows cross-origin requests (CORS)

## Credits

- Built with [Groq](https://groq.com/) API
- Model: [Meta Llama 3.3 70B](https://www.llama.com/)
- Fonts: [Google Fonts](https://fonts.google.com/)

---

**Made with 🎵 by the Moodwave team**
