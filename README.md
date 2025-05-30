# AI-Powered Coding Assistant

A sophisticated AI-powered coding assistant with multi-model support, advanced coding features, web search capabilities, and real-time collaboration tools.

**Developed by Lackadaisical Security**

![AI Chatbot](https://img.shields.io/badge/React-18.2.0-blue) ![TypeScript](https://img.shields.io/badge/TypeScript-5.2.2-blue) ![Node.js](https://img.shields.io/badge/Node.js-Express-green) ![Socket.IO](https://img.shields.io/badge/Socket.IO-4.7.4-black) ![License](https://img.shields.io/badge/License-Proprietary-red.svg)

## ✨ Features

### 🤖 Multi-Model AI Support
- **OpenAI**: GPT-3.5 Turbo, GPT-4, GPT-4 Turbo, GPT-4 Vision
- **Anthropic**: Claude 3 Haiku, Sonnet, Opus
- **Google**: Gemini Pro, Gemini Pro Vision
- **Groq**: Llama2 70B, Mixtral 8x7B, Gemma 7B
- **Ollama**: Local model support

### 💻 Advanced Coding Features
- **Code Generation** - Generate code in any programming language
- **Code Analysis** - Analyze and explain existing code with quality metrics
- **File Operations** - Create, edit, and delete files through AI suggestions
- **Bug Fixing** - Intelligent debugging and error resolution
- **Test Generation** - Automated unit test creation
- **Documentation** - Generate comprehensive code documentation
- **Monaco Editor** - Full-featured code editor with IntelliSense
- **Code Quality Dashboard** - Real-time code quality assessment
- **Snippet Library** - Searchable, categorized code snippets

### 🔍 Enhanced Capabilities
- **Web Search** - Real-time web search integration (Bing/DuckDuckGo)
- **Image Generation** - Create images using DALL-E 3 and Stable Diffusion
- **Image Analysis** - Analyze and describe uploaded images
- **Code Examples** - Search for coding solutions and examples
- **Voice Coding** - Voice-driven development interface
- **Visual Code Generation** - Generate code from mockups

### ⚡ Real-time Features
- **Streaming Responses** - Live streaming of AI responses using Socket.IO
- **Model Switching** - Change AI models during conversations
- **Connection Status** - Real-time connection monitoring
- **Typing Indicators** - Live typing status
- **Collaborative Coding** - Real-time code collaboration

### 🌐 External Integrations
- **Weather Data** - Get current weather for any location
- **News Updates** - Fetch latest news or search specific topics
- **Wikipedia Search** - Access Wikipedia knowledge base
- **Document Analysis** - Upload and analyze documents with AI

### 🔐 Enterprise Features
- **Authentication System** - Secure JWT-based authentication
- **🛡️ Comprehensive Privacy Protection** - Enterprise-grade privacy system
  - **Multi-Level Anonymization** - Personal data detection and removal
  - **End-to-End Encryption** - Data encrypted in transit and at rest
  - **Anonymous Sessions** - Privacy-preserving user sessions
  - **Privacy-Aware Rate Limiting** - Intelligent traffic management
  - **Emergency Data Deletion** - Complete data removal on demand
  - **GDPR Compliance** - Full compliance with privacy regulations
- **Admin Panel** - Comprehensive user and system management
- **Role-Based Access** - User, Premium, and Admin roles
- **Activity Logging** - Complete audit trail
- **Productivity Analytics** - Developer productivity insights

### 🎨 Modern Interface
- **Mode Switching** - Toggle between Chat and Code Assistant modes
- **Model Selector** - Easy AI model selection and configuration
- **Beautiful UI** - Modern gradient design with smooth animations
- **Responsive Design** - Works perfectly on all devices
- **Real-time Status** - Live connection and model indicators
- **Dark/Light Theme** - Customizable theme support

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ 
- PostgreSQL 14+
- npm or yarn
- OpenAI API key (required)
- Weather API key (optional - from OpenWeatherMap)
- News API key (optional - from NewsAPI)

### Installation

1. **Clone and setup:**
```bash
git clone <your-repo>
cd ai-copilot
npm install
```

2. **Configure environment:**
```bash
cp .env.example .env
# Edit .env with your API keys and database credentials
```

3. **Initialize database:**
```bash
npm run db:init
```

4. **Start the application:**
```bash
# Start both frontend and backend
npm run dev:full

# Or start separately:
npm run server  # Backend (port 3001)
npm run dev     # Frontend (port 3000)
```

5. **Open your browser:**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:3001

## 📚 Documentation

- [Setup Guide](./SETUP.md) - Detailed installation and configuration
- [User Instructions](./INSTRUCTIONS.md) - Complete user guide
- [API Documentation](./docs/API.md) - API endpoints reference
- [Development Guide](./docs/DEVELOPMENT.md) - Contributing guidelines

## 🛠️ Technology Stack

### Frontend
- React 18 with TypeScript
- Socket.IO Client for real-time communication
- Monaco Editor for code editing
- Chart.js for analytics visualization
- React Router for navigation

### Backend
- Node.js with Express
- Socket.IO for WebSocket connections
- PostgreSQL database
- JWT authentication
- Multiple AI provider integrations

### Security
- Bcrypt password hashing
- JWT token authentication
- Rate limiting
- Input validation
- SQL injection prevention
- XSS protection

## 📱 Key Features Overview

### Code Quality Analysis
- Cyclomatic complexity analysis
- Maintainability index
- Test coverage tracking
- Security vulnerability scanning
- Performance bottleneck detection

### Productivity Tools
- File explorer with advanced search
- Integrated terminal
- Voice coding support
- Productivity analytics dashboard
- Code snippet management

### AI Capabilities
- Multi-model support
- Context-aware suggestions
- Natural language to code
- Code translation between languages
- Intelligent refactoring

## 🤝 Contributing

This is proprietary software owned by Lackadaisical Security. For internal contributors:

1. Create a feature branch
2. Make your changes
3. Submit a pull request
4. Ensure all tests pass

## 📄 License

This project is proprietary software owned by **Lackadaisical Security**.

**Copyright © 2025 Lackadaisical Security. All Rights Reserved.**

This software and associated documentation files are the proprietary and confidential property of Lackadaisical Security. This Software is protected by copyright laws and international copyright treaties, as well as other intellectual property laws and treaties.

**RESTRICTIONS:**
- No redistribution, copying, or distribution allowed
- No reverse engineering or decompilation permitted
- Authorized use only under separate license agreement
- Confidential and proprietary information - no disclosure to third parties

For licensing inquiries, please contact: licensing@lackadaisicalsecurity.com

## 👨‍💻 Author

**Lackadaisical Security**
- AI-Powered Development Solutions
- Advanced Coding Assistant Technology
- Enterprise Software Development

## 🆘 Support

For support and inquiries:
- Internal Support: support@lackadaisicalsecurity.com
- Documentation: See [INSTRUCTIONS.md](./INSTRUCTIONS.md)
- Bug Reports: Use internal issue tracker

## 🔮 Roadmap

See [ADDITIONAL_CODING_ENHANCEMENTS.md](./ADDITIONAL_CODING_ENHANCEMENTS.md) for the complete development roadmap and future features.

---

**Version**: 1.0.0  
**Last Updated**: December 2024
