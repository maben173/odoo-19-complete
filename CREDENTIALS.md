# 📋 QUICK ACCESS GUIDE - All Credentials & URLs

## 🔐 MASTER CREDENTIALS

### Odoo Admin
```
URL: http://localhost:8069 (Local) or https://your-domain.com (Production)
Email: admin@example.com
Password: admin123456  ⚠️ CHANGE ON FIRST LOGIN!
```

### Database - PostgreSQL
```
Host: localhost (Local) or DB_HOST (Production)
Port: 5432
Database: odoo
Username: odoo
Password: odoo_secure_pass_2026
```

### Cache - Redis
```
Host: localhost (Local) or REDIS_HOST (Production)
Port: 6379
Password: redis_secure_2026
```

---

## 🌐 GITHUB REPOSITORIES

### Main Repository (Complete Stack)
```
https://github.com/maben173/odoo-19-complete
Description: Full Odoo 19 with GitHub OAuth, Webhooks, Docker
```

### Related Repositories
```
https://github.com/maben173/odoo-19                    (Base Odoo)
https://github.com/maben173/odoo-19-modules            (Custom Modules)
https://github.com/maben173/odoo-19-api-backend        (REST API)
https://github.com/maben173/odoo-19-frontend           (React Dashboard)
https://github.com/maben173/odoo-19-infrastructure     (DevOps)
```

---

## 🚀 DEPLOYMENT OPTIONS

### Local Development
```bash
cd odoo-19-complete
docker-compose up -d
http://localhost:8069
```

### Railway (Recommended)
```
Deploy: https://railway.app
Connect: GitHub Account
Repo: maben173/odoo-19-complete
URL: https://your-app.railway.app
```

### Render
```
Deploy: https://render.com
Connect: GitHub Account  
Repo: maben173/odoo-19-complete
URL: https://your-app.onrender.com
```

### Heroku
```
Deploy: https://www.heroku.com
Connect: GitHub Account
Repo: maben173/odoo-19-complete
URL: https://your-app.herokuapp.com
```

---

## 🔑 GITHUB OAUTH SETUP

### Create GitHub App
```
https://github.com/settings/apps/new

App Name: Odoo 19 Complete
Homepage: https://github.com/maben173/odoo-19-complete
Callback URL: https://your-domain.com/auth/github/callback
Webhook URL: https://your-domain.com/webhook/github
```

### Get Credentials
```
Client ID: Copy from GitHub App page
Client Secret: Generate & copy (show once only!)
```

### Configure in Odoo
```
Settings > Administration > GitHub Auth
Add Provider:
  Name: GitHub
  Client ID: Iv1.xxxxx
  Client Secret: ghp_xxxxx
  Active: ✓
```

---

## 📊 SERVICE URLS

### Local (Docker)
```
Odoo:       http://localhost:8069
PostgreSQL: localhost:5432
Redis:      localhost:6379
Nginx:      http://localhost:80
API:        http://localhost:8069/api
```

### Production (Railway)
```
Odoo:       https://your-app.railway.app
PostgreSQL: Managed by Railway
Redis:      Managed by Railway
API:        https://your-app.railway.app/api
```

---

## 🔐 ENVIRONMENT VARIABLES

```bash
# Database
DB_NAME=odoo
DB_USER=odoo
DB_PASSWORD=odoo_secure_pass_2026
DB_PORT=5432

# Admin
ADMIN_PASSWD=admin123456

# Redis
REDIS_PASSWORD=redis_secure_2026

# GitHub
GITHUB_CLIENT_ID=Iv1.xxxxx
GITHUB_CLIENT_SECRET=ghp_xxxxx

# Server
WORKERS=4
LOG_LEVEL=info
DOMAIN=your-domain.com
HTTPS=true
```

---

## 📁 FILE LOCATIONS

```
odoo-19-complete/
├── .env.example              (Copy to .env, update values)
├── docker-compose.yml        (Complete stack config)
├── Dockerfile                (Odoo image)
├── requirements.txt          (Python packages)
├── config/
│   ├── odoo.conf            (Odoo server config)
│   ├── nginx.conf           (Reverse proxy config)
│   └── ssl/                 (SSL certificates)
├── addons/
│   └── odoo_github_auth/    (GitHub OAuth module)
├── scripts/
│   ├── start.sh             (Quick start)
│   ├── deploy.sh            (Deployment)
│   └── backup.sh            (Database backup)
├── docs/
│   ├── GITHUB_OAUTH.md      (OAuth setup guide)
│   ├── HOSTING_GITHUB_ONLINE.md (Hosting guide)
│   └── README.md            (Full documentation)
└── .github/workflows/        (CI/CD pipelines)
    ├── deploy.yml           (Auto-deploy)
    └── security.yml         (Security checks)
```

---

## ⚡ QUICK START COMMANDS

```bash
# Clone
git clone https://github.com/maben173/odoo-19-complete.git
cd odoo-19-complete

# Setup
cp .env.example .env
chmod +x scripts/*.sh

# Start locally
./scripts/start.sh

# View logs
docker-compose logs -f odoo

# Backup database
./scripts/backup.sh

# Deploy (production)
./scripts/deploy.sh
```

---

## 🔒 SECURITY REMINDERS

⚠️ **DO NOT:**
- Commit `.env` file to git
- Share client secrets publicly
- Use default passwords in production
- Enable debug mode in production
- Expose admin password in logs

✅ **DO:**
- Use environment variables for secrets
- Change all default passwords immediately
- Enable HTTPS/SSL in production
- Set up regular backups
- Monitor logs for errors
- Use strong passwords (20+ characters)
- Enable two-factor authentication

---

## 📞 SUPPORT

### Documentation
- Full Guide: `docs/HOSTING_GITHUB_ONLINE.md`
- OAuth Setup: `docs/GITHUB_OAUTH.md`
- API Docs: `docs/API.md`
- README: `README.md`

### Resources
- GitHub Repo: https://github.com/maben173/odoo-19-complete
- GitHub Issues: https://github.com/maben173/odoo-19-complete/issues
- Odoo Docs: https://www.odoo.com/documentation/19.0/
- Railway Docs: https://docs.railway.app/

---

## ✅ DEPLOYMENT CHECKLIST

### Before Going Live
- [ ] Change admin password
- [ ] Configure GitHub OAuth
- [ ] Set up custom domain
- [ ] Generate SSL certificates
- [ ] Configure SMTP/Email
- [ ] Test login and features
- [ ] Set up backups
- [ ] Configure monitoring
- [ ] Document deployment
- [ ] Train users

### Post-Deployment
- [ ] Monitor app logs daily
- [ ] Review database backups
- [ ] Check OAuth functionality
- [ ] Monitor resource usage
- [ ] Update security patches
- [ ] Review user access
- [ ] Perform security audit

---

## 📈 NEXT STEPS

1. Read `README.md` for overview
2. Follow `docs/HOSTING_GITHUB_ONLINE.md` to deploy
3. Complete `docs/GITHUB_OAUTH.md` for OAuth
4. Test OAuth login at `/auth/github/login`
5. Configure webhooks in GitHub App
6. Monitor first deployment in production
7. Celebrate! 🎉

---

**Last Updated**: 2026-09-03
**Repository**: https://github.com/maben173/odoo-19-complete
**Status**: Production Ready ✅
