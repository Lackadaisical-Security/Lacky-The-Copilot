# Privacy System Migration Guide

## Overview

This guide helps migrate existing API routes to use the comprehensive privacy protection system implemented in the AI-Copilot project. The privacy system provides enterprise-grade protection for all user data and AI interactions.

## Privacy-Protected Routes

### New Privacy-Enhanced Endpoints

#### Chat Privacy Routes (`/api/chat/privacy/`)
- `POST /api/chat/privacy/secure-message` - Privacy-protected messaging with anonymization
- `POST /api/chat/privacy/secure-stream` - Privacy-protected streaming responses
- `GET /api/chat/privacy/secure-conversation/:id` - Retrieve privacy-protected conversations
- `DELETE /api/chat/privacy/secure-conversation/:id` - Secure conversation deletion
- `POST /api/chat/privacy/secure-analyze-document` - Privacy-protected document analysis
- `GET /api/chat/privacy/privacy-metrics` - Privacy system metrics

#### AI Privacy Routes (`/api/ai/privacy/`)
- `GET /api/ai/privacy/quotas` - Privacy-protected quota information
- `POST /api/ai/privacy/api-keys` - Secure API key storage with encryption
- `POST /api/ai/privacy/generate` - Privacy-protected AI response generation
- `POST /api/ai/privacy/test-model` - Privacy-protected model testing
- `GET /api/ai/privacy/privacy-analytics` - Anonymized usage analytics
- `POST /api/ai/privacy/privacy-preferences` - Manage privacy preferences
- `POST /api/ai/privacy/emergency-delete` - Emergency data deletion

## Privacy Levels

### Standard Privacy
- Basic anonymization
- Standard encryption
- Minimal data retention

### High Privacy (Default)
- Advanced anonymization
- Strong encryption
- Reduced data retention
- Request obfuscation

### Maximum Privacy
- Complete anonymization
- Military-grade encryption
- Minimal data retention
- Full traffic analysis protection

## Migration Strategy

### 1. Route Headers for Legacy Compatibility

Add privacy notice headers to existing routes:

```typescript
// Example: Adding privacy notice to existing chat route
router.post('/message', async (req, res) => {
  // Add privacy notice headers
  res.setHeader('X-Privacy-Notice', 'Consider using /api/chat/privacy/secure-message for enhanced privacy protection');
  res.setHeader('X-Privacy-Alternative', '/api/chat/privacy/secure-message');
  
  // Existing route logic...
});
```

### 2. Client-Side Migration

Update frontend components to use privacy-protected endpoints:

```typescript
// Before (legacy)
const response = await fetch('/api/chat/message', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ message, conversationId })
});

// After (privacy-protected)
const response = await fetch('/api/chat/privacy/secure-message', {
  method: 'POST',
  headers: { 
    'Content-Type': 'application/json',
    'X-Privacy-Level': 'high' // optional: standard, high, maximum
  },
  body: JSON.stringify({ message, conversationId })
});
```

### 3. Gradual Migration Plan

#### Phase 1: Parallel Routes (Current)
- Privacy-protected routes available alongside legacy routes
- Privacy notice headers on legacy routes
- Users can opt-in to privacy-protected endpoints

#### Phase 2: Deprecation Warnings
- Add deprecation warnings to legacy routes
- Encourage migration to privacy-protected routes
- Provide migration tools and documentation

#### Phase 3: Full Migration
- Redirect legacy routes to privacy-protected versions
- Remove legacy route implementations
- Full privacy protection by default

## Privacy Features

### Anonymization
- Personal data detection and removal
- Code identifier replacement
- Metadata stripping
- Sensitive data hashing

### Encryption
- Data in transit encryption
- Data at rest encryption
- Perfect forward secrecy
- Homomorphic encryption support

### Session Management
- Anonymous session creation
- Automatic session rotation
- Fingerprint protection
- Privacy-preserving context handling

### Rate Limiting
- Privacy-aware rate limiting
- Adaptive limits based on privacy level
- Anti-fingerprinting protection

## Configuration

### Environment Variables

```bash
# Privacy system configuration
PRIVACY_ENCRYPTION_KEY=your-encryption-key-here
PRIVACY_STRICT_MODE=true
PRIVACY_DEFAULT_LEVEL=high
PRIVACY_ENABLE_METRICS=true
PRIVACY_MAX_RETENTION_HOURS=24

# Development/testing only
PRIVACY_ENABLE_TEST_ENDPOINTS=false
PRIVACY_ENABLE_DEBUG_LOGGING=false
```

### Privacy Configuration

The privacy system is configured in `server/config/privacy.ts`:

```typescript
// Example privacy configuration
const privacyConfig = {
  general: {
    enableAuditLogging: true,
    enableMetricsCollection: true,
    strictMode: true
  },
  anonymization: {
    defaultLevel: 'high',
    enableAutoAnonymization: true,
    personalDataDetection: true
  },
  encryption: {
    enableMultiLayerEncryption: true,
    enablePerfectForwardSecrecy: true,
    keyRotationInterval: 3600000 // 1 hour
  }
};
```

