# Development Guide

Welcome to the Development Guide for the AI-Powered Coding Assistant by Lackadaisical Security. This document provides all the necessary information and guidelines for developers to contribute to the project.

## Table of Contents
- [Getting Started](#getting-started)
- [Code Contribution](#code-contribution)
- [Code Style Guide](#code-style-guide)
- [Testing](#testing)
- [Development Tools](#development-tools)
- [Performance Profiling](#performance-profiling)
- [Building & Deployment](#building--deployment)
- [Continuous Integration](#continuous-integration)
- [Contributing](#contributing)
- [Resources](#resources)

## Getting Started

To get started with development, please follow these steps:

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/ai-copilot.git
   cd ai-copilot
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   - Copy the example environment file
   ```bash
   cp .env.example .env
   ```
   - Update the `.env` file with your configuration

4. **Run the development server**
   ```bash
   npm run dev
   ```

## Code Contribution

We welcome contributions from everyone. Please follow these guidelines when contributing:

1. **Fork the repository** - Create your own copy of the repository by forking it on GitHub.

2. **Create a feature branch** - Create a new branch for your feature or bugfix.
   ```bash
   git checkout -b feature/my-new-feature
   ```

3. **Make your changes** - Implement your feature or bugfix.

4. **Commit your changes** - Write a clear and descriptive commit message.
   ```bash
   git commit -m "Add my new feature"
   ```

5. **Push to your fork** - Push your changes to your GitHub fork.
   ```bash
   git push origin feature/my-new-feature
   ```

6. **Create a pull request** - Go to the original repository and create a pull request from your feature branch.

7. **Pull request process**
   - Create feature branch from `develop`
   - Write code following style guide
   - Add/update tests
   - Update documentation
   - Create PR with description
   - Pass CI/CD checks
   - Get code review approval
   - Merge to `develop`

## Code Style Guide

We follow strict coding standards to maintain code quality and consistency. Please adhere to the following guidelines:

### TypeScript/JavaScript
```typescript
// Use const/let, never var
const MAX_RETRIES = 3;
let currentAttempt = 0;

// Use arrow functions for callbacks
array.map(item => item.id);

// Use async/await over promises
async function fetchData() {
  try {
    const data = await api.get('/endpoint');
    return data;
  } catch (error) {
    logger.error('Failed to fetch data:', error);
    throw error;
  }
}

// Use interfaces for type definitions
interface User {
  id: number;
  name: string;
  email: string;
  role: UserRole;
}

// Use enums for constants
enum UserRole {
  ADMIN = 'admin',
  USER = 'user',
  GUEST = 'guest'
}
```

### React Components
```typescript
// Use functional components with hooks
import React, { useState, useEffect } from 'react';

interface Props {
  title: string;
  onSubmit: (data: FormData) => void;
}

export const MyComponent: React.FC<Props> = ({ title, onSubmit }) => {
  const [loading, setLoading] = useState(false);
  
  useEffect(() => {
    // Effect logic
  }, [dependency]);
  
  return (
    <div className="component-wrapper">
      <h2>{title}</h2>
      {/* Component content */}
    </div>
  );
};
```

### CSS Conventions
```css
/* BEM naming convention */
.component-name { }
.component-name__element { }
.component-name--modifier { }

/* Use CSS variables */
:root {
  --primary-color: #667eea;
  --text-primary: #ffffff;
  --spacing-unit: 8px;
}

/* Mobile-first responsive design */
.container {
  padding: var(--spacing-unit);
}

@media (min-width: 768px) {
  .container {
    padding: calc(var(--spacing-unit) * 2);
  }
}
```

## Testing

We use a variety of tests to ensure the quality and functionality of our code. Please follow these guidelines when writing tests:

### Test Structure
```
tests/
├── unit/
│   ├── components/     # React component tests
│   ├── services/       # Service layer tests
│   └── utils/          # Utility function tests
├── integration/
│   ├── api/           # API endpoint tests
│   └── database/      # Database integration tests
└── e2e/
    ├── auth.spec.ts   # Authentication flows
    ├── chat.spec.ts   # Chat functionality
    └── admin.spec.ts  # Admin features
```

### Writing Tests

#### Unit Tests
```typescript
// Example component test
import { render, screen, fireEvent } from '@testing-library/react';
import { ChatInput } from '../src/components/ChatInput';

describe('ChatInput', () => {
  it('should submit message on Enter key', () => {
    const onSubmit = jest.fn();
    render(<ChatInput onSubmit={onSubmit} />);
    
    const input = screen.getByRole('textbox');
    fireEvent.change(input, { target: { value: 'Test message' } });
    fireEvent.keyPress(input, { key: 'Enter', code: 13 });
    
    expect(onSubmit).toHaveBeenCalledWith('Test message');
  });
});
```

#### Integration Tests
```typescript
// Example API test
import request from 'supertest';
import app from '../server/app';

describe('POST /api/chat/message', () => {
  it('should return AI response', async () => {
    const response = await request(app)
      .post('/api/chat/message')
      .set('Authorization', 'Bearer token')
      .send({ message: 'Hello AI' });
    
    expect(response.status).toBe(200);
    expect(response.body).toHaveProperty('response');
  });
});
```

#### E2E Tests
```typescript
// Example Playwright test
import { test, expect } from '@playwright/test';

test('user can send chat message', async ({ page }) => {
  await page.goto('/');
  await page.fill('[data-testid="chat-input"]', 'Hello AI');
  await page.press('[data-testid="chat-input"]', 'Enter');
  
  await expect(page.locator('[data-testid="ai-response"]')).toBeVisible();
});
```

### Running Tests
```bash
# Run all tests
npm test

# Run specific test suite
npm run test:unit
npm run test:integration
npm run test:e2e

# Watch mode
npm run test:watch

# Coverage report
npm run test:coverage
```

## Development Tools

We recommend using the following tools and extensions to enhance your development experience:

### VS Code Setup

#### Recommended Extensions
```json
// .vscode/extensions.json
{
  "recommendations": [
    "dbaeumer.vscode-eslint",
    "esbenp.prettier-vscode",
    "ms-vscode.vscode-typescript-tslint-plugin",
    "bradlc.vscode-tailwindcss",
    "christian-kohler.path-intellisense",
    "formulahendry.auto-rename-tag",
    "streetsidesoftware.code-spell-checker",
    "wayou.vscode-todo-highlight",
    "gruntfuggly.todo-tree",
    "eamodio.gitlens"
  ]
}
```

#### Workspace Settings
```json
// .vscode/settings.json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "typescript.preferences.importModuleSpecifier": "relative",
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

### Debugging

#### VS Code Debug Configuration
```json
// .vscode/launch.json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Debug Server",
      "program": "${workspaceFolder}/server/index.ts",
      "preLaunchTask": "tsc: build - tsconfig.server.json",
      "outFiles": ["${workspaceFolder}/dist/**/*.js"],
      "envFile": "${workspaceFolder}/.env.development"
    },
    {
      "type": "chrome",
      "request": "launch",
      "name": "Debug Client",
      "url": "http://localhost:3000",
      "webRoot": "${workspaceFolder}/src"
    }
  ]
}
```

## Performance Profiling

We use performance profiling to identify and fix bottlenecks in our application. Please follow these guidelines when profiling performance:

### Backend Profiling
```typescript
// Add performance monitoring
import { performance } from 'perf_hooks';

export function measurePerformance(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;
  
  descriptor.value = async function(...args: any[]) {
    const start = performance.now();
    const result = await originalMethod.apply(this, args);
    const end = performance.now();
    
    logger.debug(`${propertyKey} took ${end - start}ms`);
    return result;
  };
}

// Usage
class Service {
  @measurePerformance
  async processData(data: any) {
    // Method implementation
  }
}
```

## Building & Deployment

We use a variety of tools and scripts to build and deploy our application. Please follow these guidelines when building and deploying:

### Build Process
```bash
# Development build
npm run build:dev

# Production build
npm run build

# Build specific parts
npm run build:client
npm run build:server
```

### Pre-deployment Checklist
- [ ] All tests passing
- [ ] No ESLint errors
- [ ] Dependencies updated
- [ ] Security audit passed
- [ ] Environment variables documented
- [ ] Database migrations ready
- [ ] Performance benchmarks met
- [ ] Documentation updated

### Deployment Scripts
```bash
# scripts/deploy.sh
#!/bin/bash
set -e

echo "🚀 Starting deployment..."

# Run tests
npm test

# Build application
npm run build

# Run database migrations
npm run db:migrate:prod

# Deploy to server
rsync -avz --delete dist/ user@server:/app/

# Restart services
ssh user@server "pm2 restart ai-copilot"

echo "✅ Deployment complete!"
```

## Continuous Integration

We use GitHub Actions for continuous integration. Please follow these guidelines when working with CI:

### GitHub Actions Workflow
```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  test:
    runs-on: ubuntu-latest
    
    services:
      postgres:
        image: postgres:15
        env:
          POSTGRES_PASSWORD: postgres
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '20'
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run linter
        run: npm run lint
      
      - name: Run tests
        run: npm test
        env:
          DATABASE_URL: postgresql://postgres:postgres@localhost/test
      
      - name: Build
        run: npm run build
```

## Contributing

We welcome contributions from everyone. Please follow these guidelines when contributing:

1. **Report Issues**
   - Use issue templates
   - Provide reproduction steps
   - Include environment details

2. **Submit Pull Requests**
   - Fork the repository
   - Create feature branch
   - Follow coding standards
   - Write tests
   - Update documentation

3. **Code Review Process**
   - Automated checks must pass
   - At least one approval required
   - Address all feedback
   - Squash commits before merge

### Development Best Practices

1. **Security First**
   - Never commit secrets
   - Validate all inputs
   - Use parameterized queries
   - Keep dependencies updated

2. **Performance**
   - Profile before optimizing
   - Use caching wisely
   - Optimize database queries
   - Lazy load components

3. **Maintainability**
   - Write self-documenting code
   - Keep functions small
   - Use meaningful names
   - Add helpful comments

4. **Testing**
   - Write tests first (TDD)
   - Aim for 80%+ coverage
   - Test edge cases
   - Mock external services

## Resources

We provide a variety of resources to help developers understand and work with our code. Please refer to the following resources:

### Internal Resources
- [API Documentation](./API.md)
- [Architecture Guide](./ARCHITECTURE.md)
- [Security Guidelines](./SECURITY.md)

### External Resources
- [React Documentation](https://react.dev/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)
- [OWASP Security Guide](https://owasp.org/www-project-web-security-testing-guide/)

---

**Document Version**: 1.0  
**Last Updated**: December 2024  
**Next Review**: February 2025