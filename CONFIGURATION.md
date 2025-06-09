# Configuration Guide

Comprehensive configuration reference for the AI-Powered Coding Assistant.

## 🔧 Environment Variables

### Core Configuration

```bash
# .env file structure
# Server Configuration
NODE_ENV=production|development|test
PORT=3001
HOST=0.0.0.0

# Frontend URL
FRONTEND_URL=http://localhost:3000

# Database Configuration
DB_HOST=localhost
DB_PORT=5432
DB_USER=ai_copilot_user
DB_PASSWORD=your_secure_password
DB_NAME=ai_copilot
DB_SSL=true
DB_POOL_MIN=2
DB_POOL_MAX=10

# Redis Configuration
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=your_redis_password
REDIS_DB=0

# Authentication
JWT_SECRET=generate_secure_random_string_min_32_chars
JWT_EXPIRES_IN=7d
REFRESH_TOKEN_EXPIRES_IN=30d
SESSION_SECRET=another_secure_random_string
ADMIN_PASSWORD=initial_admin_password

# API Keys
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...
GOOGLE_AI_API_KEY=AIza...
GROQ_API_KEY=gsk_...

# External APIs (Optional)
WEATHER_API_KEY=your_openweather_api_key
NEWS_API_KEY=your_newsapi_key
SEARCH_API_KEY=your_search_api_key

# Security
CORS_ORIGIN=http://localhost:3000,https://yourdomain.com
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
BCRYPT_ROUNDS=12

# Logging
LOG_LEVEL=info|debug|error|warn
LOG_FORMAT=json|simple
LOG_DIR=./logs

# File Storage
UPLOAD_DIR=./uploads
MAX_FILE_SIZE=10485760
ALLOWED_FILE_TYPES=.txt,.md,.pdf,.js,.ts,.py,.java

# Analytics
ENABLE_ANALYTICS=true
ANALYTICS_KEY=your_analytics_key

# Email (Optional)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password
EMAIL_FROM=noreply@yourdomain.com
```

### Environment-Specific Configs

#### Development (.env.development)
```bash
NODE_ENV=development
LOG_LEVEL=debug
CORS_ORIGIN=*
RATE_LIMIT_MAX_REQUESTS=1000
DB_SSL=false
```

#### Production (.env.production)
```bash
NODE_ENV=production
LOG_LEVEL=error
CORS_ORIGIN=https://yourdomain.com
RATE_LIMIT_MAX_REQUESTS=100
DB_SSL=true
ENABLE_MONITORING=true
```

#### Testing (.env.test)
```bash
NODE_ENV=test
DB_NAME=ai_copilot_test
LOG_LEVEL=error
JWT_SECRET=test_secret_key
```

## ⚙️ Application Configuration

### Server Configuration

