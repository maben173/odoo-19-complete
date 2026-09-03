# GitHub OAuth Configuration Guide

## 🔐 GitHub App Setup for Odoo 19

This guide shows you how to create and configure a GitHub OAuth application for Odoo 19 authentication.

---

## 📋 Step 1: Create GitHub App

### Go to GitHub App Creation
👉 **URL**: https://github.com/settings/apps/new

---

## ✅ Step 2: Fill in GitHub App Form

### Required Fields:

#### **App Information**

```
Application name: Odoo 19 Complete
Homepage URL: https://github.com/maben173/odoo-19-complete
Application description: Complete Odoo 19 Stack with GitHub OAuth Integration
```

#### **Authorization Callback URL**

```
Authorization callback URL: http://localhost:8069/auth/github/callback
```

**For Production:**
```
Authorization callback URL: https://your-domain.com/auth/github/callback
```

#### **Setup URL** (Optional)

```
Setup URL: https://github.com/maben173/odoo-19-complete/blob/main/docs/GITHUB_OAUTH.md
```

#### **Webhook**

```
Webhook URL: http://localhost:8069/webhook/github
Webhook Active: ✓ Checked
```

**For Production:**
```
Webhook URL: https://your-domain.com/webhook/github
Webhook Active: ✓ Checked
```

---

## 🔑 Step 3: Permissions (Required)

### User Permissions

- ✅ **Email addresses**: `read`
- ✅ **Profile**: `read`

### Repository Permissions

- ✅ **Contents**: `read`
- ✅ **Issues**: `read`
- ✅ **Pull requests**: `read`
- ✅ **Commits**: `read`

### Organization Permissions

- ✅ **Members**: `read`

---

## 🎯 Step 4: Webhook Events

Select these events to subscribe to:

- ✅ **Push**
- ✅ **Pull request**
- ✅ **Issues**
- ✅ **Issue comment**
- ✅ **Release**
- ✅ **Repository**
- ✅ **Installation**
- ✅ **Installation repositories**

---

## 🆔 Step 5: Get Credentials

After creating the app:

### Copy These Values

1. **Client ID**
   - Location: App page > About section
   - Format: `Iv1.xxxxx`

2. **Client Secret**
   - Click: "Generate a new client secret"
   - Copy immediately (only shown once!)
   - Format: `ghp_xxxxx` or `ghu_xxxxx`

3. **App ID**
   - Location: App page > About section
   - Format: `12345`

4. **Private Key** (Optional, for app authentication)
   - Click: "Generate a private key"
   - Save the `.pem` file securely

---

## 📝 Step 6: Configure in Odoo

### Access Odoo GitHub OAuth Settings

```
http://localhost:8069/web/login
```

1. Login with admin credentials:
   ```
   Email: admin@example.com
   Password: admin123456
   ```

2. Go to Menu: **Settings > Administration > GitHub Auth**

3. Click **GitHub OAuth Providers** > **New**

4. Fill in the form:
   ```
   Name: GitHub
   Client ID: Iv1.xxxxx (from GitHub App)
   Client Secret: ghp_xxxxx (from GitHub App)
   Active: ✓ Checked
   ```

5. Click **Save**

---

## 🧪 Step 7: Test OAuth Flow

### Test Login

1. Open: http://localhost:8069/auth/github/login
2. Click "Authorize with GitHub"
3. You'll be redirected to GitHub authorization page
4. Click "Authorize maben173"
5. You'll be redirected back to Odoo
6. You should be logged in automatically

---

## 🪝 Step 8: Test Webhooks

### View Webhook Deliveries

1. GitHub App page > **Webhooks**
2. Click on your webhook URL
3. Check **Recent Deliveries** tab
4. Each event should show a successful `200 OK` response

### Check Odoo Webhooks Log

```bash
Odoo Menu: GitHub Auth > GitHub Webhooks
```

You should see incoming webhook events:
- Event Type: `push`, `pull_request`, `issues`, etc.
- Status: `pending`, `success`, `error`
- Timestamp: When received

---

## 📱 GitHub App Permissions Summary

| Permission | Purpose |
|-----------|----------|
| User Email | Get user email from GitHub profile |
| User Profile | Get user info (name, avatar, bio, etc.) |
| Repository Contents | Access code in webhooks |
| Issues | Process issue webhooks |
| Pull Requests | Process PR webhooks |
| Commits | Get commit info |

---

## 🔒 Security Best Practices

### 1. Protect Secrets

```bash
# Store in environment variables, NOT in code
export GITHUB_CLIENT_ID="Iv1.xxxxx"
export GITHUB_CLIENT_SECRET="ghp_xxxxx"
```

### 2. Use HTTPS in Production

```
Authorization callback URL: https://your-domain.com/auth/github/callback
Webhook URL: https://your-domain.com/webhook/github
```

