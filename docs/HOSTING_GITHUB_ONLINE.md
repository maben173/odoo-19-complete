# 🌐 Odoo 19 Hosted on GitHub - Complete Access Guide

## 📌 GitHub Repository URL

```
https://github.com/maben173/odoo-19-complete
```

---

## 🚀 Deploy Odoo 19 on GitHub Pages + Railway/Render/Heroku

You can host Odoo 19 on various platforms:

### Option 1: **Railway.app** (Recommended)

#### Deploy to Railway

1. Go to: https://railway.app
2. Sign in with GitHub
3. New Project > GitHub Repo > Select `odoo-19-complete`
4. Add services:
   - PostgreSQL (Database)
   - Redis (Cache)
   - Odoo (from Dockerfile)

#### Environment Variables

```
DB_HOST=postgres
DB_USER=odoo
DB_PASSWORD=odoo_secure_2026
DB_NAME=odoo
REDIS_ADDR=redis://redis:6379
ADMIN_PASSWD=admin123456
```

#### Access Production

```
Odoo: https://your-railway-app.railway.app
Database: Managed by Railway
Backups: Automatic
```

---

### Option 2: **Render.com**

#### Deploy to Render

1. Go to: https://render.com
2. Sign in with GitHub
3. New > Web Service
4. Connect GitHub repo
5. Configure:
   - Build Command: `pip install -r requirements.txt`
   - Start Command: `odoo -c /etc/odoo/odoo.conf`

#### Database Setup

1. Create PostgreSQL Database on Render
2. Copy connection details
3. Set environment variables

#### Access Production

```
Odoo: https://your-render-app.onrender.com
```

---

### Option 3: **Heroku** (with GitHub Actions)

#### Setup Heroku

```bash
# Install Heroku CLI
curl https://cli-assets.heroku.com/install.sh | sh

# Login
heroku login

# Create app
heroku apps:create odoo-19-complete

# Add PostgreSQL
heroku addons:create heroku-postgresql:standard-0 -a odoo-19-complete

# Set config variables
heroku config:set ADMIN_PASSWD=admin123456 -a odoo-19-complete
```

#### GitHub Actions Deployment

Create `.github/workflows/heroku.yml`:

```yaml
name: Deploy to Heroku

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: akhileshns/heroku-deploy@v3.12.12
        with:
          heroku_api_key: ${{ secrets.HEROKU_API_KEY }}
          heroku_app_name: odoo-19-complete
          heroku_email: ${{ secrets.HEROKU_EMAIL }}
```

#### Access Production

```
Odoo: https://odoo-19-complete.herokuapp.com
```

---

### Option 4: **Docker Hub + Any VPS**

#### Build Docker Image

```bash
# Login to Docker Hub
docker login

# Build image
docker build -t maben173/odoo-19-complete:latest .

# Push to Docker Hub
docker push maben173/odoo-19-complete:latest
```

#### Pull on VPS

```bash
# SSH to VPS
ssh user@your-vps.com

# Pull image
docker pull maben173/odoo-19-complete:latest

# Run with docker-compose
docker-compose up -d
```

---

## 📊 Recommended Hosting Providers

| Platform | Cost | Database | Redis | SSL | Best For |
|----------|------|----------|-------|-----|----------|
| **Railway** | $5-50/mo | Included | Included | ✅ | Production Apps |
| **Render** | Free-$20/mo | Included | Optional | ✅ | Small/Medium |
| **Heroku** | $7-50/mo | Included | Optional | ✅ | Quick Deploy |
| **DigitalOcean** | $5-40/mo | Manual | Manual | ✅ | Full Control |
| **AWS** | Pay-as-go | RDS | ElastiCache | ✅ | Enterprise |
| **Azure** | Pay-as-go | SQL DB | Cache | ✅ | Enterprise |

---

## 🎯 Step-by-Step: Deploy on Railway (Best Option)

### 1. Prepare Repository

```bash
git clone https://github.com/maben173/odoo-19-complete.git
cd odoo-19-complete
```

### 2. Add railway.json

Create `railway.json`:

```json
{
  "$schema": "https://railway.app/schema.json",
  "build": {
    "builder": "dockerfile"
  },
  "deploy": {
    "startCommand": "odoo -c /etc/odoo/odoo.conf",
    "restartPolicyMaxRetries": 5,
    "restartPolicyWindowSeconds": 60
  }
}
```

### 3. Go to Railway

https://railway.app

### 4. Create New Project

- Click "New Project"
- Select "Deploy from GitHub Repo"
- Connect GitHub account
- Select `maben173/odoo-19-complete`

### 5. Add Database

- Click "+"
- Add PostgreSQL service
- Generate random password
- Add Redis service (Optional)

### 6. Configure Environment

Set variables in Railway:

```
DB_NAME=odoo
DB_USER=postgres
DB_PASSWORD=<Railway generated>
DB_HOST=<Railway PostgreSQL hostname>
DB_PORT=5432
ADMIN_PASSWD=your_secure_password_here
WORKERS=2
LOG_LEVEL=info
```

