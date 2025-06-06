# API Reference Documentation

Complete API reference for the AI-Powered Coding Assistant.

## 🌐 Base URLs

- **Development**: `http://localhost:3001/api`
- **Production**: `https://api.yourdomain.com/api`

## 🔐 Authentication

### Overview
The API uses JWT (JSON Web Token) authentication. Include the token in the Authorization header:

```http
Authorization: Bearer <your-jwt-token>
```

### Authentication Endpoints

#### Register New User
```http
POST /api/auth/register
Content-Type: application/json

{
  "username": "johndoe",
  "email": "john@example.com",
  "password": "SecurePass123!"
}
```

**Response:**
```json
{
  "message": "Registration successful",
  "user": {
    "id": 1,
    "username": "johndoe",
    "email": "john@example.com",
    "role": "user"
  },
  "tokens": {
    "accessToken": "eyJhbGc...",
    "refreshToken": "eyJhbGc...",
    "expiresIn": 604800000
  }
}
```

#### Login
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "SecurePass123!"
}
```

#### Refresh Token
```http
POST /api/auth/refresh
Content-Type: application/json

{
  "refreshToken": "eyJhbGc..."
}
```

#### Logout
```http
POST /api/auth/logout
Authorization: Bearer <token>
Content-Type: application/json

{
  "refreshToken": "eyJhbGc..."
}
```

## 💬 Chat Endpoints

### Send Message
```http
POST /api/chat/message
Authorization: Bearer <token> (optional)
Content-Type: application/json

{
  "message": "Write a Python function to sort a list",
  "conversationId": "550e8400-e29b-41d4-a716-446655440000",
  "model": "gpt-4",
  "mode": "code",
  "streamResponse": true
}
```

**Response (Streaming):**
```json
{
  "id": "msg_123",
  "conversationId": "550e8400-e29b-41d4-a716-446655440000",
  "content": "Here's a Python function...",
  "model": "gpt-4",
  "timestamp": "2024-01-15T10:30:00Z",
  "streaming": true
}
```

### Get Conversation History
```http
GET /api/chat/conversation/:conversationId
Authorization: Bearer <token>
```

**Response:**
```json
{
  "conversationId": "550e8400-e29b-41d4-a716-446655440000",
  "messages": [
    {
      "id": "msg_123",
      "role": "user",
      "content": "Write a Python function",
      "timestamp": "2024-01-15T10:30:00Z"
    },
    {
      "id": "msg_124",
      "role": "assistant",
      "content": "Here's a Python function...",
      "timestamp": "2024-01-15T10:30:05Z"
    }
  ]
}
```

### Clear Conversation
```http
DELETE /api/chat/conversation/:conversationId
Authorization: Bearer <token>
```

### Analyze Document
```http
POST /api/chat/analyze-document
Authorization: Bearer <token>
Content-Type: multipart/form-data

file: <binary>
prompt: "Summarize this document"
```

## 🔍 External API Integrations

### Weather Information
```http
GET /api/weather/:location
Authorization: Bearer <token> (optional)
```

**Example:**
```http
GET /api/weather/London
```

**Response:**
```json
{
  "location": "London",
  "temperature": 18,
  "unit": "celsius",
  "description": "Partly cloudy",
  "humidity": 65,
  "windSpeed": 12,
  "icon": "02d"
}
```

### News Articles
```http
GET /api/news?category=technology&limit=10
Authorization: Bearer <token> (optional)
```

**Query Parameters:**
- `category` - News category (technology, business, health, etc.)
- `q` - Search query
- `limit` - Number of articles (default: 10)

**Response:**
```json
{
  "articles": [
    {
      "title": "AI Breakthrough Announced",
      "source": "TechCrunch",
      "url": "https://...",
      "publishedAt": "2024-01-15T08:00:00Z",
      "description": "..."
    }
  ],
  "totalResults": 50
}
```

### Wikipedia Search
```http
GET /api/wikipedia/:query
Authorization: Bearer <token> (optional)
```

**Example:**
```http
GET /api/wikipedia/machine%20learning
```

## 📝 Code Analysis Endpoints

### Analyze Code Quality
```http
POST /api/code/analyze
Authorization: Bearer <token>
Content-Type: application/json

{
  "code": "function example() { ... }",
  "language": "javascript",
  "metrics": ["complexity", "maintainability", "security"]
}
```

**Response:**
```json
{
  "analysis": {
    "complexity": {
      "cyclomatic": 5,
      "cognitive": 8,
      "score": "B"
    },
    "maintainability": {
      "index": 75,
      "score": "A"
    },
    "security": {
      "vulnerabilities": [],
      "score": "A"
    },
    "suggestions": [
      {
        "type": "refactoring",
        "message": "Consider extracting method",
        "line": 15
      }
    ]
  }
}
```

### Generate Tests
```http
POST /api/code/generate-tests
Authorization: Bearer <token>
Content-Type: application/json

