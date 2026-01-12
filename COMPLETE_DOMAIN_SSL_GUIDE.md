# Complete Guide: Domain to HTTPS - Step by Step

> **From domain purchase to fully working HTTPS with multiple subdomains**

**Example Domain Used:** `sampurna.com`  
**Your Server IP:** `4.187.152.147`

---

## 📋 Table of Contents

1. [Prerequisites](#prerequisites)
2. [Phase 1: Domain Setup](#phase-1-domain-setup)
3. [Phase 2: DNS Configuration](#phase-2-dns-configuration)
4. [Phase 3: Server Preparation](#phase-3-server-preparation)
5. [Phase 4: Nginx Installation & Configuration](#phase-4-nginx-installation--configuration)
6. [Phase 5: SSL Certificate Setup](#phase-5-ssl-certificate-setup)
7. [Phase 6: Testing & Verification](#phase-6-testing--verification)
8. [Phase 7: Application Configuration](#phase-7-application-configuration)
9. [Troubleshooting](#troubleshooting)

---

## Prerequisites

### What You Need:
- ✅ Azure VM running (4.187.152.147)
- ✅ HR Onboarding app running on ports 8000-8506
- ✅ Domain name (purchase if you don't have one)
- ✅ SSH access to VM
- ✅ Sudo privileges on VM

### Estimated Time:
- With existing domain: **30-45 minutes**
- With new domain: **1-2 hours** (including DNS propagation)

---

## Phase 1: Domain Setup

### Option A: If You Already Have a Domain

✅ Skip to [Phase 2](#phase-2-dns-configuration)

### Option B: Purchase a New Domain

#### Where to Buy:
1. **GoDaddy** (https://www.godaddy.com) - Most popular
2. **Namecheap** (https://www.namecheap.com) - Cheaper
3. **Google Domains** (https://domains.google) - Simple
4. **AWS Route 53** (https://aws.amazon.com/route53) - If using AWS
5. **Cloudflare** (https://www.cloudflare.com) - Good prices + security

#### Steps to Purchase (Example: Namecheap):

1. **Search for domain**
   - Go to namecheap.com
   - Search: `sampurna.com` or `sampurna.in`
   - Check availability

2. **Purchase**
   - Add to cart
   - **Important:** Disable "Auto-Renew" if you want (optional)
   - **Important:** Get "WhoisGuard" (privacy protection) - Usually FREE
   - Complete payment

3. **Verify Email**
   - Check your email
   - Verify domain ownership (required by ICANN)

**Cost:** ₹500-1500/year for `.com`, ₹300-800/year for `.in`

---

## Phase 2: DNS Configuration

### Goal: Point your domain to Azure VM

**DNS Records to Create:**

| Type | Name | Value | TTL | Purpose |
|------|------|-------|-----|---------|
| A | @ | 4.187.152.147 | 3600 | Main domain (sampurna.com) |
| A | www | 4.187.152.147 | 3600 | www subdomain |
| A | hr | 4.187.152.147 | 3600 | HR app subdomain |
| A | api | 4.187.152.147 | 3600 | API subdomain |
| A | * | 4.187.152.147 | 3600 | Wildcard (all subdomains) |

### Step-by-Step (GoDaddy Example):

1. **Login to GoDaddy**
   - Go to https://www.godaddy.com
   - Login with your credentials

2. **Access DNS Management**
   - Click "My Products"
   - Find your domain
   - Click "DNS" or "Manage DNS"

3. **Add A Records**
   
   **Record 1: Root Domain**
   ```
   Type: A
   Name: @
   Value: 4.187.152.147
   TTL: 1 Hour
   ```
   Click "Add Record"

   **Record 2: WWW Subdomain**
   ```
   Type: A
   Name: www
   Value: 4.187.152.147
   TTL: 1 Hour
   ```
   Click "Add Record"

   **Record 3: HR Subdomain**
   ```
   Type: A
   Name: hr
   Value: 4.187.152.147
   TTL: 1 Hour
   ```
   Click "Add Record"

   **Record 4: API Subdomain**
   ```
   Type: A
   Name: api
   Value: 4.187.152.147
   TTL: 1 Hour
   ```
   Click "Add Record"

   **Record 5: Wildcard (Optional but Recommended)**
   ```
   Type: A
   Name: *
   Value: 4.187.152.147
   TTL: 1 Hour
   ```
   Click "Add Record"

4. **Save Changes**
   - Click "Save" or "Save All Records"

### Step-by-Step (Namecheap Example):

1. **Login to Namecheap**
   - Go to https://www.namecheap.com
   - Login

2. **Access DNS**
   - Click "Domain List"
   - Click "Manage" next to your domain
   - Click "Advanced DNS" tab

3. **Add Records**
   - Click "Add New Record"
   - Add the same records as above (A records)
   - Click the green checkmark after each

4. **Save**
   - Changes auto-save

### Wait for DNS Propagation

**Time Required:** 5 minutes to 48 hours (usually 10-30 minutes)

**Check Propagation:**
```bash
# On your local machine
nslookup sampurna.com
nslookup hr.sampurna.com
nslookup api.sampurna.com

# Should return: 4.187.152.147
```

**Online Checker:**
- https://dnschecker.org
- Enter: `hr.sampurna.com`
- Check worldwide propagation

---

## Phase 3: Server Preparation

### Step 1: Connect to Your VM

```bash
ssh Azureuser@4.187.152.147
```

### Step 2: Update System

```bash
sudo apt update
sudo apt upgrade -y
```

### Step 3: Open Required Ports in Azure NSG

**In Azure Portal:**

1. Go to your VM: `AZ-CI-SM-VM-UAT-01`
2. Click "Networking" → "Network settings"
3. Click "Create port rule" → "Inbound port rule"
4. Add these rules:

**Rule 1: HTTP**
```
Source: Any
Source port ranges: *
Destination: Any
Service: HTTP
Destination port ranges: 80
Protocol: TCP
Action: Allow
Priority: 1000
Name: Allow-HTTP
```

**Rule 2: HTTPS**
```
Source: Any
Source port ranges: *
Destination: Any
Service: HTTPS
Destination port ranges: 443
Protocol: TCP
Action: Allow
Priority: 1001
Name: Allow-HTTPS
```

**Or via Azure CLI:**
```bash
# From your local machine
az network nsg rule create \
  --resource-group YOUR-RESOURCE-GROUP \
  --nsg-name YOUR-NSG-NAME \
  --name Allow-HTTP-HTTPS \
  --priority 1000 \
  --destination-port-ranges 80 443 \
  --access Allow \
  --protocol Tcp
```

### Step 4: Check VM Firewall (UFW)

```bash
# Check status
sudo ufw status

# If active, allow ports
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# Verify
sudo ufw status
```

### Step 5: Verify Services are Running

```bash
cd ~/hr_projects/HR_Onboarding
./check_running.sh

# All services should be running on ports 8000-8506
```

---

## Phase 4: Nginx Installation & Configuration

### Step 1: Install Nginx

```bash
sudo apt update
sudo apt install nginx -y
```

### Step 2: Verify Installation

```bash
# Check nginx status
sudo systemctl status nginx

# Should show "active (running)"

# Test default page
curl http://localhost
```

### Step 3: Create Nginx Configuration

**Create config file:**
```bash
sudo nano /etc/nginx/sites-available/hr-onboarding
```

**Paste this configuration** (Replace `sampurna.com` with your domain):

```nginx
# Redirect all HTTP to HTTPS (will be configured by certbot)
server {
    listen 80;
    server_name sampurna.com www.sampurna.com hr.sampurna.com api.sampurna.com 
                form1.sampurna.com form2.sampurna.com form3.sampurna.com form4.sampurna.com;
    
    location / {
        return 301 https://$host$request_uri;
    }
}

# Main HR Application (hr.sampurna.com)
server {
    listen 80;
    server_name hr.sampurna.com;
    
    location / {
        proxy_pass http://127.0.0.1:8501;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_read_timeout 86400;
        proxy_buffering off;
    }
}

# Main API (api.sampurna.com)
server {
    listen 80;
    server_name api.sampurna.com;
    
    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_read_timeout 300;
    }
}

# Server API (api.sampurna.com/server)
server {
    listen 80;
    server_name api.sampurna.com;
    
    location /server {
        proxy_pass http://127.0.0.1:8001;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

# Form 1 (form1.sampurna.com)
server {
    listen 80;
    server_name form1.sampurna.com;
    
    location / {
        proxy_pass http://127.0.0.1:8502;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_read_timeout 86400;
        proxy_buffering off;
    }
}

# Form 2 (form2.sampurna.com)
server {
    listen 80;
    server_name form2.sampurna.com;
    
    location / {
        proxy_pass http://127.0.0.1:8504;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_read_timeout 86400;
        proxy_buffering off;
    }
}

# Form 3 (form3.sampurna.com)
server {
    listen 80;
    server_name form3.sampurna.com;
    
    location / {
        proxy_pass http://127.0.0.1:8505;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_read_timeout 86400;
        proxy_buffering off;
    }
}

# Form 4 (form4.sampurna.com)
server {
    listen 80;
    server_name form4.sampurna.com;
    
    location / {
        proxy_pass http://127.0.0.1:8506;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_read_timeout 86400;
        proxy_buffering off;
    }
}

# Root Domain (sampurna.com) - Redirect to hr subdomain
server {
    listen 80;
    server_name sampurna.com www.sampurna.com;
    return 301 https://hr.sampurna.com$request_uri;
}
```

**Save:** Press `Ctrl+X`, then `Y`, then `Enter`

### Step 4: Enable the Configuration

```bash
# Create symbolic link
sudo ln -s /etc/nginx/sites-available/hr-onboarding /etc/nginx/sites-enabled/

# Remove default site
sudo rm /etc/nginx/sites-enabled/default

# Test configuration
sudo nginx -t

# Should show: "syntax is ok" and "test is successful"
```

### Step 5: Start Nginx

```bash
# Restart nginx
sudo systemctl restart nginx

# Enable to start on boot
sudo systemctl enable nginx

# Check status
sudo systemctl status nginx
```

### Step 6: Test HTTP Access

```bash
# Test from VM
curl http://hr.sampurna.com

# Test from your browser (not HTTPS yet)
http://hr.sampurna.com
```

You should see your application (without HTTPS yet).

---

## Phase 5: SSL Certificate Setup

### Step 1: Install Certbot

```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx -y
```

### Step 2: Verify DNS is Propagated

```bash
# Check each subdomain
nslookup hr.sampurna.com
nslookup api.sampurna.com
nslookup form1.sampurna.com
nslookup form2.sampurna.com
nslookup form3.sampurna.com
nslookup form4.sampurna.com

# All should return: 4.187.152.147
```

**If not propagated yet, WAIT.** Certbot needs DNS to be working.

### Step 3: Get SSL Certificates

**Option A: Get All Certificates at Once (Recommended)**

```bash
sudo certbot --nginx \
  -d hr.sampurna.com \
  -d api.sampurna.com \
  -d form1.sampurna.com \
  -d form2.sampurna.com \
  -d form3.sampurna.com \
  -d form4.sampurna.com \
  --non-interactive \
  --agree-tos \
  --email your.email@sampurna.com \
  --redirect
```

**Option B: Get One by One**

```bash
# HR subdomain
sudo certbot --nginx -d hr.sampurna.com

# API subdomain
sudo certbot --nginx -d api.sampurna.com

# Form subdomains
sudo certbot --nginx -d form1.sampurna.com
sudo certbot --nginx -d form2.sampurna.com
sudo certbot --nginx -d form3.sampurna.com
sudo certbot --nginx -d form4.sampurna.com
```

**Follow prompts:**
1. **Email address:** Enter your email
2. **Agree to Terms:** Yes (Y)
3. **Share email:** No (N) - optional
4. **Redirect HTTP to HTTPS:** Yes (2) - recommended

### Step 4: Verify SSL Installation

```bash
# List all certificates
sudo certbot certificates

# Should show:
# Certificate Name: hr.sampurna.com
# Certificate Name: api.sampurna.com
# etc.
```

### Step 5: Test HTTPS Access

**In browser, visit:**
```
https://hr.sampurna.com/
https://api.sampurna.com/docs
https://form1.sampurna.com/
```

**You should see:**
- ✅ Green padlock
- ✅ "Secure" or "Connection is secure"
- ✅ Valid certificate

### Step 6: Setup Auto-Renewal

Certbot automatically sets up auto-renewal. Verify:

```bash
# Test renewal
sudo certbot renew --dry-run

# Should show: "Congratulations, all simulated renewals succeeded"
```

**Renewal happens automatically via systemd timer:**
```bash
# Check renewal timer
sudo systemctl status certbot.timer

# Should show: "active"
```

---

## Phase 6: Testing & Verification

### Test Checklist:

#### 1. DNS Resolution
```bash
nslookup hr.sampurna.com      # Should return 4.187.152.147
nslookup api.sampurna.com     # Should return 4.187.152.147
nslookup form1.sampurna.com   # Should return 4.187.152.147
```

#### 2. HTTP to HTTPS Redirect
```bash
curl -I http://hr.sampurna.com
# Should show: HTTP/1.1 301 Moved Permanently
# Location: https://hr.sampurna.com/
```

#### 3. SSL Certificate Valid
```bash
# Check certificate
openssl s_client -connect hr.sampurna.com:443 -servername hr.sampurna.com < /dev/null

# Should show certificate details
```

**Online SSL Checker:**
- https://www.ssllabs.com/ssltest/
- Enter: `hr.sampurna.com`
- Should get A or A+ rating

#### 4. Application Accessibility

**Test each URL in browser:**

| URL | Expected Result |
|-----|----------------|
| https://hr.sampurna.com | HR Login Page, Green Lock |
| https://api.sampurna.com/docs | API Documentation, Green Lock |
| https://form1.sampurna.com | Form 1 Page, Green Lock |
| https://form2.sampurna.com | Form 2 Page, Green Lock |
| https://form3.sampurna.com | Form 3 Page, Green Lock |
| https://form4.sampurna.com | Form 4 Page, Green Lock |

#### 5. Backend Services Running

```bash
cd ~/hr_projects/HR_Onboarding
./check_running.sh

# All services should show "Running"
```

#### 6. Nginx Logs (Check for Errors)

```bash
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```

---

## Phase 7: Application Configuration

### Update Application URLs (If Needed)

Some applications may have hardcoded URLs. Update them:

#### 1. Update .env File

```bash
cd ~/hr_projects/HR_Onboarding
nano .env
```

Add/Update:
```
BASE_URL=https://hr.sampurna.com
API_URL=https://api.sampurna.com
FRONTEND_URL=https://hr.sampurna.com
```

#### 2. Update Streamlit Config

```bash
mkdir -p ~/.streamlit
nano ~/.streamlit/config.toml
```

Add:
```toml
[server]
enableCORS = false
enableXsrfProtection = false

[browser]
serverAddress = "hr.sampurna.com"
serverPort = 443
```

#### 3. Restart Services

```bash
sudo systemctl restart hr-api-main hr-api-server hr-login hr-form1 hr-form2 hr-form3 hr-form4
```

---

## 🎯 Final URL Structure

After complete setup:

```
Main Application:
└─ https://hr.sampurna.com/                    [HR Login & Dashboard]

API Endpoints:
├─ https://api.sampurna.com/docs               [API Documentation]
├─ https://api.sampurna.com/items              [API Endpoints]
└─ https://api.sampurna.com/server             [Server API]

Forms:
├─ https://form1.sampurna.com/                 [Mobile Entry Form]
├─ https://form2.sampurna.com/                 [Screening Form]
├─ https://form3.sampurna.com/                 [Interview Form]
└─ https://form4.sampurna.com/                 [Interview Day Form]

Redirects:
├─ http://sampurna.com  → https://hr.sampurna.com/
├─ https://sampurna.com → https://hr.sampurna.com/
└─ http://hr.sampurna.com → https://hr.sampurna.com/
```

---

## 📊 Complete Architecture Diagram

```
┌─────────────────────────────────────────────────────┐
│           INTERNET (Users)                          │
└──────────────────┬──────────────────────────────────┘
                   │
                   │ HTTPS (443)
                   ↓
┌─────────────────────────────────────────────────────┐
│         Azure NSG (Network Security Group)          │
│         Ports: 80, 443 (Open)                       │
└──────────────────┬──────────────────────────────────┘
                   │
                   ↓
┌─────────────────────────────────────────────────────┐
│         NGINX Reverse Proxy                         │
│         - SSL Termination (Let's Encrypt)           │
│         - Domain Routing                            │
└──────────┬──────┬──────┬──────┬──────┬──────┬───────┘
           │      │      │      │      │      │
           ↓      ↓      ↓      ↓      ↓      ↓
        ┌────┐ ┌────┐ ┌────┐ ┌────┐ ┌────┐ ┌────┐
        │8501│ │8000│ │8001│ │8502│ │8504│ │8505│ │8506│
        └────┘ └────┘ └────┘ └────┘ └────┘ └────┘ └────┘
          │      │      │      │      │      │      │
          ↓      ↓      ↓      ↓      ↓      ↓      ↓
    ┌──────────────────────────────────────────────────┐
    │         HR Onboarding Services                    │
    │         (Systemd Managed)                        │
    └──────────────────────────────────────────────────┘
```

---

## Troubleshooting

### Issue 1: DNS Not Resolving

**Symptom:**
```bash
nslookup hr.sampurna.com
# Server can't find hr.sampurna.com: NXDOMAIN
```

**Solution:**
1. Wait longer (up to 48 hours)
2. Check DNS records in domain registrar
3. Use `dig hr.sampurna.com` for more details
4. Try: https://dnschecker.org

### Issue 2: Certbot Fails

**Symptom:**
```
Error: Domain doesn't resolve to this server
```

**Solution:**
```bash
# Verify DNS first
nslookup hr.sampurna.com

# Check nginx is serving the domain
curl -I http://hr.sampurna.com

# Check port 80 is open
sudo netstat -tulpn | grep :80

# Try manual verification
sudo certbot certonly --manual -d hr.sampurna.com
```

### Issue 3: SSL Certificate Validation Failed

**Symptom:** Certbot fails with "too many requests"

**Solution:**
```bash
# Use staging server first (for testing)
sudo certbot --nginx -d hr.sampurna.com --staging

# If successful, then use production
sudo certbot --nginx -d hr.sampurna.com
```

### Issue 4: "502 Bad Gateway"

**Symptom:** Nginx shows 502 error

**Solution:**
```bash
# Check backend services
cd ~/hr_projects/HR_Onboarding
./check_running.sh

# Check nginx error log
sudo tail -f /var/log/nginx/error.log

# Restart services
sudo systemctl restart hr-api-main hr-login
```

### Issue 5: Mixed Content Warning

**Symptom:** HTTPS page with mixed content warning

**Solution:**
1. Update all HTTP URLs to HTTPS in your code
2. Check browser console for specific URLs
3. Update API URLs in frontend code

### Issue 6: Certificate Auto-Renewal Failed

**Symptom:** Certificate expired

**Solution:**
```bash
# Manual renewal
sudo certbot renew

# Force renewal (even if not due)
sudo certbot renew --force-renewal

# Check renewal timer
sudo systemctl status certbot.timer
sudo systemctl restart certbot.timer
```

---

## 🔧 Useful Commands

### Nginx Commands
```bash
# Test configuration
sudo nginx -t

# Reload (no downtime)
sudo systemctl reload nginx

# Restart
sudo systemctl restart nginx

# View logs
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```

### Certbot Commands
```bash
# List certificates
sudo certbot certificates

# Renew all
sudo certbot renew

# Renew specific domain
sudo certbot renew --cert-name hr.sampurna.com

# Delete certificate
sudo certbot delete --cert-name hr.sampurna.com

# Test renewal
sudo certbot renew --dry-run
```

### DNS Commands
```bash
# Check DNS
nslookup hr.sampurna.com
dig hr.sampurna.com
host hr.sampurna.com

# Trace DNS
dig hr.sampurna.com +trace
```

### SSL Commands
```bash
# Check certificate details
openssl s_client -connect hr.sampurna.com:443 -servername hr.sampurna.com

# Check certificate expiry
echo | openssl s_client -servername hr.sampurna.com -connect hr.sampurna.com:443 2>/dev/null | openssl x509 -noout -dates
```

---

## 📝 Maintenance Checklist

### Daily
- [ ] Check application is accessible
- [ ] Monitor error logs

### Weekly
- [ ] Check SSL certificate expiry
- [ ] Review nginx logs for issues
- [ ] Test all subdomains

### Monthly
- [ ] Verify certificate auto-renewal works
- [ ] Update nginx if needed
- [ ] Review and optimize nginx config

### Quarterly
- [ ] Review DNS records
- [ ] Check for security updates
- [ ] Audit SSL configuration

---

## 🎓 Key Takeaways

1. **One domain, unlimited subdomains** - FREE
2. **SSL certificates for each subdomain** - FREE (Let's Encrypt)
3. **Auto-renewal every 90 days** - Automatic
4. **Nginx as reverse proxy** - Powerful & flexible
5. **All traffic encrypted** - Secure

---

## 📞 Support Resources

- **Nginx Docs:** https://nginx.org/en/docs/
- **Let's Encrypt:** https://letsencrypt.org/
- **Certbot:** https://certbot.eff.org/
- **DNS Checker:** https://dnschecker.org/
- **SSL Checker:** https://www.ssllabs.com/ssltest/

---

## 🚀 Next Steps

After completing this setup, you can:

1. **Add more subdomains** - Just add DNS record + certbot
2. **Setup monitoring** - Use tools like Uptime Robot
3. **Add WAF** - Cloudflare for DDoS protection
4. **Setup CDN** - For faster global access
5. **Implement rate limiting** - Nginx rate limiting
6. **Add authentication** - OAuth, JWT tokens
7. **Setup backup domain** - For redundancy

---

**Setup Complete!** 🎉

Your HR Onboarding application is now:
✅ Accessible via clean domain names
✅ Fully HTTPS encrypted
✅ Auto-renewing SSL certificates
✅ Production-ready

---

**Last Updated:** January 2026  
**Version:** 1.0  
**Maintained by:** Sahil