### 7. Deploy

- Railway auto-deploys from git push
- Monitor logs in real-time
- Get public URL

### 8. Access Odoo

```
https://your-app.railway.app/web/login
```

---

## 🔐 Production Access Credentials

### Odoo Web Interface

```
URL: https://your-app.railway.app (or your domain)
Email: admin@example.com
Password: admin123456  (CHANGE ON FIRST LOGIN!)
```

### PostgreSQL Database

```
Host: your-railway-db-host
Port: 5432
Database: odoo
Username: postgres
Password: (Railway generated)
```

### Redis Cache

```
Host: your-railway-redis-host
Port: 6379
Password: (Railway generated)
```

---

## 🔗 GitHub Integration Setup

### 1. Create GitHub App

https://github.com/settings/apps/new

### 2. Configure OAuth URLs

```
Homepage URL: https://your-app.railway.app
Authorization callback URL: https://your-app.railway.app/auth/github/callback
Webhook URL: https://your-app.railway.app/webhook/github
```

### 3. Save Credentials

```
Client ID: Iv1.xxxxx
Client Secret: ghp_xxxxx
```

### 4. Set in Odoo

```
Settings > Administration > GitHub Auth > GitHub OAuth Providers
Name: GitHub
Client ID: Iv1.xxxxx
Client Secret: ghp_xxxxx
Active: ✓
```

---

## 🌐 Custom Domain Setup

### For Railway

1. Go to Railway Project Settings
2. Add Domain
3. Point DNS:
   ```
   CNAME: your-app.railway.app
   ```
4. SSL auto-generated by Railway

### For Other Providers

1. Update OAuth URLs to use domain
2. Add SSL certificate (automatic with most providers)
3. Update firewall/DNS rules

---

## 📱 GitHub Actions CI/CD

Automatic deployment on push:

```yaml
name: Deploy to Production

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Deploy to Railway
        uses: railwayapp/deploy-action@v1
        with:
          token: ${{ secrets.RAILWAY_TOKEN }}
          service: odoo
          environment: production
```

---

## 🔒 Security Checklist

- [ ] Change admin password immediately
- [ ] Set strong database password
- [ ] Enable HTTPS/SSL (automatic on most platforms)
- [ ] Configure firewall rules
- [ ] Set up database backups
- [ ] Enable audit logging
- [ ] Configure SMTP for emails
- [ ] Set up monitoring & alerts
- [ ] Review GitHub OAuth permissions
- [ ] Enable two-factor authentication

---

## 📊 Monitoring & Logs

### Railway Logs

```bash
# View real-time logs
railway logs

# Specific service
railway logs --service odoo
```

### Database Backups

```bash
# Manual backup
railway run pg_dump -U postgres odoo > backup.sql

# Restore
railway run psql -U postgres odoo < backup.sql
```

---

## 💰 Cost Estimation

### Railway

```
Odoo Container: $5/month (always on)
PostgreSQL (512MB): $15/month
Redis (512MB): $5/month
Bandwidth: Included
Total: ~$25/month
```

### Render

```
Web Service: Free-$7/month
PostgreSQL: $15/month
Total: ~$22/month (free tier available)
```

### Heroku

```
Dyno: $7/month (minimum)
PostgreSQL: $9/month
Total: ~$16/month
```

---

## 🆘 Troubleshooting

### App won't start

```bash
# Check logs
railway logs

# Check config
echo $ADMIN_PASSWD
```

### Database connection error

```bash
# Verify connection string
echo $DATABASE_URL

# Test connection
psql $DATABASE_URL
```

### Webhook not working

1. Verify public URL is accessible
2. Check firewall allows HTTPS
3. Review Odoo logs
4. Test webhook delivery in GitHub

---

## 📚 Documentation

- [Railway Docs](https://docs.railway.app/)
- [Render Docs](https://render.com/docs)
- [Heroku Docs](https://devcenter.heroku.com/)
- [GitHub Actions](https://docs.github.com/en/actions)
- [Odoo Docs](https://www.odoo.com/documentation/19.0/)

---

## ✨ Next Steps

1. ✅ Choose hosting platform
2. ✅ Deploy repository
3. ✅ Configure environment variables
4. ✅ Set up custom domain
5. ✅ Create GitHub App
6. ✅ Configure OAuth in Odoo
7. ✅ Test login flow
8. ✅ Set up monitoring
9. ✅ Configure backups
10. ✅ Go live!

---

## 🎉 You're All Set!

**Repository**: https://github.com/maben173/odoo-19-complete

**Production URL**: https://your-app-name.railway.app

**Admin Panel**: https://your-app-name.railway.app/web/login

---

**Last Updated**: 2026-09-03
**Version**: 1.0.0
**Hosting**: GitHub + Railway/Render/Heroku
