# Ollama Local AI Integration Guide

## Overview

The AI Copilot now includes comprehensive support for local AI models through Ollama integration. This provides privacy-focused, offline-capable AI functionality with support for multiple high-performance models including Llama 2 Uncensored and Mistral 7B.

## Supported Models

### 🔥 Recommended Models

| Model | ID | Description | Size | Features |
|-------|----|-----------  |------|----------|
| **Llama 3.2** | `llama3.2` | Latest Llama model for general tasks | 2.0GB | Fast, efficient |
| **Llama 2 Uncensored** | `llama2-uncensored` | Unrestricted content generation | 3.8GB | Uncensored responses |
| **Code Llama** | `codellama` | Specialized for code generation | 3.8GB | Code-focused |
| **Mistral 7B** | `mistral:7b` | High-performance 7B parameter model | 4.1GB | Balanced performance |
| **Mistral** | `mistral` | General purpose Mistral model | 4.1GB | Versatile |

### ⚠️ Important Notes

- **Llama 2 Uncensored**: This model generates uncensored content. Use responsibly and in accordance with your organization's policies.
- **Storage Requirements**: Ensure you have sufficient disk space (10-15GB recommended for all models).
- **Performance**: Models run locally and performance depends on your hardware capabilities.

## Quick Setup

### 1. Install Ollama

First, install Ollama on your system:

**Windows:**
```powershell
# Download and install from https://ollama.ai/download
# Or use winget (if available)
winget install Ollama.Ollama
```

**macOS:**
```bash
brew install ollama
```

**Linux:**
```bash
curl -fsSL https://ollama.ai/install.sh | sh
```

### 2. Setup AI Copilot Models

Use our automated setup script:

```powershell
# Pull all recommended models
npm run ollama:setup

# Check model status
npm run ollama:status

# Pull a specific model
npm run ollama:pull llama2-uncensored
```

### 3. Start Ollama Server

```powershell
# Start Ollama server (runs on localhost:11434)
ollama serve

# Or use our startup script
./scripts/start-ollama.sh
```

## Manual Model Management

### Pull Individual Models

```powershell
# Core models
ollama pull llama3.2
ollama pull llama2-uncensored
ollama pull codellama
ollama pull mistral:7b

# Additional models
ollama pull mistral
ollama pull stable-diffusion
```

### List Installed Models

```powershell
ollama list
```

### Remove Models

```powershell
ollama rm <model-name>
```

## Configuration

### Environment Variables

Add to your `.env` file:

```env
# Ollama Configuration
OLLAMA_HOST=http://localhost:11434
OLLAMA_TIMEOUT=120000
OLLAMA_MAX_RETRIES=3

# Model Preferences
OLLAMA_DEFAULT_MODEL=llama3.2
OLLAMA_CODE_MODEL=codellama
OLLAMA_UNCENSORED_MODEL=llama2-uncensored
```

### Model Selection in UI

1. Open the AI Copilot application
2. Click on the model selector (gear icon)
3. Select "Ollama (Local)" as provider
4. Choose your preferred model
5. Configure temperature and max tokens as needed

## Usage Examples

### 1. General Chat with Llama 3.2

```javascript
// Frontend model selection
const config = {
  model: 'llama3.2',
  provider: 'ollama',
  temperature: 0.7,
  maxTokens: 2048,
  baseUrl: 'http://localhost:11434'
};
```

### 2. Code Generation with Code Llama

```javascript
// Specialized for code tasks
const codeConfig = {
  model: 'codellama',
  provider: 'ollama',
  temperature: 0.3,
  maxTokens: 4096,
  systemPrompt: 'You are a specialized coding assistant.'
};
```

### 3. Uncensored Content with Llama 2 Uncensored

```javascript
// For unrestricted responses
const uncensoredConfig = {
  model: 'llama2-uncensored',
  provider: 'ollama',
  temperature: 0.8,
  maxTokens: 2048,
  baseUrl: 'http://localhost:11434'
};
```

## API Integration

### Direct Ollama API

```typescript
// Direct API call to Ollama
const response = await fetch('http://localhost:11434/api/chat', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    model: 'llama2-uncensored',
    messages: [
      { role: 'user', content: 'Hello, how are you?' }
    ],
    stream: false
  })
});
```

### Through AI Copilot Service

```typescript
// Using MultiModelService
import { MultiModelService } from './server/services/multiModelService';

const modelService = new MultiModelService();

const response = await modelService.generateResponse(
  [{ role: 'user', content: 'Explain quantum computing' }],
  {
    model: 'mistral:7b',
    provider: 'ollama',
    temperature: 0.7,
    maxTokens: 2048,
    baseUrl: 'http://localhost:11434'
  }
);
```

