# 1. Overview
https://learn.microsoft.com/en-us/azure/app-service/overview
> Azure App Service is an HTTP-based service for hosting web applications, REST APIs, and mobile back ends. You can develop in your favorite language, be it .NET, .NET Core, Java, Node.js, PHP, or Python. Applications run and scale with ease on both Windows and Linux-based environments.


https://learn.microsoft.com/en-us/azure/app-service/

Main page of App services

![](https://i.imgur.com/D8k2yCj.png)



## 1.1 Kudu
https://learn.microsoft.com/en-us/azure/app-service/resources-kudu
>Kudu is the engine behind [git deployments in Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/web-sites-publish-source-control/). It can also run outside of Azure.


https://github.com/projectkudu/kudu/wiki
https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service
>If your web site has URL `http://mysite.azurewebsites.net/`, then the root URL of the Kudu service is `https://mysite.scm.azurewebsites.net/`. Note the added `scm` token.


==Alert== : [Ones with Kudu access are ones owning the site - regardless if read-only or not. To expand, they can deploy any codes (good or malicious) to and able to read any secret settings of the site (eg. KeyVault, SQL and Storage credentials, Private Certificates, etc.). Hence for Azure, only those with Contributor / Owner access (to be exact, with `microsoft.web/sites/publish/action` or, for slot, `microsoft.web/sites/slots/publish/action`) can access to Kudu (SCM).](https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service#once-youre-in-the-kudu-service)



# Commands
https://learn.microsoft.com/en-us/cli/azure/webapp?view=azure-cli-latest
```
az webapp list
```