```typescript
// server/config/index.ts
export const config = {
  server: {
    port: process.env.PORT || 3001,
    host: process.env.HOST || 'localhost',
    bodyLimit: '10mb',
    corsOptions: {
      origin: process.env.CORS_ORIGIN?.split(',') || ['http://localhost:3000'],
      credentials: true,
      optionsSuccessStatus: 200
    }
  },
  
  database: {
    connectionString: process.env.DATABASE_URL || 
      `postgresql://${process.env.DB_USER}:${process.env.DB_PASSWORD}@${process.env.DB_HOST}:${process.env.DB_PORT}/${process.env.DB_NAME}`,
    pool: {
      min: parseInt(process.env.DB_POOL_MIN || '2'),
      max: parseInt(process.env.DB_POOL_MAX || '10'),
      idleTimeoutMillis: 30000,
      connectionTimeoutMillis: 2000,
    },
    ssl: process.env.DB_SSL === 'true' ? { rejectUnauthorized: false } : false
  },
  
  redis: {
    host: process.env.REDIS_HOST || 'localhost',
    port: parseInt(process.env.REDIS_PORT || '6379'),
    password: process.env.REDIS_PASSWORD,
    db: parseInt(process.env.REDIS_DB || '0'),
    retryStrategy: (times: number) => Math.min(times * 50, 2000)
  },
  
  auth: {
    jwtSecret: process.env.JWT_SECRET!,
    jwtExpiresIn: process.env.JWT_EXPIRES_IN || '7d',
    refreshTokenExpiresIn: process.env.REFRESH_TOKEN_EXPIRES_IN || '30d',
    bcryptRounds: parseInt(process.env.BCRYPT_ROUNDS || '12'),
    sessionTimeout: 30 * 60 * 1000, // 30 minutes
  },
  
  ai: {
    openai: {
      apiKey: process.env.OPENAI_API_KEY!,
      organization: process.env.OPENAI_ORG,
      defaultModel: 'gpt-4',
      maxTokens: 4096,
      temperature: 0.7,
      timeout: 30000
    },
    anthropic: {
      apiKey: process.env.ANTHROPIC_API_KEY,
      defaultModel: 'claude-3-opus-20240229',
      maxTokens: 4096
    },
    google: {
      apiKey: process.env.GOOGLE_AI_API_KEY,
      defaultModel: 'gemini-pro'
    }
  },
  
  features: {
    enableChat: true,
    enableCodeAnalysis: true,
    enableVoiceCoding: true,
    enableCollaboration: true,
    enableAnalytics: process.env.ENABLE_ANALYTICS === 'true',
    enableFileUpload: true,
    maxFileSize: parseInt(process.env.MAX_FILE_SIZE || '10485760'),
    allowedFileTypes: process.env.ALLOWED_FILE_TYPES?.split(',') || ['.txt', '.md', '.pdf']
  }
};
```

### Frontend Configuration

```typescript
// src/config/index.ts
export const clientConfig = {
  api: {
    baseURL: process.env.REACT_APP_API_URL || 'http://localhost:3001/api',
    timeout: 30000,
    retryAttempts: 3,
    retryDelay: 1000
  },
  
  websocket: {
    url: process.env.REACT_APP_WS_URL || 'ws://localhost:3001',
    reconnection: true,
    reconnectionAttempts: 5,
    reconnectionDelay: 1000,
    reconnectionDelayMax: 5000,
    timeout: 20000
  },
  
  ui: {
    theme: 'dark',
    primaryColor: '#667eea',
    secondaryColor: '#764ba2',
    fontSize: 14,
    fontFamily: 'Inter, system-ui, sans-serif',
    codeFont: 'Fira Code, Consolas, monospace',
    animations: true,
    soundEffects: false
  },
  
  editor: {
    theme: 'vs-dark',
    fontSize: 14,
    lineNumbers: true,
    minimap: true,
    wordWrap: 'on',
    formatOnSave: true,
    tabSize: 2,
    insertSpaces: true
  },
  
  chat: {
    maxMessageLength: 10000,
    typingIndicatorDelay: 1000,
    messageHistoryLimit: 100,
    autoSaveInterval: 30000,
    streamingEnabled: true
  }
};
```

## 🎛️ Feature Flags

### Configuration File
```json
// config/features.json
{
  "features": {
    "newUI": {
      "enabled": true,
      "rollout": 100,
      "allowList": []
    },
    "advancedCodeAnalysis": {
      "enabled": true,
      "rollout": 50,
      "allowList": ["premium", "admin"]
    },
    "collaboration": {
      "enabled": false,
      "rollout": 0,
      "allowList": ["admin"]
    },
    "aiModelSelection": {
      "enabled": true,
      "models": {
        "gpt-4": { "enabled": true, "roles": ["all"] },
        "claude-3": { "enabled": true, "roles": ["premium", "admin"] },
        "gemini": { "enabled": false, "roles": ["admin"] }
      }
    }
  }
}
```

### Feature Flag Service
```typescript
// server/services/featureFlags.ts
export class FeatureFlags {
  static isEnabled(feature: string, user?: User): boolean {
    const config = features[feature];
    if (!config || !config.enabled) return false;
    
    // Check rollout percentage
    if (config.rollout < 100) {
      const hash = this.hashUserId(user?.id || 'anonymous');
      if (hash % 100 >= config.rollout) return false;
    }
    
    // Check allow list
    if (config.allowList?.length > 0) {
      return config.allowList.includes(user?.role || 'guest');
    }
    
    return true;
  }
}
```

## 🔐 Security Configuration

### HTTPS/TLS Configuration
```nginx
# nginx.conf
server {
    listen 443 ssl http2;
    server_name yourdomain.com;
    
    # SSL Configuration
    ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;
    ssl_session_timeout 1d;
    ssl_session_cache shared:SSL:50m;
    ssl_session_tickets off;
    
    # Modern configuration
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256;
    ssl_prefer_server_ciphers off;
    
    # HSTS
    add_header Strict-Transport-Security "max-age=63072000" always;
}
```

### Content Security Policy
```typescript
// server/middleware/security.ts
export const securityHeaders = {
  'Content-Security-Policy': [
    "default-src 'self'",
    "script-src 'self' 'unsafe-inline' 'unsafe-eval' https://cdn.jsdelivr.net",
    "style-src 'self' 'unsafe-inline' https://fonts.googleapis.com",
    "img-src 'self' data: https: blob:",
    "font-src 'self' https://fonts.gstatic.com",
    "connect-src 'self' wss: https://api.openai.com https://api.anthropic.com",
    "frame-ancestors 'none'",
    "base-uri 'self'",
    "form-action 'self'"
  ].join('; '),
  'X-Frame-Options': 'DENY',
  'X-Content-Type-Options': 'nosniff',
  'X-XSS-Protection': '1; mode=block',
  'Referrer-Policy': 'strict-origin-when-cross-origin',
  'Permissions-Policy': 'camera=(), microphone=(), geolocation=()'
};
```

## 📊 Monitoring Configuration

### Logging Configuration
```typescript
// server/config/winston.ts
import winston from 'winston';

