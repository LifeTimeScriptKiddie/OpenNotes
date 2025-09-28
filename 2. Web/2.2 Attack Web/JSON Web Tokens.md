---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/json-web-tokens/","noteIcon":"","created":"2025-04-15T14:11:19.605-04:00"}
---
















# 1. What is JWT?
[JSON web token (JWT), pronounced "jot", is an open standard ([RFC 7519](https://tools.ietf.org/html/rfc7519)) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. Again, JWT is a standard, meaning that all JWTs are tokens, but not all tokens are JWTs.](https://auth0.com/docs/secure/tokens/json-web-tokens

https://www.mohitkhare.com/blog/json-web-token/


## 1.1 JWT Structure

Header.Payload.Signature


MohitKhare did a great job illustrating and explaining a JWT structure. 
![](https://i.imgur.com/7n3ZwuX.png)


## 1.2 JWT Stucture example with jwt.io
[jwt.io](https://jwt.io/) does a great job of decoding. 
I want to emphasize a little concern before we drop a jwt to this website or any online tools. 
> **Warning:** JWTs are credentials, which can grant access to resources. Be careful where you paste them! We do not record tokens, all validation and debugging is done on the client side.

At the end of the day, this website is still out in the internet and we don't know what is behind this interface.  I recommend using off-line resource to decode official JWT. 


The

![](https://i.imgur.com/3jfKZfm.png)


## 1.3 JWT - What if it is stolen?

https://stackoverflow.com/questions/34259248/what-if-jwt-is-stolen