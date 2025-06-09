# Quick Start Guide

Get the AI-Powered Coding Assistant running in 5 minutes!

## 🚀 Prerequisites Checklist

- [ ] Node.js 18+ installed
- [ ] PostgreSQL 14+ installed
- [ ] Git installed
- [ ] OpenAI API key ready

## 📋 5-Minute Setup

### 1. Clone & Install (1 minute)
```bash
# Clone the repository
git clone <repository-url>
cd ai-copilot

# Install dependencies
npm install
```

### 2. Configure Environment (2 minutes)
```bash
# Copy environment template
cp .env.example .env

# Edit .env file - Add these required values:
OPENAI_API_KEY=your_openai_api_key_here
DB_PASSWORD=choose_a_secure_password
JWT_SECRET=generate_random_string_here
```

### 3. Setup Database (1 minute)
```bash
# Create database (run in PostgreSQL)
createdb ai_copilot

# Initialize database schema
npm run db:init
```

### 4. Start Application (1 minute)
```bash
# Start both frontend and backend
npm run dev:full
```

### 5. Access Application
Open your browser and navigate to:
- **Application**: http://localhost:3000
- **API**: http://localhost:3001

## 🎯 First Steps

### 1. Guest Access
Click "Continue as Guest" to explore without registration

### 2. Create Account
1. Click "Sign Up"
2. Enter username, email, and password
3. Start using all features

### 3. Try Basic Features
```
You: Hello, can you help me write a Python function?
AI: Of course! What kind of function would you like to create?

You: Create a function to calculate fibonacci numbers
AI: Here's a Python function to calculate Fibonacci numbers...
```

## 🔑 Essential Commands

### Development
```bash
npm run dev        # Start frontend only
npm run server     # Start backend only
npm run dev:full   # Start both
```

### Database
```bash
npm run db:init    # Initialize database
npm run db:reset   # Reset database
```

### Testing
```bash
npm test           # Run tests
npm run lint       # Check code style
```

## 🎨 Key Features to Try

### 1. Chat with AI
- Type a message and press Enter
- Try: "Explain React hooks"

### 2. Code Generation
- Ask: "Create a REST API endpoint in Express"
- Watch real-time code generation

### 3. Model Switching
- Click model selector in sidebar
- Try different AI models

### 4. File Upload
- Drag and drop a code file
- Ask AI to analyze or improve it

### 5. External APIs
- Try: "What's the weather in New York?"
- Try: "Show me latest tech news"

## ⚡ Keyboard Shortcuts

- `Ctrl/Cmd + Enter` - Send message
- `Ctrl/Cmd + K` - Quick command
- `Ctrl/Cmd + /` - Toggle sidebar
- `Esc` - Close modals

## 🔧 Common Issues

### Port Already in Use
```bash
# Kill process on port 3000 or 3001
npx kill-port 3000 3001
```

### Database Connection Failed
```bash
# Check PostgreSQL is running
sudo systemctl status postgresql

# Verify credentials in .env
```

### Missing Dependencies
```bash
# Clear and reinstall
rm -rf node_modules package-lock.json
npm install
```

## 📖 Next Steps

1. **Explore Features**: See [Features Overview](./FEATURES.md)
2. **Read User Guide**: Check [User Guide](./USER_GUIDE.md)
3. **Configure Settings**: Read [Configuration](./CONFIGURATION.md)
4. **Deploy to Production**: See [Deployment Guide](./DEPLOYMENT.md)

## 🆘 Need Help?

- **Documentation**: You're in the right place!
- **Support Email**: support@lackadaisicalsecurity.com
- **FAQ**: See [Frequently Asked Questions](./FAQ.md)

---

**Happy Coding! 🚀**

---

**Document Version**: 1.0  
**Last Updated**: December 2024
