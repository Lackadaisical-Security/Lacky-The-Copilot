# Lackadaisical Copilot - Privacy-First Coding Assistant

A comprehensive AI-powered coding assistant that runs locally with Ollama for complete privacy, or optionally connects to cloud AI providers. Built by Lackadaisical Security with privacy, security, and developer productivity in mind.

## 🔒 Privacy-First Design

- **Local AI Processing**: Uses Ollama by default for complete privacy
- **No Data Sharing**: Everything runs on your machine
- **Optional Cloud Models**: Connect to external APIs only when needed
- **Encrypted Storage**: All data is encrypted at rest
- **Zero Telemetry**: No usage data is collected or transmitted

## ✨ New Features

- **Enhanced Image Generation**: Multi-provider support with Automatic1111 and Ollama integration
- **Model Deduplication**: Clean, deduplicated model lists for better user experience
- **Improved UI/UX**: Better provider status reporting and enhanced error handling
- **Local Model Optimization**: Optimized storage and management for Ollama models

## 🚀 Quick Start with Ollama (Recommended)

### Prerequisites
- Node.js 18+ and npm
- Windows, macOS, or Linux

### 1. Clone and Install
```bash
git clone <repository-url>
cd lackadaisical-copilot
npm install
```

### 2. Set Up Ollama (Automated)
```bash
npm run setup-ollama
```

This script will:
- Check if Ollama is installed
- Start the Ollama service
- Pull recommended AI models
- Configure your environment
- Test the setup

### 3. Start the Application
```bash
npm run dev:full
```

### 4. Open Your Browser
Navigate to `http://localhost:3000`

## 🤖 AI Models

### Local Models (Ollama) - Default

#### General Purpose Models
- **Llama 3.2** - Latest and most capable model (2GB)
- **Llama 4 Maverick** - Advanced reasoning capabilities (244GB)
- **Mistral 7B** - High-performance general purpose (4.1GB)
- **Phi-3 Mini** - Compact reasoning model (2.2GB)
- **Llama 2 Uncensored** - Unrestricted content (3.8GB)
- **Dolphin LLaMA3 Omost** - Enhanced conversational model (3.9GB)
- **Neural Chat** - Optimized for natural conversations (4.3GB)
- **Nous Hermes** - Knowledge-focused model (3.9GB)

#### Coding Models
- **Code Llama** - Specialized for code generation (3.8GB)
- **DeepSeek Coder** - Advanced code assistant (2.7GB)
- **WizardCoder** - Expert programming assistant (4.7GB)
- **CodeQwen** - Multi-language code generation (3.9GB)
- **Stable Code** - Code completion specialist (3.3GB)

#### Image & Multimodal Models
- **LLaVA** - Vision capabilities for image analysis (4.7GB)
- **Bakllava** - Enhanced visual reasoning (5.1GB) 
- **Moondream** - Specialized visual analysis (1.9GB)

#### Creative & Specialized Models
- **poluramus/llama-3.2ft_flux-prompting_v0.5** - Flux AI prompt generation (3.3GB)
- **brxce/stable-diffusion-prompt-generator** - Optimized Stable Diffusion prompts (2.9GB)
- **impactframes/dolphin_llama3_omost** - Advanced visual descriptions (3.9GB)
- **Yi** - Multi-purpose Chinese-English model (2.6GB)
- **Qwen** - Advanced bilingual assistant (3.1GB)
- **Starling** - Instruction-optimized model (4.2GB)
- **Vicuna** - Conversational specialist (3.9GB)
- **Samantha** - Personality-enhanced assistant (3.6GB)
- **Zephyr** - Balanced performance and efficiency (3.3GB)

### Cloud Models (Optional)
- **OpenAI** - GPT-4, GPT-3.5 Turbo
- **Anthropic** - Claude 3 family
- **Google** - Gemini Pro, Gemini Flash
- **Groq** - Ultra-fast inference

## 📋 Features

### 🎯 Core AI Features
- **Chat Interface** - Natural language conversations
- **Code Assistant** - Generate, explain, and debug code
- **Model Selection** - Easy switching between AI models
- **Streaming Responses** - Real-time AI responses
- **Privacy Protection** - Comprehensive data protection
- **Image Generation** - Multi-provider image creation with Ollama enhancement

### 💻 Development Tools
- **Code Editor** - Integrated Monaco editor
- **Terminal** - Built-in terminal interface
- **File Explorer** - Project file management
- **Snippet Library** - Code snippet storage
- **Quality Dashboard** - Code analysis and metrics

### 🔧 Advanced Features
- **Voice Coding** - Speech-to-code functionality
- **Productivity Tracking** - Development metrics
- **Admin Panel** - System management
- **API Integration** - External service connections
- **Local Image Generation** - Create images with Automatic1111 and Ollama

### Local AI Integration
- **Local AI Integration**: Run entirely on your machine with Ollama for complete privacy and no API costs
- **Multi-Model Support**: Use local Ollama models or connect to OpenAI, Anthropic, Google, and other AI providers
- **Code Intelligence**: Get code suggestions, explanations, and automated refactoring

## 🛠️ Manual Setup

