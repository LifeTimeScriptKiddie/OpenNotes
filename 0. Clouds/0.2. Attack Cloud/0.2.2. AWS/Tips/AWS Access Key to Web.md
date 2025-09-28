---
dg-publish: true
---


##  Manual AWS Console Login (Federation URL)
##  Step-by-Step (Manual URL)

### 1. Set Environment Variables (optional)

```bash
export AWS_ACCESS_KEY_ID="YourAccessKeyId"
export AWS_SECRET_ACCESS_KEY="YourSecretAccessKey"
export AWS_SESSION_TOKEN="YourSessionToken"
export AWS_DEFAULT_REGION="us-east-1"
````

---

### **2. Create a Temporary Credentials Session JSON**


Save this as session.json:

```
{
  "sessionId": "YourAccessKeyId",
  "sessionKey": "YourSecretAccessKey",
  "sessionToken": "YourSessionToken"
}
```

---

### **3. Get a SigninToken from AWS**

```
SESSION=$(jq -c . session.json | python3 -c 'import sys, urllib.parse; print(urllib.parse.quote(sys.stdin.read()))')
curl "https://signin.aws.amazon.com/federation?Action=getSigninToken&Session=${SESSION}"
```

This returns:

```
{"SigninToken":"FQoDY..."}
```

---

### **4. Generate Console Login URL**

  

Plug the token into this URL format:

```
https://signin.aws.amazon.com/federation?Action=login&Issuer=Example&Destination=https%3A%2F%2Fconsole.aws.amazon.com%2F&SigninToken=
```