export const logger = winston.createLogger({
  level: process.env.LOG_LEVEL || 'info',
  format: winston.format.combine(
    winston.format.timestamp(),
    winston.format.errors({ stack: true }),
    winston.format.splat(),
    winston.format.json()
  ),
  defaultMeta: { service: 'ai-copilot' },
  transports: [
    new winston.transports.File({ 
      filename: 'logs/error.log', 
      level: 'error',
      maxsize: 5242880, // 5MB
      maxFiles: 5
    }),
    new winston.transports.File({ 
      filename: 'logs/combined.log',
      maxsize: 5242880, // 5MB
      maxFiles: 5
    }),
    new winston.transports.Console({
      format: winston.format.combine(
        winston.format.colorize(),
        winston.format.simple()
      )
    })
  ]
});
```

### Metrics Configuration
```yaml
# prometheus.yml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'ai-copilot'
    static_configs:
      - targets: ['localhost:3001']
    metrics_path: '/metrics'
```

## 🚀 Performance Configuration

### Caching Strategy
```typescript
// server/config/cache.ts
export const cacheConfig = {
  // API Response Cache
  api: {
    ttl: 300, // 5 minutes
    maxSize: 100, // MB
    invalidateOn: ['POST', 'PUT', 'DELETE']
  },
  
  // Static Asset Cache
  static: {
    maxAge: 86400, // 1 day
    immutable: true
  },
  
  // AI Response Cache
  ai: {
    ttl: 3600, // 1 hour
    keyGenerator: (params: any) => {
      return crypto.createHash('md5')
        .update(JSON.stringify(params))
        .digest('hex');
    }
  }
};
```

### Database Optimization
```sql
-- Optimize PostgreSQL configuration
-- postgresql.conf

# Memory
shared_buffers = 256MB
effective_cache_size = 1GB
work_mem = 4MB
maintenance_work_mem = 64MB

# Connections
max_connections = 100
max_prepared_transactions = 0

# Write Performance
wal_buffers = 16MB
checkpoint_segments = 32
checkpoint_completion_target = 0.9

# Query Tuning
random_page_cost = 1.1
effective_io_concurrency = 200
```

## 🔄 Backup Configuration

### Automated Backup
```yaml
# backup-config.yml
backup:
  schedule:
    database: "0 2 * * *"  # 2 AM daily
    files: "0 3 * * 0"     # 3 AM weekly
    
  retention:
    daily: 7
    weekly: 4
    monthly: 6
    
  destinations:
    - type: s3
      bucket: ai-copilot-backups
      region: us-east-1
    - type: local
      path: /backups
      
  encryption:
    enabled: true
    algorithm: AES-256
```

## 📝 Configuration Best Practices

1. **Use Environment Variables**: Never hardcode sensitive data
2. **Validate Configuration**: Check all required vars on startup
3. **Document Changes**: Update this guide when adding new configs
4. **Version Control**: Use `.env.example` for templates
5. **Secure Storage**: Use secret management tools in production
6. **Regular Reviews**: Audit configuration quarterly

---

**Document Version**: 1.0  
**Last Updated**: December 2024  
**Configuration Review**: Quarterly
