# Setup and Deployment Guide

This guide provides detailed instructions for setting up and deploying the AI-Powered Coding Assistant.

## Table of Contents

1. [System Requirements](#system-requirements)
2. [Development Setup](#development-setup)
3. [Production Deployment](#production-deployment)
4. [Docker Deployment](#docker-deployment)
5. [Cloud Deployment](#cloud-deployment)
6. [Configuration](#configuration)
7. [Troubleshooting](#troubleshooting)

## System Requirements

### Minimum Requirements
- **OS**: Ubuntu 20.04+, Windows 10+, or macOS 10.15+
- **Node.js**: 18.0.0 or higher
- **PostgreSQL**: 14.0 or higher
- **RAM**: 4GB minimum, 8GB recommended
- **Storage**: 2GB free space
- **CPU**: 2 cores minimum, 4 cores recommended

### Recommended Requirements
- **OS**: Ubuntu 22.04 LTS
- **Node.js**: 20.x LTS
- **PostgreSQL**: 15.x
- **RAM**: 16GB
- **Storage**: 10GB SSD
- **CPU**: 4+ cores

## Development Setup

### 1. Prerequisites Installation

#### Ubuntu/Debian
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# Install PostgreSQL
sudo apt install postgresql postgresql-contrib -y

# Install build tools
sudo apt install build-essential git -y
```

#### macOS
```bash
# Install Homebrew if not installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Node.js
brew install node@20

# Install PostgreSQL
brew install postgresql@15
brew services start postgresql@15
```

#### Windows
1. Install Node.js from [nodejs.org](https://nodejs.org/)
2. Install PostgreSQL from [postgresql.org](https://www.postgresql.org/download/windows/)
3. Install Git from [git-scm.com](https://git-scm.com/download/win)

### 2. Database Setup

```sql
-- Connect to PostgreSQL
sudo -u postgres psql

-- Create database and user
CREATE DATABASE ai_copilot;
CREATE USER ai_copilot_user WITH ENCRYPTED PASSWORD 'your_secure_password';
GRANT ALL PRIVILEGES ON DATABASE ai_copilot TO ai_copilot_user;

-- Grant schema permissions
\c ai_copilot
GRANT ALL ON SCHEMA public TO ai_copilot_user;
\q
```

### 3. Project Setup

```bash
# Clone repository
git clone <repository-url>
cd ai-copilot

# Install dependencies
npm install

# Create environment file
cp .env.example .env

# Edit .env file with your configuration
nano .env
```

### 4. Environment Configuration

Edit `.env` file:
```env
# Server Configuration
PORT=3001
NODE_ENV=development
FRONTEND_URL=http://localhost:3000

# Database Configuration
DB_HOST=localhost
DB_PORT=5432
DB_USER=ai_copilot_user
DB_PASSWORD=your_secure_password
DB_NAME=ai_copilot

# Authentication
JWT_SECRET=generate_a_secure_random_string_here
ADMIN_PASSWORD=set_initial_admin_password

# OpenAI Configuration (Required)
OPENAI_API_KEY=your_openai_api_key

# Optional API Keys
WEATHER_API_KEY=your_openweather_api_key
NEWS_API_KEY=your_news_api_key

# Security
SESSION_SECRET=another_secure_random_string
CORS_ORIGIN=http://localhost:3000
```

### 5. Initialize Database

```bash
# Run database initialization
npm run db:init

# Verify tables were created
psql -U ai_copilot_user -d ai_copilot -c "\dt"
```

### 6. Start Development Servers

```bash
# Start both frontend and backend
npm run dev:full

# Or start separately
npm run server  # Backend on port 3001
npm run dev     # Frontend on port 3000
```

## Production Deployment

### 1. Build for Production

```bash
# Install production dependencies only
npm ci --production

# Build frontend
npm run build

# Set environment
export NODE_ENV=production
```

### 2. Database Migration

```bash
# Run production migrations
npm run db:migrate:prod

# Verify database
npm run db:verify
```

### 3. Process Management with PM2

```bash
# Install PM2 globally
npm install -g pm2

# Create ecosystem file
cat > ecosystem.config.js << EOL
module.exports = {
  apps: [{
    name: 'ai-copilot',
    script: './dist/server/index.js',
    instances: 'max',
    exec_mode: 'cluster',
    env: {
      NODE_ENV: 'production',
      PORT: 3001
    },
    error_file: './logs/error.log',
    out_file: './logs/out.log',
    log_file: './logs/combined.log',
    time: true
  }]
};
EOL

# Start application
pm2 start ecosystem.config.js

# Save PM2 configuration
pm2 save
pm2 startup
```

### 4. Nginx Configuration

```nginx
# /etc/nginx/sites-available/ai-copilot
server {
    listen 80;
    server_name your-domain.com;

    # Redirect to HTTPS
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name your-domain.com;

    # SSL Configuration
    ssl_certificate /etc/letsencrypt/live/your-domain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/your-domain.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;

    # Frontend
    location / {
        root /var/www/ai-copilot/build;
        try_files $uri $uri/ /index.html;
    }

    # Backend API
    location /api {
        proxy_pass http://localhost:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Socket.IO
    location /socket.io/ {
        proxy_pass http://localhost:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Enable site:
```bash
sudo ln -s /etc/nginx/sites-available/ai-copilot /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

### 5. SSL Setup with Let's Encrypt

```bash
# Install Certbot
sudo apt install certbot python3-certbot-nginx -y

# Obtain certificate
sudo certbot --nginx -d your-domain.com

# Auto-renewal
sudo certbot renew --dry-run
```

## Docker Deployment

### 1. Create Dockerfile

```dockerfile
# Dockerfile
FROM node:20-alpine AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./
RUN npm ci

# Copy source code
COPY . .

# Build application
RUN npm run build

# Production image
FROM node:20-alpine

WORKDIR /app

# Install production dependencies
COPY package*.json ./
RUN npm ci --production

# Copy built application
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/build ./build

# Create non-root user
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nodejs -u 1001
USER nodejs

EXPOSE 3001

CMD ["node", "dist/server/index.js"]
```

### 2. Create docker-compose.yml

```yaml
# docker-compose.yml
version: '3.8'

services:
  postgres:
    image: postgres:15-alpine
    container_name: ai_copilot_db
    environment:
      POSTGRES_DB: ai_copilot
      POSTGRES_USER: ai_copilot_user
      POSTGRES_PASSWORD: ${DB_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    networks:
      - ai_copilot_network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ai_copilot_user"]
      interval: 10s
      timeout: 5s
      retries: 5

  app:
    build: .
    container_name: ai_copilot_app
    depends_on:
      postgres:
        condition: service_healthy
    environment:
      NODE_ENV: production
      DB_HOST: postgres
      DB_PORT: 5432
      DB_USER: ai_copilot_user
      DB_PASSWORD: ${DB_PASSWORD}
      DB_NAME: ai_copilot
      JWT_SECRET: ${JWT_SECRET}
      OPENAI_API_KEY: ${OPENAI_API_KEY}
    ports:
      - "3001:3001"
    networks:
      - ai_copilot_network
    restart: unless-stopped

  nginx:
    image: nginx:alpine
    container_name: ai_copilot_nginx
    depends_on:
      - app
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./build:/usr/share/nginx/html
      - ./ssl:/etc/nginx/ssl
    networks:
      - ai_copilot_network
    restart: unless-stopped

volumes:
  postgres_data:

networks:
  ai_copilot_network:
    driver: bridge
```

### 3. Deploy with Docker

```bash
# Build and start containers
docker-compose up -d

# View logs
docker-compose logs -f

# Stop containers
docker-compose down
```

## Cloud Deployment

### AWS Deployment

#### 1. EC2 Setup
```bash
# Launch EC2 instance (Ubuntu 22.04 LTS)
# Instance type: t3.medium or larger
# Security group: Allow ports 22, 80, 443, 3001

# Connect to instance
ssh -i your-key.pem ubuntu@your-instance-ip

# Run development setup steps
```

#### 2. RDS PostgreSQL
```bash
# Create RDS instance
# Engine: PostgreSQL 15
# Instance class: db.t3.micro or larger
# Update .env with RDS endpoint
```

#### 3. Application Load Balancer
- Create target group for port 3001
- Configure health checks
- Add SSL certificate from ACM

### Google Cloud Platform

#### 1. Compute Engine
```bash
# Create VM instance
gcloud compute instances create ai-copilot \
  --machine-type=e2-medium \
  --image-family=ubuntu-2204-lts \
  --image-project=ubuntu-os-cloud \
  --boot-disk-size=20GB
```

#### 2. Cloud SQL
```bash
# Create PostgreSQL instance
gcloud sql instances create ai-copilot-db \
  --database-version=POSTGRES_15 \
  --tier=db-f1-micro \
  --region=us-central1
```

### Azure Deployment

#### 1. App Service
```bash
# Create App Service plan
az appservice plan create \
  --name ai-copilot-plan \
  --resource-group ai-copilot-rg \
  --sku B2 \
  --is-linux

# Create web app
az webapp create \
  --resource-group ai-copilot-rg \
  --plan ai-copilot-plan \
  --name ai-copilot-app \
  --runtime "NODE|20-lts"
```

#### 2. Azure Database for PostgreSQL
```bash
# Create PostgreSQL server
az postgres server create \
  --resource-group ai-copilot-rg \
  --name ai-copilot-db \
  --admin-user adminuser \
  --admin-password YourPassword \
  --sku-name B_Gen5_1
```

## Configuration

### Security Best Practices

1. **Environment Variables**
   - Never commit `.env` files
   - Use strong, unique passwords
   - Rotate JWT secrets regularly

2. **Database Security**
   - Use connection pooling
   - Enable SSL for connections
   - Regular backups

3. **API Security**
   - Implement rate limiting
   - Use API key rotation
   - Monitor usage patterns

### Performance Optimization

1. **Frontend**
   - Enable CDN for static assets
   - Implement lazy loading
   - Use service workers

2. **Backend**
   - Enable compression
   - Implement caching
   - Use connection pooling

3. **Database**
   - Create proper indexes
   - Regular VACUUM
   - Monitor query performance

## Troubleshooting

### Common Issues

#### Database Connection Failed
```bash
# Check PostgreSQL status
sudo systemctl status postgresql

# Check connection
psql -U ai_copilot_user -d ai_copilot -h localhost

# Check logs
tail -f /var/log/postgresql/postgresql-*.log
```

#### Port Already in Use
```bash
# Find process using port
lsof -i :3001

# Kill process
kill -9 <PID>
```

#### Module Not Found
```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

#### Build Failures
```bash
# Clear build cache
rm -rf dist build .cache

# Rebuild
npm run build
```

### Monitoring

#### Application Logs
```bash
# PM2 logs
pm2 logs ai-copilot

# Docker logs
docker-compose logs -f app

# System logs
journalctl -u ai-copilot -f
```

#### Performance Monitoring
```bash
# PM2 monitoring
pm2 monit

# System resources
htop

# Database performance
pg_top
```

## Maintenance

### Regular Tasks

1. **Daily**
   - Check application logs
   - Monitor API usage
   - Review error rates

2. **Weekly**
   - Update dependencies
   - Database backups
   - Security scans

3. **Monthly**
   - Performance review
   - Cost optimization
   - Feature usage analysis

### Backup Strategy

```bash
# Database backup
pg_dump -U ai_copilot_user ai_copilot > backup_$(date +%Y%m%d).sql

# Application backup
tar -czf ai_copilot_backup_$(date +%Y%m%d).tar.gz --exclude=node_modules .

# Automated backups with cron
0 2 * * * /path/to/backup_script.sh
```

## Support

For deployment support:
- Documentation: See [INSTRUCTIONS.md](./INSTRUCTIONS.md)
- Internal Support: devops@lackadaisicalsecurity.com
- Emergency: +1-XXX-XXX-XXXX

---

**Document Version**: 1.0  
**Last Updated**: December 2024  
**Next Review**: January 2025