## Testing Privacy Protection

### Development Endpoints (Non-Production)

```typescript
// Test privacy protection
POST /api/chat/privacy/test-privacy
{
  "testData": "John Smith works at Acme Corp, email: john@acme.com",
  "privacyLevel": "high"
}

// Test privacy system status
GET /api/ai/privacy/privacy-status
```

### Integration Testing

```bash
# Run privacy integration tests
npm run test:privacy

# Test privacy middleware
npm run test:middleware

# Test encryption services
npm run test:encryption
```

## Client Integration Examples

### React Component Migration

```typescript
// Before: Legacy chat component
const sendMessage = async (message: string) => {
  const response = await fetch('/api/chat/message', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ message, conversationId })
  });
  return response.json();
};

// After: Privacy-protected chat component
const sendSecureMessage = async (message: string, privacyLevel = 'high') => {
  const response = await fetch('/api/chat/privacy/secure-message', {
    method: 'POST',
    headers: { 
      'Content-Type': 'application/json',
      'X-Privacy-Level': privacyLevel
    },
    body: JSON.stringify({ message, conversationId })
  });
  
  const data = await response.json();
  
  // Handle privacy metadata
  if (data.privacyMetadata) {
    console.log('Privacy protection applied:', data.privacyMetadata);
  }
  
  return data;
};
```

### Streaming with Privacy Protection

```typescript
const streamSecureResponse = async (message: string) => {
  const response = await fetch('/api/chat/privacy/secure-stream', {
    method: 'POST',
    headers: { 
      'Content-Type': 'application/json',
      'X-Privacy-Level': 'high'
    },
    body: JSON.stringify({ message, conversationId })
  });

  const reader = response.body?.getReader();
  const decoder = new TextDecoder();

  while (true) {
    const { done, value } = await reader!.read();
    if (done) break;

    const chunk = decoder.decode(value);
    const lines = chunk.split('\n');

    for (const line of lines) {
      if (line.startsWith('data: ')) {
        const data = line.slice(6);
        if (data === '[DONE]') return;
        
        try {
          const parsed = JSON.parse(data);
          // Handle privacy-protected streaming data
          if (parsed.type === 'chunk') {
            handleStreamChunk(parsed.content);
          }
        } catch (e) {
          // Handle parsing errors
        }
      }
    }
  }
};
```

## Security Considerations

### Data Protection
- All sensitive data is encrypted at rest and in transit
- Personal information is automatically detected and anonymized
- Code identifiers are replaced with privacy-preserving alternatives

### Access Control
- Anonymous sessions for sensitive operations
- Privacy-aware rate limiting
- Emergency data deletion capabilities

### Compliance
- GDPR compliance through comprehensive data protection
- Right to be forgotten via emergency deletion
- Data minimization and purpose limitation

## Troubleshooting

### Common Issues

1. **Privacy middleware not applying**
   - Check route configuration in `server/config/privacy.ts`
   - Verify middleware is properly initialized in `server/index.ts`

2. **Encryption errors**
   - Ensure `PRIVACY_ENCRYPTION_KEY` environment variable is set
   - Check encryption service initialization

3. **Anonymous session issues**
   - Verify session management is enabled in privacy config
   - Check `X-Privacy-Session` header handling

### Debug Logging

Enable debug logging for privacy system:

```bash
# Set environment variable
PRIVACY_ENABLE_DEBUG_LOGGING=true

# Check logs for privacy operations
npm run dev:full 2>&1 | grep "Privacy"
```

## Best Practices

### For Developers

1. **Always use privacy-protected routes for new features**
2. **Test with different privacy levels (standard/high/maximum)**
3. **Handle privacy metadata in client responses**
4. **Implement proper error handling for privacy failures**

### For Users

1. **Choose appropriate privacy level for your use case**
2. **Use anonymous sessions for sensitive operations**
3. **Regularly review and update privacy preferences**
4. **Use emergency deletion if needed**

## Monitoring and Metrics

### Privacy Metrics

Monitor privacy system performance:

```typescript
GET /api/chat/privacy/privacy-metrics
GET /api/ai/privacy/privacy-analytics
```

### Performance Impact

The privacy system is designed for minimal performance impact:
- Encryption operations: ~1-5ms overhead
- Anonymization: ~2-10ms overhead
- Session management: ~1-3ms overhead

## Future Enhancements

### Planned Features

1. **Advanced Homomorphic Encryption**
   - Computation on encrypted data
   - Zero-knowledge proofs

2. **Federated Learning Support**
   - Privacy-preserving model training
   - Differential privacy mechanisms

3. **Blockchain Integration**
   - Immutable privacy audit trails
   - Decentralized key management

4. **AI-Powered Privacy**
   - Intelligent privacy level recommendations
   - Automated privacy compliance checking

---

For questions or support, please refer to the main documentation or create an issue in the project repository.
