[Active Directory Federation Service (AD FS) enables Federated Identity and Access Management by securely sharing digital identity and entitlements rights across security and enterprise boundaries.](https://learn.microsoft.com/en-us/windows-server/identity/ad-fs/ad-fs-overview). 

[Jaap Wesselius](https://jaapwesselius.com/2020/01/02/implementing-active-directory-federation-services-step-by-step/) has a great write up regarding how to setup ADFS services. 

>In a federated environment when you try to logon to a cloud service (in Office 365 this can be SharePoint, Teams, Exchange, OneDrive, the Microsoft Portal) an authentication request is presented. Instead of entering a password that can be authenticated by an Azure AD Domain Controller, the request is redirected to an on-premises federation server. This service is called the Security Token Service or STS. The STS in an Active Directory environment is implemented by means of an ADFS instance running on a Windows 2022 server in the DMZ. This is the Web Application Proxy or WAP server. Common names for this server are sts.contoso.com, adfs.contoso.com or federation.contoso.com.

![](https://i.imgur.com/Dy6O4Cs.png)




Active Directory Federation Service is a tool that helps connect a company's local network (on-premises) to cloud services. It allows employees use their regular work login to access both on-premises apps and cloud apps without needing a separate cloud password. ==It is similar to a single sign on service.== 

However, there is difference between SSO vs federation.

Federation is about multiple systems or organizations trusting each other to authenticate users. Like how I logged in using Google. 

SSO is more about an authenticated user don't need to login again to access other related services ==within the same system or domain==