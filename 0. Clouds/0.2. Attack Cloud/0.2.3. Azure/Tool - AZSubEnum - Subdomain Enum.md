---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/clouds/azure/tool-az-sub-enum-subdomain-enum/","noteIcon":"","created":"2025-04-15T14:11:19.596-04:00"}
---






AzSubEnum
https://github.com/yuyudhn/AzSubEnum

Let’s take a look at the following code snippet. It indicates the possible subdomains that can be used by each Azure service. It uses .com, .net, and .io. 


```bash
            'onmicrosoft.com': 'Microsoft Hosted Domain',
            'scm.azurewebsites.net': 'App Services - Management',
            'azurewebsites.net': 'App Services',
            'p.azurewebsites.net': 'App Services',
            'cloudapp.net': 'App Services',
            'file.core.windows.net': 'Storage Accounts - Files',
            'blob.core.windows.net': 'Storage Accounts - Blobs',
            'queue.core.windows.net': 'Storage Accounts - Queues',
            'table.core.windows.net': 'Storage Accounts - Tables',
            'mail.protection.outlook.com': 'Email',
            'sharepoint.com': 'SharePoint',
            'redis.cache.windows.net': 'Databases-Redis',
            'documents.azure.com': 'Databases-Cosmos DB',
            'database.windows.net': 'Databases-MSSQL',
            'vault.azure.net': 'Key Vaults',
            'azureedge.net': 'CDN',
            'search.windows.net': 'Search Appliance',
            'azure-api.net': 'API Services',
            'azurecr.io': 'Azure Container Registry'
```