### Environment Configuration
Create a `.env` file:
```env
# Server Configuration
PORT=3001
FRONTEND_URL=http://localhost:3000

# Ollama Configuration (Local AI)
DEFAULT_AI_PROVIDER=ollama
DEFAULT_AI_MODEL=llama3.2:latest
OLLAMA_BASE_URL=http://localhost:11434

# Optional Cloud API Keys
OPENAI_API_KEY=your_openai_key_here
ANTHROPIC_API_KEY=your_anthropic_key_here
GOOGLE_API_KEY=your_google_key_here

# Privacy & Security
ENABLE_PRIVACY_MODE=true
ENABLE_ENCRYPTION=true
```

### Manual Ollama Installation
1. Download from [ollama.ai](https://ollama.ai/download)
2. Install and start the service:
   ```bash
   ollama serve
   ```
3. Pull recommended models:
   ```bash
   ollama pull llama3.2
   ollama pull codellama
   ollama pull mistral
   ollama pull phi3-mini
   ollama pull llava
   ```

## 🔧 Development

### Scripts
```bash
# Setup
npm run setup-ollama          # Automated Ollama setup
npm install                   # Install dependencies

# Development
npm run dev                   # Start frontend only
npm run server               # Start backend only
npm run dev:full             # Start both frontend and backend

# Build
npm run build                # Build for production
npm run start                # Start production server

# Ollama Management
npm run ollama:status        # Check Ollama models
npm run ollama:setup         # Pull recommended models
npm run ollama:pull <model>  # Pull specific model
```

### Project Structure
```
ai-copilot/
├── src/                     # Frontend React app
│   ├── components/          # UI components
│   ├── contexts/           # React contexts
│   └── utils/              # Utility functions
├── server/                  # Backend Node.js app
│   ├── routes/             # API routes
│   ├── services/           # Business logic
│   ├── models/             # Database models
│   └── middleware/         # Express middleware
├── scripts/                # Setup and utility scripts
└── docs/                   # Documentation
```

## 🔒 Privacy & Security

### Local Processing
- All AI processing happens on your machine with Ollama
- No data is sent to external servers by default
- Complete control over your code and conversations

### Data Protection
- End-to-end encryption for all stored data
- Secure session management
- Privacy-focused request handling
- Audit logging for security monitoring

### Optional Cloud Usage
- Cloud AI providers are opt-in only
- API keys stored locally and encrypted
- Configurable fallback chains
- Rate limiting and quota management

## 🌟 Key Benefits

### For Developers
- **Privacy-First**: Keep your code completely private
- **No Latency**: Local AI responses are instant
- **Offline Capable**: Works without internet connection
- **Cost-Effective**: No API fees for local models
- **Customizable**: Full control over AI models and behavior

### For Teams
- **Self-Hosted**: Deploy on your own infrastructure
- **Compliance**: Meet data privacy requirements
- **Scalable**: Add more models and resources as needed
- **Auditable**: Complete visibility into AI interactions

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License & Copyright

© 2025 Lackadaisical Security. All Rights Reserved.

This software and its documentation are proprietary and confidential.
Unauthorized use, reproduction, or distribution is strictly prohibited.

Website: [https://lackadaisical-security.com](https://lackadaisical-security.com)  
GitHub: [https://github.com/Lackadaisical-Security](https://github.com/Lackadaisical-Security)

See the [LICENSE](LICENSE) file for details.

## 🆘 Support

### Common Issues

**Ollama not starting:**
```bash
# Check if Ollama is installed
ollama --version

# Start Ollama service
ollama serve

# Check status
curl http://localhost:11434/api/version
```

**Model not found:**
```bash
# List installed models
ollama list

# Pull missing model
ollama pull llama3.2
```

**Port conflicts:**
- Frontend: Change port in `vite.config.js`
- Backend: Set `PORT` in `.env`
- Ollama: Set `OLLAMA_BASE_URL` in `.env`

### Getting Help
- Check the [Issues](../../issues) page
- Review the [Documentation](docs/)
- Join our community discussions

## 🔗 Links

- [Ollama Models](https://ollama.ai/library)
- [OpenAI API](https://platform.openai.com/api-keys)
- [Anthropic API](https://console.anthropic.com/)
- [Google AI Studio](https://makersuite.google.com/app/apikey)

---

**Built with ❤️ for privacy-conscious developers**

## Getting Started

### Option 1: Quick Start with Ollama (Recommended)

For a completely local, private AI experience:

1. Install [Ollama](https://ollama.ai/download)
2. Run the setup script: `.\start-with-ollama.ps1`
3. Open http://localhost:3000 in your browser

For more details, see [Ollama Integration Guide](OLLAMA_INTEGRATION.md).

### Option 2: Standard Setup

```bash
# Server Configuration
PORT=3001
FRONTEND_URL=http://localhost:3000

# Ollama Configuration (Local AI)
DEFAULT_AI_PROVIDER=ollama
DEFAULT_AI_MODEL=llama3.2:latest
OLLAMA_BASE_URL=http://localhost:11434

# Optional Cloud API Keys
OPENAI_API_KEY=your_openai_key_here
ANTHROPIC_API_KEY=your_anthropic_key_here
GOOGLE_API_KEY=your_google_key_here

# Privacy & Security
ENABLE_PRIVACY_MODE=true
ENABLE_ENCRYPTION=true
```
