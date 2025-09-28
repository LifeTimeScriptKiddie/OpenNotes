# WAF
https://www.f5.com/glossary/web-application-firewall-waf

https://securityboulevard.com/2023/05/how-does-a-waf-work/

https://www.cloudflare.com/learning/ddos/glossary/web-application-firewall-waf/


# What is WAF?
It is a security system designed to protect web applications by monitoring, filtering, and analyzing HTTP/HTTPS traffic between a web app and the internet. 

Operates at layer 7 - application layer
## Examples
```javascript
# Detecting WAF in HTTP Request/Response Headers

A Web Application Firewall (WAF) itself is not something you will directly find in an HTTP request header. However, certain HTTP headers may indicate that a WAF is in place, or you might see headers added by the WAF.

## Response Headers
1. **Server Header**: Sometimes the server header may indicate the presence of a WAF.
   - Example: `Server: Cloudflare`
   
2. **X-WAF Header**: Some WAFs add specific headers.
   - Example: `X-WAF: Enabled`
   
3. **X-CDN Headers**: Headers indicating a content delivery network (CDN) often include WAF functionality.
   - Example: `X-CDN: Imperva`
   
4. **Specific WAF Headers**: Certain WAFs add their own headers.
   - Example: `X-Akamai-EdgeConnect`

## Request Headers
While request headers typically don’t indicate a WAF, the behavior of requests might give hints:
- **Modified User-Agent**: If your requests are being blocked or altered, the WAF might modify headers.
- **X-Forwarded-For**: This header might be added by a proxy or WAF to show the original client's IP address.

## Examples of WAF Indications in Headers
Here are a few examples of response headers that could suggest the presence of a WAF:

- Cloudflare WAF:
  Server: cloudflare
  CF-RAY: 6d5f1b2a9f0d0efb-LHR

- AWS WAF:
Via: 1.1 9e82d1b832e1e2a5bf00a2e4.cloudfront.net (CloudFront)
X-Amz-Cf-Id: xxxxx


-Imperva WAF:
X-CDN: Imperva
X-Iinfo: 10-678910-678910 PNNN RT(1605678910670 0) q(0 0 0 -1) r(1 1) B10(4,289,0) U5


```


## Virtual Patch
In technical terms, a virtual patch is a security rule set up in a Web Application Firewall (WAF) that blocks malicious traffic exploiting a known vulnerability, without changing the underlying software code. It buys you time to apply a permanent fix or update to the software.

https://cheatsheetseries.owasp.org/cheatsheets/Virtual_Patching_Cheat_Sheet.html