{
  "code": "function add(a, b) { return a + b; }",
  "language": "javascript",
  "framework": "jest"
}
```

## 📊 Analytics Endpoints

### Get Productivity Metrics
```http
GET /api/productivity/metrics?range=week
Authorization: Bearer <token>
```

**Query Parameters:**
- `range` - Time range (day, week, month)

**Response:**
```json
{
  "codingTime": {
    "today": 240,
    "thisWeek": 1680,
    "thisMonth": 7200
  },
  "linesOfCode": {
    "added": 1250,
    "removed": 380,
    "modified": 650
  },
  "languages": {
    "javascript": 45,
    "python": 30,
    "typescript": 25
  },
  "productivity": {
    "score": 85,
    "trend": "up",
    "suggestions": []
  }
}
```

### Track Activity
```http
POST /api/productivity/track
Authorization: Bearer <token>
Content-Type: application/json

{
  "activity": "coding",
  "duration": 30,
  "language": "javascript"
}
```

## 📁 File Management Endpoints

### Get File Tree
```http
GET /api/files/tree?path=/src
Authorization: Bearer <token>
```

**Response:**
```json
[
  {
    "id": "file_123",
    "name": "components",
    "type": "folder",
    "path": "/src/components",
    "children": [...]
  },
  {
    "id": "file_124",
    "name": "App.tsx",
    "type": "file",
    "path": "/src/App.tsx",
    "size": 2048,
    "extension": "tsx"
  }
]
```

## 👨‍💼 Admin Endpoints

### Get System Statistics
```http
GET /api/admin/stats
Authorization: Bearer <token>
```

**Required Role:** admin

**Response:**
```json
{
  "users": {
    "total": 1250,
    "active": 450,
    "new": 25,
    "premium": 180
  },
  "usage": {
    "totalRequests": 50000,
    "tokensUsed": 2500000,
    "avgResponseTime": 1.2,
    "errorRate": 0.02
  }
}
```

### Manage Users
```http
GET /api/admin/users?page=1&limit=50&search=john
Authorization: Bearer <token>
```

```http
POST /api/admin/users/:userId/activate
Authorization: Bearer <token>
```

```http
POST /api/admin/users/:userId/deactivate
Authorization: Bearer <token>
```

## 🔌 WebSocket Events

### Connection
```javascript
const socket = io('ws://localhost:3001', {
  auth: {
    token: 'your-jwt-token'
  }
});
```

### Events

#### Client to Server
- `chat:message` - Send chat message
- `chat:typing` - Typing indicator
- `code:analyze` - Request code analysis
- `collaboration:join` - Join collaboration session

#### Server to Client
- `chat:response` - Receive chat response
- `chat:streaming` - Streaming response chunk
- `chat:error` - Error message
- `collaboration:update` - Collaboration updates

### Example Usage
```javascript
// Send message
socket.emit('chat:message', {
  message: 'Hello AI',
  conversationId: '123'
});

// Listen for response
socket.on('chat:response', (data) => {
  console.log('AI Response:', data);
});
```

## 📊 Rate Limiting

### Default Limits
- **Anonymous Users**: 20 requests/hour
- **Authenticated Users**: 100 requests/hour
- **Premium Users**: 500 requests/hour
- **Admin Users**: Unlimited

### Rate Limit Headers
```http
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1642089600
```

## 🔍 Error Handling

### Error Response Format
```json
{
  "error": {
    "code": "INVALID_REQUEST",
    "message": "Invalid request parameters",
    "details": {
      "field": "email",
      "reason": "Invalid email format"
    }
  },
  "timestamp": "2024-01-15T10:30:00Z",
  "requestId": "req_abc123"
}
```

### Common Error Codes
- `AUTH_REQUIRED` - Authentication required
- `INVALID_TOKEN` - Invalid or expired token
- `RATE_LIMITED` - Rate limit exceeded
- `INVALID_REQUEST` - Invalid request parameters
- `NOT_FOUND` - Resource not found
- `SERVER_ERROR` - Internal server error

## 🔒 Security Headers

All API responses include security headers:
```http
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block
Strict-Transport-Security: max-age=31536000; includeSubDomains
```

## 📝 Best Practices

1. **Always use HTTPS** in production
2. **Include proper error handling** for all API calls
3. **Implement retry logic** for failed requests
4. **Cache responses** when appropriate
5. **Use WebSocket** for real-time features
6. **Validate input** on client side
7. **Handle rate limits** gracefully

---

**API Version**: 1.0  
**Last Updated**: December 2024  
**Support**: api-support@lackadaisicalsecurity.com
