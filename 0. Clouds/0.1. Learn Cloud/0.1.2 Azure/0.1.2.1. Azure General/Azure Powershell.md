---
{"dg-publish":true,"permalink":"/0-learn-like-a-systems-engineer/clouds/azure/azure-general/azure-powershell/","noteIcon":"","created":"2025-04-15T14:11:19.583-04:00"}
---





https://learn.microsoft.com/en-us/powershell/azure/?view=azps-12.3.0


https://learn.microsoft.com/en-us/azure/governance/resource-graph/first-query-powershell

```
Install-Module -Name Az -Repository PSGallery -Force
Update-Module -Name Az -Force
Connect-AzAccount

Install-Module -Name Az.ResourceGraph -Repository PSGallery -Scope CurrentUser

```

| Resource Type    | Azure PowerShell Module | Noun Prefix      |
| ---------------- | ----------------------- | ---------------- |
| Resource Groups  | Az.Resources            | AzResourceGroup  |
| Virtual Machines | Az.Compute              | AzVM             |
| Storage Accounts | Az.Storage              | AzStorageAccount |
| Key Vault        | Az.KeyVault             | AzKeyVault       |
| Web Applications | Az.Websites             | AzWebApp         |
| SQL Databases    | Az.Sql                  | AzSqlDatabase    |



Great open source!
https://github.com/andreipintica/Azure-PowerShell-CheatSheet

