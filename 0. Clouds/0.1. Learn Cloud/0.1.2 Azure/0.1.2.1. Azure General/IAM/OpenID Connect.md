---
{"dg-publish":true,"permalink":"/0-learn-like-a-systems-engineer/clouds/azure/azure-general/iam/open-id-connect/","noteIcon":"","created":"2025-04-15T14:11:19.584-04:00"}
---






# 1 OpenID Connect

https://learn.microsoft.com/en-us/entra/identity-platform/v2-protocols-oidc

>OpenID Connect (OIDC) extends the OAuth 2.0 authorization protocol for use as another authentication protocol. You can use OIDC to enable single sign-on (SSO) between your OAuth-enabled applications by using a security token called an ID token.


https://swagger.io/docs/specification/authentication/openid-connect-discovery/#:~:text=https%3A%2F%2Fserver.com%2F,request%20to%20the%20OpenID%20server.\
>This URL returns a JSON listing of the OpenID/OAuth endpoints, supported scopes and claims, public keys used to sign the tokens, and other details. The clients can use this information to construct a request to the OpenID server


## 1.1 Well-known configuration document path
```
Well-known configuration document path: /.well-known/openid-configuration
Authority URL: https://login.microsoftonline.com/{tenant}/v2.0
```
>Every app registration in Microsoft Entra ID is provided a publicly accessible endpoint that serves its OpenID configuration document. To determine the URI of the configuration document's endpoint for your app, append the well-known OpenID configuration path to your app registration's authority URL.



