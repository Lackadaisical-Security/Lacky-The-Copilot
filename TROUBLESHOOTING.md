# Troubleshooting Guide

## 🛠️ Common Issues

### Development Issues

#### Issue: Server not starting
**Diagnosis:**
```bash
# Check if the port is in use
sudo lsof -i :3000

# Check the server logs
tail -n 50 logs/server.log
```

**Solutions:**
1. Kill the process using the port:
```bash
sudo kill -9 <PID>
```

2. Check for syntax errors:
```bash
# For JavaScript/TypeScript
npm run lint

# For Python
flake8 .
```

3. Check CSS specificity

### Production Issues

#### Issue: Application not accessible
**Diagnosis:**
```bash
# Check service status
sudo systemctl status ai-copilot

# Check logs
journalctl -u ai-copilot -n 100

# Test connectivity
curl -I http://localhost:3001/health
```

**Solutions:**
1. Restart services:
```bash
sudo systemctl restart ai-copilot
sudo systemctl restart nginx
sudo systemctl restart postgresql
```

2. Check firewall:
```bash
sudo ufw status
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

## 🛠️ Advanced Troubleshooting

### Debug Tools

#### Backend Debugging
```typescript
// Enable detailed logging
import debug from 'debug';
const log = debug('ai-copilot:server');

// Add to your code
log('Processing request:', { userId, action });
```

#### Frontend Debugging
```javascript
// React DevTools
// Install React Developer Tools extension

// Enable React profiler
import { Profiler } from 'react';

<Profiler id="Chat" onRender={onRenderCallback}>
  <ChatInterface />
</Profiler>
```

#### Database Debugging
```sql
-- Enable query logging
ALTER SYSTEM SET log_statement = 'all';
SELECT pg_reload_conf();

-- View logs
tail -f /var/log/postgresql/postgresql-*.log
```

### Performance Profiling

#### Node.js Profiling
```bash
# CPU profiling
node --cpu-prof server/index.js

# Memory profiling
node --heap-prof server/index.js

# Analyze with Chrome DevTools
chrome://inspect
```

#### Frontend Profiling
```javascript
// Performance API
performance.mark('myFeature-start');
// ... feature code ...
performance.mark('myFeature-end');
performance.measure('myFeature', 'myFeature-start', 'myFeature-end');

const measure = performance.getEntriesByName('myFeature')[0];
console.log(`Feature took ${measure.duration}ms`);
```

## 📋 Diagnostic Scripts

### Health Check Script
Create `scripts/health-check.js`:
```javascript
const checks = {
  database: async () => {
    const { pool } = require('../server/models/database');
    await pool.query('SELECT 1');
    return 'OK';
  },
  
  redis: async () => {
    const redis = require('../server/services/redis');
    await redis.ping();
    return 'OK';
  },
  
  openai: async () => {
    const response = await fetch('https://api.openai.com/v1/models', {
      headers: { 'Authorization': `Bearer ${process.env.OPENAI_API_KEY}` }
    });
    return response.ok ? 'OK' : 'Failed';
  }
};

// Run all checks
Object.entries(checks).forEach(async ([name, check]) => {
  try {
    const status = await check();
    console.log(`✓ ${name}: ${status}`);
  } catch (error) {
    console.log(`✗ ${name}: Error - ${error.message}`);
  }
});
```

## 🔍 Log Analysis

### Common Log Patterns

#### Error Patterns
```bash
# Find all errors
grep -i error /var/log/ai-copilot/*.log

# Find specific error types
grep "ECONNREFUSED" /var/log/ai-copilot/*.log
grep "Rate limit" /var/log/ai-copilot/*.log

# Count errors by type
awk '/ERROR/ {print $5}' app.log | sort | uniq -c | sort -nr
```

#### Performance Analysis
```bash
# Response time analysis
awk '/Request completed/ {print $NF}' access.log | \
  awk '{sum+=$1; count++} END {print "Avg:", sum/count "ms"}'

# Slow queries
grep "Slow query" postgresql.log | tail -20
```

## 💊 Quick Fixes

### Reset Everything
```bash
# Complete reset (CAUTION: Deletes all data)
npm run reset:all

# Individual resets
npm run reset:database
npm run reset:cache
npm run reset:sessions
```

### Emergency Recovery
```bash
# Backup current state
npm run backup:emergency

# Restore from backup
npm run restore:latest

# Rollback deployment
npm run deploy:rollback
```

## 📞 Getting Help

### Information to Provide

When reporting issues, include:

1. **Environment Details**
```bash
npm run diagnostic-info
```

2. **Error Messages**
- Full error stack trace
- Browser console errors
- Network tab HAR file

3. **Steps to Reproduce**
- Exact sequence of actions
- User role and permissions
- Time of occurrence

4. **Logs**
```bash
# Collect logs
npm run collect-logs
# Creates: logs-{timestamp}.tar.gz
```

### Support Channels

1. **Community Support**
   - Discord: discord.gg/ai-copilot
   - Forum: forum.lackadaisicalsecurity.com

2. **Professional Support**
   - Email: support@lackadaisicalsecurity.com
   - Phone: +1-XXX-XXX-XXXX (Business hours)

3. **Emergency Support** (Premium only)
   - 24/7 Hotline: +1-XXX-XXX-XXXX
   - Priority Email: priority@lackadaisicalsecurity.com

---

**Document Version**: 1.0  
**Last Updated**: December 2024  
**Next Review**: Monthly