---
dg-publish: true
---
https://learn.microsoft.com/en-us/azure/azure-functions/functions-overview
![](https://i.imgur.com/ZRXdb3N.png)


Function apps vs [[Azure App Services]]
https://stackoverflow.com/questions/67546988/azure-app-service-plan-function-vs-app-service

>An Azure function is [triggered by an external event or a timer](https://learn.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings?tabs=csharp#supported-bindings). It then executes the code of the function. When hosted on a consumption plan this execution is allowed to run for [5 or 10 minutes max](https://learn.microsoft.com/en-us/azure/azure-functions/functions-scale#timeout). When you need a longer execution time you need to run it on an App Service Plan.