### 3. Verify Webhook Signatures

The module automatically verifies:
- Header: `X-Hub-Signature-256`
- Algorithm: HMAC SHA-256

### 4. Rotate Secrets Regularly

```bash
# In GitHub App > Client secrets
# Click "Rotate" to generate new secret
# Update in Odoo after rotation
```

### 5. Monitor Webhook Failures

```bash
Odoo > GitHub Auth > GitHub Webhooks
# Filter by Status: Error
# Check error_message field
```

---

## 🚀 Production Deployment

### Update OAuth URLs for Production

1. GitHub App Settings
2. Update URLs:
   ```
   Homepage URL: https://your-domain.com
   Authorization callback URL: https://your-domain.com/auth/github/callback
   Webhook URL: https://your-domain.com/webhook/github
   ```

3. Generate new Client Secret
4. Update Odoo configuration
5. Redeploy with new credentials

### Environment Variables

```bash
# .env file
GITHUB_CLIENT_ID=Iv1.xxxxx
GITHUB_CLIENT_SECRET=ghp_xxxxx
GITHUB_WEBHOOK_SECRET=whsec_xxxxx
DOMAIN=your-domain.com
HTTPS=true
```

---

## 📊 OAuth Flow Diagram

```
┌─────────────┐         ┌──────────────┐         ┌──────────┐
│   Odoo      │         │   GitHub     │         │  User    │
│             │         │              │         │  Browser │
└──────┬──────┘         └──────┬───────┘         └────┬─────┘
       │                       │                      │
       │  Redirect to GitHub   │                      │
       │<──────────────────────│←─────────────────────┤
       │                       │                      │
       │                       │  User Authorizes     │
       │                       │←─────────────────────┤
       │                       │                      │
       │  Redirect to Odoo     │                      │
       │                       │────────────────────→ │
       │                       │                      │
       │  Exchange Code        │                      │
       ├──────────────────────→│                      │
       │                       │                      │
       │  Access Token         │                      │
       │←──────────────────────┤                      │
       │                       │                      │
       │  Get User Info        │                      │
       ├──────────────────────→│                      │
       │                       │                      │
       │  User Data            │                      │
       │←──────────────────────┤                      │
       │                       │                      │
       │  Create Session       │                      │
       ├───────────────────────────────────────────→ │
       │                       │                      │
       │  Logged In            │                      │
       │←───────────────────────────────────────────┤
```

---

## 🆘 Troubleshooting

### Issue: "Invalid client ID"

```
Solution:
1. Verify Client ID in GitHub App settings
2. Make sure it's copied correctly (no spaces)
3. Check it matches in Odoo configuration
```

### Issue: "Redirect URI mismatch"

```
Solution:
1. GitHub expects exact match:
   http://localhost:8069/auth/github/callback
2. Check for trailing slashes
3. Protocol must match (http vs https)
```

### Issue: "Webhook not working"

```
Solution:
1. Verify webhook URL is accessible
2. Check Odoo firewall/proxy settings
3. View webhook deliveries in GitHub App
4. Check Odoo logs: docker-compose logs odoo
```

### Issue: "User email not found"

```
Solution:
1. Make sure "Email addresses" permission is set to "read"
2. User must have public email on GitHub profile
3. Check Odoo logs for permission errors
```

---

## 📚 Related Documentation

- [GitHub OAuth Documentation](https://docs.github.com/en/apps/oauth-apps)
- [GitHub App Documentation](https://docs.github.com/en/apps/creating-github-apps)
- [Odoo Documentation](https://www.odoo.com/documentation/19.0/)
- [OAuth 2.0 RFC 6749](https://tools.ietf.org/html/rfc6749)

---

## ✨ Features Enabled

After configuring GitHub OAuth, you get:

✅ **Single Sign-On (SSO)**
- Users can login with GitHub account
- Automatic user creation on first login

✅ **Profile Synchronization**
- GitHub username → Odoo login
- GitHub email → Odoo email
- GitHub avatar → Odoo profile pic
- GitHub bio → Odoo bio

✅ **Webhook Integration**
- Push events logged
- PR events tracked
- Issue events monitored
- Release events captured

✅ **Repository Linking**
- Link Odoo projects to GitHub repos
- Sync issue/PR data
- Track commits

---

## 🎓 Next Steps

1. ✅ Create GitHub App (Done!)
2. ✅ Configure in Odoo (Above)
3. 🔄 Test OAuth Login
4. 🔄 Test Webhook Delivery
5. 🔄 Configure GitHub Integrations
6. 🔄 Set up issue/PR tracking
7. 🔄 Deploy to production

---

**Last Updated**: 2026-09-03  
**Version**: 1.0.0  
**GitHub App**: https://github.com/settings/apps/new
