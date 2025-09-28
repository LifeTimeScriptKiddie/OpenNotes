---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/ssrf/ssrf-basic/","noteIcon":"","created":"2025-04-15T14:11:19.608-04:00"}
---
















Server-Side Request Forgery (SSRF) occurs when an attacker can force an application or server to request data or a resource. Since the request is originating at the server, it might be able to access data that the attacker cannot access directly.

![](../../../../unpublished/OSWE/OSWE_round1/10.%20APIGATEWAY-SSRF/SSRF.canvas)

![](https://i.imgur.com/mL0wQhM.png)

![](https://i.imgur.com/1Se9Nan.png)

```
curl -i -X POST -H "Content-Type: application/json" -d '{"url":"http://localhost:8055/"}' http://apigateway:8000/files/import

```

Subnet scanning with SSRF. --> Check for network gateways. 

| IP Address Range              | Subnet Mask | CIDR Notation  | Possible Gateway IP Address |
| ----------------------------- | ----------- | -------------- | --------------------------- |
| 10.0.0.0 - 10.255.255.255     | 255.0.0.0   | 10.0.0.0/8     | 10.0.0.1                    |
| 172.16.0.0 - 172.31.255.255   | 255.240.0.0 | 172.16.0.0/12  | 172.16.0.1                  |
| 192.168.0.0 - 192.168.255.255 | 255.255.0.0 | 192.168.0.0/16 | 192.168.0.1                 |


The backend URL and frontend URL, which is exposed by the API gateway, could be different. 
![](https://i.imgur.com/NfJl494.png)

Blind SSRF --> Check response, timing, etc
