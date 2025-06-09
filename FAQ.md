# Frequently Asked Questions (FAQ)

## General Questions

### What is the AI-Powered Coding Assistant?
The AI-Powered Coding Assistant is a comprehensive development environment that combines advanced AI models, real-time collaboration, code analysis, and productivity tools to enhance your coding experience. Developed by Lackadaisical Security, it supports multiple programming languages and integrates with various AI providers.

### Which AI models are supported?
We support multiple AI providers and models:
- **OpenAI**: GPT-3.5 Turbo, GPT-4, GPT-4 Turbo, GPT-4 Vision
- **Anthropic**: Claude 3 Haiku, Sonnet, Opus
- **Google**: Gemini Pro, Gemini Pro Vision
- **Groq**: Llama2 70B, Mixtral 8x7B, Gemma 7B
- **Ollama**: Local models for privacy-focused development

### Is my code secure and private?
Yes, we take security seriously:
- All communications are encrypted using TLS 1.3
- Code is not stored unless explicitly saved by you
- JWT-based authentication protects your account
- Optional local model support for sensitive projects
- Comprehensive audit logging for enterprise users

### What programming languages are supported?
We support 50+ programming languages including:
- **Full support**: JavaScript, TypeScript, Python, Java, C++, C#, Go, Rust, Ruby, PHP
- **Syntax highlighting**: 40+ additional languages
- **AI assistance**: Available for all major languages

### Can I use this offline?
Partial offline support is available:
- Local Ollama models work completely offline
- Cached responses remain available
- Code editor and analysis tools work offline
- External APIs and cloud AI models require internet

## Account & Billing

### Do I need an account to use the assistant?
No, you can use basic features as a guest. However, an account provides:
- Saved conversations and code
- Productivity analytics
- Custom settings sync
- Access to premium features
- Priority support

### What are the different subscription tiers?
| Tier | Features | Price |
|------|----------|-------|
| **Guest** | Basic chat, limited API calls | Free |
| **User** | Full features, 100 API calls/hour | Free |
| **Premium** | Advanced models, 500 API calls/hour, priority support | $19/month |
| **Enterprise** | Unlimited usage, admin panel, SSO, dedicated support | Contact us |

### How do I upgrade my account?
1. Log in to your account
2. Go to Settings → Subscription
3. Choose your plan
4. Enter payment details
5. Enjoy premium features immediately

### Can I cancel my subscription anytime?
Yes, you can cancel anytime. You'll retain access until the end of your billing period.

## Technical Questions

### What are the system requirements?
**Minimum Requirements:**
- Modern web browser (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)
- 4GB RAM
- Stable internet connection (for AI features)

**Recommended:**
- 8GB+ RAM
- High-speed internet
- 1920x1080 or higher resolution

### How do I set up API keys?
1. Obtain API keys from providers:
   - OpenAI: https://platform.openai.com/api-keys
   - Weather: https://openweathermap.org/api
   - News: https://newsapi.org
2. Add to `.env` file:
   ```
   OPENAI_API_KEY=your_key_here
   WEATHER_API_KEY=your_key_here
   NEWS_API_KEY=your_key_here
   ```
3. Restart the application

### Why am I getting "Rate limit exceeded" errors?
Rate limits protect the service and ensure fair usage:
- **Guest**: 20 requests/hour
- **User**: 100 requests/hour
- **Premium**: 500 requests/hour

Solutions:
1. Wait for the limit to reset (hourly)
2. Upgrade to a higher tier
3. Use more efficient queries
4. Enable response caching

### How do I report a bug?
1. Check if it's already reported: github.com/lackadaisical/ai-copilot/issues
2. Gather information:
   - Steps to reproduce
   - Error messages
   - Browser/OS details
   - Screenshots
3. Submit via:
   - GitHub Issues
   - Email: bugs@lackadaisicalsecurity.com
   - In-app feedback button

## Feature Questions

