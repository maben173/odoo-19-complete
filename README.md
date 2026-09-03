# Odoo 19 Complete Stack - Production Ready

🚀 **Full-Stack Deployment Guide & Access Credentials**

---

## 📦 Repository Structure

```
odoo-19-complete/
├── docker-compose.yml          # Docker Compose production
├── Dockerfile                  # Odoo image
├── requirements.txt            # Python dependencies
├── .env.example               # Environment variables
├── config/
│   ├── odoo.conf             # Odoo configuration
│   ├── nginx.conf            # Nginx reverse proxy
│   └── ssl/                  # SSL certificates
├── addons/                   # Custom modules
│   └── odoo_github_auth/     # GitHub OAuth module
├── .github/
│   └── workflows/            # CI/CD pipelines
├── scripts/
│   ├── deploy.sh            # Deployment script
│   ├── backup.sh            # Backup script
│   └── init.sql             # Database initialization
└── docs/
    ├── SETUP.md             # Installation guide
    ├── DEPLOYMENT.md        # Deployment guide
    └── API.md               # API documentation
```

---

## 🔐 Access Credentials

### Odoo Admin Access

```
URL: https://github.com/maben173/odoo-19-complete
Email: admin@example.com
Password: admin123456
```

⚠️ **IMPORTANT**: Change the admin password on first login!

```bash
# Change password via Docker
docker-compose exec odoo odoo-bin -d odoo -c /etc/odoo/odoo.conf --change-admin-password
```

---

## 🗃️ Database Access

### PostgreSQL

```
Host: localhost
Port: 5432
Database: odoo
Username: odoo
Password: odoo_secure_pass_2026
```

**Connection String**:
```
psql -h localhost -U odoo -d odoo
```

**Docker Access**:
```bash
docker-compose exec postgres psql -U odoo -d odoo
```

---

## 💾 Redis Cache

```
Host: localhost
Port: 6379
Password: redis_secure_2026
```

**Test Connection**:
```bash
redis-cli -h localhost -p 6379 -a redis_secure_2026 ping
```

**Docker Access**:
```bash
docker-compose exec redis redis-cli -a redis_secure_2026
```

---

## 🔑 GitHub OAuth Configuration

### GitHub App Setup

1. **Create GitHub App**:
   - Go to: https://github.com/settings/apps/new
   - **App name**: `Odoo 19 Auth`
   - **Homepage URL**: `https://github.com/maben173/odoo-19-complete`
   - **Authorization callback URL**: `http://localhost:8069/auth/github/callback`
   - **Webhook URL**: `http://localhost:8069/webhook/github`
   - **Webhook active**: ✓
   - **Permissions**:
     - User: `email`, `profile`
     - Repository: `contents`, `issues`, `pull_requests`

2. **Configure in Odoo**:
   - Go to: **Settings > Administration > GitHub Auth**
   - Add new provider with:
     - **Client ID**: Your GitHub App Client ID
     - **Client Secret**: Your GitHub App Client Secret
     - **Active**: ✓

### OAuth Endpoints

```bash
# Login endpoint
http://localhost:8069/auth/github/login

# Callback endpoint
http://localhost:8069/auth/github/callback

# Webhook endpoint
http://localhost:8069/webhook/github
```

---

## 🚀 Deployment URLs

| Service | URL | Credentials |
|---------|-----|-------------|
| **GitHub Repository** | https://github.com/maben173/odoo-19-complete | - |
| **Odoo Web** | http://localhost:8069 | admin / admin123456 |
| **PostgreSQL** | localhost:5432 | odoo / odoo_secure_pass_2026 |
| **Redis** | localhost:6379 | redis_secure_2026 |
| **Nginx** | http://localhost:80 | - |
| **API** | http://localhost:8069/api | Bearer Token |

---

## 📦 Quick Start

### 1. Clone Repository

```bash
git clone https://github.com/maben173/odoo-19-complete.git
cd odoo-19-complete
```

### 2. Configure Environment

```bash
cp .env.example .env
# Edit .env with your values
nano .env
```

### 3. Make Scripts Executable

```bash
chmod +x scripts/*.sh
```

### 4. Start Services

```bash
# Using quick start script
./scripts/start.sh

# OR manually with docker-compose
docker-compose up -d
```

### 5. Check Status

```bash
docker-compose ps
```

### 6. Access Odoo

```
Open: http://localhost:8069
Login with: admin@example.com / admin123456
```

---

## 🔧 Useful Commands

### View Logs

```bash
# All services
docker-compose logs -f

# Specific service
docker-compose logs -f odoo
docker-compose logs -f postgres
docker-compose logs -f nginx
```

### Database Management

```bash
# Backup database
./scripts/backup.sh

# Restore database
docker-compose exec -T postgres psql -U odoo odoo < backups/odoo_backup_YYYYMMDD_HHMMSS.sql

# Connect to database
docker-compose exec postgres psql -U odoo -d odoo

# Run SQL query
docker-compose exec postgres psql -U odoo -d odoo -c "SELECT version();"
```

### Module Management