## Performance Optimization

### Hardware Recommendations

**Minimum Requirements:**
- 8GB RAM
- 20GB free disk space
- Modern CPU (4+ cores)

**Recommended:**
- 16GB+ RAM
- 50GB+ free disk space
- GPU support (for faster inference)
- SSD storage

### Model-Specific Performance

| Model | RAM Usage | Speed | Quality |
|-------|-----------|-------|---------|
| llama3.2 | 4-6GB | Fast | Good |
| llama2-uncensored | 6-8GB | Medium | High |
| codellama | 6-8GB | Medium | Excellent (code) |
| mistral:7b | 8-12GB | Medium | High |
| mistral | 8-12GB | Medium | High |

## Troubleshooting

### Common Issues

**1. Ollama not found**
```powershell
# Check if Ollama is installed
ollama --version

# If not found, reinstall Ollama
```

**2. Connection refused**
```powershell
# Check if Ollama server is running
netstat -an | findstr 11434

# Start Ollama server
ollama serve
```

**3. Model not found**
```powershell
# List available models
ollama list

# Pull missing model
ollama pull <model-name>
```

**4. Out of memory errors**
```powershell
# Check system memory
wmic computersystem get TotalPhysicalMemory

# Use smaller models or adjust max_tokens
```

### Performance Issues

**Slow responses:**
- Reduce `maxTokens` parameter
- Use smaller models (llama3.2 instead of mistral:7b)
- Close other applications to free up memory
- Consider using GPU acceleration if available

**High memory usage:**
- Limit concurrent requests
- Use model-specific memory limits
- Monitor system resources

## Security Considerations

### Local Privacy Benefits

- **Data Privacy**: All processing happens locally
- **No API Keys**: No external API calls required
- **Offline Capability**: Works without internet connection
- **Custom Control**: Full control over model behavior

### Responsible Use Guidelines

1. **Uncensored Models**: Use responsibly and within legal/ethical boundaries
2. **Content Filtering**: Implement your own content filters if needed
3. **Data Handling**: Ensure compliance with your organization's data policies
4. **Model Updates**: Keep models updated for security and performance

## Integration with AI Copilot Features

### Model Selection Priority

The AI Copilot automatically selects the best model based on task type:

```typescript
const modelPriority = {
  'code-generation': 'codellama',
  'general-chat': 'llama3.2',
  'uncensored-content': 'llama2-uncensored',
  'complex-reasoning': 'mistral:7b',
  'default': 'llama3.2'
};
```

### Fallback Chain

When a model is unavailable, the system falls back to:
1. Primary Ollama model
2. Secondary Ollama model
3. External API providers (if configured)

### Streaming Support

All Ollama models support real-time streaming:

```typescript
const streamResponse = await modelService.generateResponse(
  messages,
  config,
  (chunk: string) => {
    console.log('Streaming chunk:', chunk);
  }
);
```

## Advanced Configuration

### Custom Model Parameters

```env
# Advanced Ollama settings
OLLAMA_TEMPERATURE_DEFAULT=0.7
OLLAMA_TEMPERATURE_CODE=0.3
OLLAMA_TEMPERATURE_CREATIVE=0.9
OLLAMA_MAX_TOKENS_DEFAULT=2048
OLLAMA_MAX_TOKENS_CODE=4096
OLLAMA_CONTEXT_WINDOW=4096
```

### Load Balancing

For high-usage scenarios, you can run multiple Ollama instances:

```powershell
# Instance 1 (port 11434)
ollama serve

# Instance 2 (port 11435)
OLLAMA_HOST=0.0.0.0:11435 ollama serve
```

## Monitoring and Logging

### Health Checks

```powershell
# Check Ollama health
curl http://localhost:11434/api/version

# Monitor model status
npm run ollama:status
```

### Performance Metrics

The AI Copilot includes built-in monitoring for:
- Response times
- Memory usage
- Model selection patterns
- Error rates

## Support and Resources

### Documentation
- [Ollama Official Docs](https://github.com/ollama/ollama)
- [Model Hub](https://ollama.ai/library)
- [AI Copilot GitHub](https://github.com/your-org/ai-copilot)

### Community
- [Ollama Discord](https://discord.gg/ollama)
- [AI Copilot Issues](https://github.com/your-org/ai-copilot/issues)

### Getting Help

If you encounter issues:
1. Check this documentation
2. Run `npm run ollama:status` for diagnostics
3. Check the [Troubleshooting](#troubleshooting) section
4. Open an issue on GitHub with:
   - System information
   - Error messages
   - Steps to reproduce

---

*Last updated: May 31, 2025*
*AI Copilot v1.0.0 with Enhanced Ollama Integration*