### How does voice coding work?
Voice coding uses speech recognition to convert natural language into code:
1. Click the microphone icon
2. Speak clearly: "Create a function called calculateTotal"
3. AI generates the code
4. Review and accept changes

Supported commands:
- Create functions/classes
- Add variables
- Import modules
- Navigate code
- Refactor existing code

### Can multiple people collaborate on the same code?
Yes, real-time collaboration is supported:
1. Start a collaboration session
2. Share the session link
3. All participants see live changes
4. Built-in voice chat available
5. Session recording for playback

### How accurate is the code analysis?
Our code analysis uses multiple techniques:
- **Static analysis**: Catches ~95% of common issues
- **AI-powered review**: Identifies complex patterns
- **Security scanning**: OWASP-based vulnerability detection
- **Performance profiling**: Real-time bottleneck detection

Accuracy improves with usage as the AI learns your patterns.

### What external APIs are integrated?
Current integrations:
- **Weather**: Real-time weather data (OpenWeatherMap)
- **News**: Latest news articles (NewsAPI)
- **Wikipedia**: Knowledge base search
- **Web Search**: Coming soon (Bing/DuckDuckGo)

### How do I use custom prompts?
1. Go to Settings → Prompts
2. Create new prompt template
3. Use variables: `{language}`, `{task}`, `{context}`
4. Save and select as active
5. Your AI responses will follow the template

## Troubleshooting

### The application won't load
Try these steps:
1. Clear browser cache (Ctrl+Shift+R)
2. Disable browser extensions
3. Check internet connection
4. Try incognito/private mode
5. Update your browser

### AI responses are slow
Possible causes and solutions:
1. **High demand**: Try different AI model
2. **Large context**: Reduce conversation size
3. **Network issues**: Check connection speed
4. **Server load**: Check status page

### Code editor is not working
1. Ensure JavaScript is enabled
2. Check browser console for errors
3. Try refreshing the page
4. Disable ad blockers
5. Update browser to latest version

### Can't connect to WebSocket
1. Check firewall settings
2. Ensure port 3001 is not blocked
3. Try disabling VPN
4. Check proxy settings
5. Contact IT if on corporate network

## Privacy & Security

### What data do you collect?
We collect minimal data:
- Account information (email, username)
- Usage analytics (anonymous)
- Error logs (for debugging)
- Conversation history (if logged in)

We never collect:
- Passwords (only hashed versions)
- Payment details (handled by Stripe)
- Personal files without permission
- Browsing history

### How long is my data retained?
- **Conversations**: 90 days (adjustable)
- **Analytics**: 1 year
- **Logs**: 30 days
- **Account data**: Until deletion requested

### Can I export my data?
Yes, under Settings → Privacy → Export Data:
- All conversations
- Code snippets
- Analytics data
- Account information

### How do I delete my account?
1. Go to Settings → Account
2. Click "Delete Account"
3. Confirm via email
4. All data deleted within 30 days

## Support

### How do I get help?
Support channels:
- **Documentation**: docs.lackadaisicalsecurity.com
- **Email**: support@lackadaisicalsecurity.com
- **Chat**: Available for premium users
- **Forum**: community.lackadaisicalsecurity.com

### What's included in premium support?
- 24/7 email support
- Live chat during business hours
- Priority issue resolution
- Direct access to engineers
- Custom training sessions

### Do you offer training?
Yes, we offer:
- Free video tutorials
- Live webinars (monthly)
- Premium 1-on-1 training
- Team workshops
- Certification program

### Is there a community?
Yes! Join our community:
- Discord: discord.gg/ai-copilot
- Forum: community.lackadaisicalsecurity.com
- GitHub Discussions
- Monthly virtual meetups

---

**Can't find your answer?**
- Search our docs: docs.lackadaisicalsecurity.com
- Contact support: support@lackadaisicalsecurity.com
- Ask the community: community.lackadaisicalsecurity.com

**Last Updated**: December 2024