```bash
# Install module
docker-compose exec odoo odoo-bin -d odoo -i odoo_github_auth -c /etc/odoo/odoo.conf

# Update module
docker-compose exec odoo odoo-bin -d odoo -u odoo_github_auth -c /etc/odoo/odoo.conf

# List modules
docker-compose exec odoo odoo-bin -d odoo --list-modules
```

### Container Management

```bash
# Restart services
docker-compose restart

# Restart specific service
docker-compose restart odoo

# Stop services
docker-compose down

# Remove all volumes (careful!)
docker-compose down -v

# Rebuild images
docker-compose build --no-cache
```

---

## 🔒 Security Configuration

### Change Admin Password

```bash
# Interactive password change
docker-compose exec odoo odoo-bin -d odoo -c /etc/odoo/odoo.conf --change-admin-password
```

### Update Database Credentials

```bash
# Edit .env
DB_PASSWORD=your_new_secure_password

# Restart PostgreSQL
docker-compose restart postgres
```

### Generate SSL Certificates

```bash
# Create SSL directory
mkdir -p config/ssl

# Generate self-signed certificate
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout config/ssl/key.pem -out config/ssl/cert.pem

# Restart Nginx
docker-compose restart nginx
```

---

## 📊 Monitoring & Health Checks

### Service Health

```bash
# Odoo health check
curl http://localhost:8069/web/health

# PostgreSQL health check
docker-compose exec postgres pg_isready

# Redis health check
docker-compose exec redis redis-cli ping

# Nginx status
curl http://localhost:80/nginx_status
```

### Performance Metrics

```bash
# Docker container stats
docker stats

# System resource usage
docker-compose stats

# Database size
docker-compose exec postgres psql -U odoo -d odoo -c "SELECT pg_size_pretty(pg_database_size('odoo'));"
```

---

## 🐛 Troubleshooting

### Port Already in Use

```bash
# Find process using port
lsof -i :8069

# Kill process
kill -9 <PID>

# Change ports in docker-compose.yml
```

### Database Connection Failed

```bash
# Check PostgreSQL logs
docker-compose logs postgres

# Test connection
docker-compose exec postgres psql -U odoo -d odoo -c "SELECT 1;"

# Restart PostgreSQL
docker-compose restart postgres
```

### Module Installation Failed

```bash
# Fix permissions
docker-compose exec odoo chown -R odoo:odoo /mnt/extra-addons

# View error logs
docker-compose logs odoo | grep ERROR

# Reinstall module
docker-compose exec odoo odoo-bin -d odoo --uninstall-all -i odoo_github_auth
```

### Nginx Not Proxying Requests

```bash
# Check Nginx logs
docker-compose logs nginx

# Test Nginx configuration
docker-compose exec nginx nginx -t

# Restart Nginx
docker-compose restart nginx
```

---

## 📚 Documentation

- [Setup Guide](./docs/SETUP.md)
- [Deployment Guide](./docs/DEPLOYMENT.md)
- [API Documentation](./docs/API.md)
- [GitHub OAuth Setup](./docs/GITHUB_OAUTH.md)
- [Module Development](./addons/odoo_github_auth/README.md)

---

## 🚀 Production Deployment

### Prerequisites

- VPS/Server with 4GB+ RAM
- Docker & Docker Compose installed
- Domain name (for SSL)
- GitHub Account

### Deployment Steps

```bash
# 1. SSH to server
ssh user@your-server.com

# 2. Clone repository
git clone https://github.com/maben173/odoo-19-complete.git /opt/odoo
cd /opt/odoo

# 3. Configure environment
cp .env.example .env
nano .env  # Edit with production values

# 4. Make scripts executable
chmod +x scripts/*.sh

# 5. Generate SSL certificates
./scripts/ssl-generate.sh your-domain.com

# 6. Deploy
./scripts/deploy.sh

# 7. Verify
docker-compose ps
curl https://your-domain.com
```

### Using GitHub Actions

Automated deployment is configured in `.github/workflows/`

**Required GitHub Secrets**:
- `SERVER_HOST` - Your server IP/domain
- `SERVER_USER` - SSH username
- `SERVER_KEY` - SSH private key
- `DOCKER_USERNAME` - Docker Hub username
- `DOCKER_PASSWORD` - Docker Hub password

**Set secrets**:
```bash
git secrets set SERVER_HOST your-server.com
git secrets set SERVER_USER deploy
# ... etc
```

---

## 📞 Support & Contact

- **GitHub Repository**: https://github.com/maben173/odoo-19-complete
- **GitHub Issues**: https://github.com/maben173/odoo-19-complete/issues
- **GitHub Discussions**: https://github.com/maben173/odoo-19-complete/discussions
- **Odoo Documentation**: https://www.odoo.com/documentation/19.0/
- **Docker Documentation**: https://docs.docker.com/

---

## 📄 License

This project is licensed under **LGPL-3**

---

## ✅ Checklist for Production

- [ ] Change admin password
- [ ] Configure GitHub OAuth
- [ ] Set up custom domain
- [ ] Generate SSL certificates
- [ ] Configure email/SMTP
- [ ] Set up database backups
- [ ] Configure monitoring
- [ ] Set up log rotation
- [ ] Configure firewall
- [ ] Enable automatic updates

---

**Last Updated**: 2026-09-03  
**Version**: 1.0.0  
**Maintained By**: maben173
