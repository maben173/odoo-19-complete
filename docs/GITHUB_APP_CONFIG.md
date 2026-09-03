# GitHub App Configuration Template

## 🔗 Direct Links

- **Create New App**: https://github.com/settings/apps/new
- **Manage Apps**: https://github.com/settings/apps
- **OAuth Apps**: https://github.com/settings/developers

---

## 📋 Configuration Form

### Copy-Paste Values

#### Basic Information

```
Application name:
Odoo 19 Complete

Homepage URL:
https://github.com/maben173/odoo-19-complete

Application description (optional):
Complete Odoo 19 Stack with GitHub OAuth Integration, Webhooks, and API

Callback URL (will ask for this next):
http://localhost:8069/auth/github/callback
```

#### Webhook Configuration

```
Webhook URL:
http://localhost:8069/webhook/github

Webhook Active:
☑ Checked

Events to subscribe to:
☑ Push
☑ Pull request  
☑ Issues
☑ Issue comment
☑ Release
☑ Repository
☑ Installation
☑ Installation repositories
```

#### Permissions

```
User permissions:
- Email addresses: Read
- Profile information: Read

Repository permissions:
- Contents: Read
- Issues: Read  
- Pull requests: Read
- Commits: Read

Organization permissions:
- Members: Read
```

---

## 🎯 After App Creation

### Step 1: Copy Client ID

```
1. Go to: https://github.com/settings/apps
2. Click your app: "Odoo 19 Complete"
3. Find: "Client ID" section
4. Copy the Client ID value (Iv1.xxxxx)
```

### Step 2: Generate Client Secret

```
1. Scroll down to: "Client secrets"
2. Click: "Generate a new client secret"
3. Copy the secret (ghp_xxxxx) - ONLY SHOWN ONCE!
4. Paste it somewhere safe
```

### Step 3: Get App ID (Optional)

```
1. Top of app page: "ID: 12345"
2. Save this for reference
```

### Step 4: Generate Private Key (Optional)

```
1. Scroll to: "Private keys"
2. Click: "Generate a private key"
3. Download the .pem file
4. Store securely (never commit to git)
```

---

## 🛠️ Odoo Configuration

### 1. Login to Odoo

```bash
http://localhost:8069
Email: admin@example.com
Password: admin123456
```

### 2. Navigate to GitHub Auth Settings

```
Menu > Settings > Administration > GitHub Auth > GitHub OAuth Providers
```

### 3. Create New Provider

```
Name: GitHub
Client ID: Iv1.xxxxx (from GitHub App)
Client Secret: ghp_xxxxx (from GitHub App)
Authorize URL: https://github.com/login/oauth/authorize
Token URL: https://github.com/login/oauth/access_token
Userinfo URL: https://api.github.com/user
Scope: user:email read:user
Active: ☑ Checked
```

### 4. Save

---

## ✅ Verification Checklist

- [ ] GitHub App Created
- [ ] Client ID Copied
- [ ] Client Secret Generated & Saved
- [ ] Webhook URL Set
- [ ] Webhook Active
- [ ] Permissions Configured
- [ ] Odoo Provider Created
- [ ] Credentials Entered in Odoo
- [ ] Test Login Works
- [ ] Webhooks Delivering

---

## 🔐 Security Reminders

⚠️ **Never commit secrets to git!**

```bash
# Good: Use environment variables
export GITHUB_CLIENT_SECRET="ghp_xxxxx"

# Bad: Do NOT do this
echo "ghp_xxxxx" > client_secret.txt
git add .
```

---

## 📝 Production URLs

Replace `localhost:8069` with your domain:

```
Callback URL: https://your-domain.com/auth/github/callback
Webhook URL: https://your-domain.com/webhook/github
Homepage URL: https://your-domain.com
```

---

**Configuration Complete!** ✨
