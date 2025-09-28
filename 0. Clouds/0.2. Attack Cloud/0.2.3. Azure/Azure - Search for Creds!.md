## ** Azure - Where Credentials Can Be Found**

| **Service**                           | **Credential Type**       | **Location**                                            | **Extraction Method**                    |
| ------------------------------------- | ------------------------- | ------------------------------------------------------- | ---------------------------------------- |
| **Azure Instance Metadata API**       | Temporary IAM Tokens      | `http://169.254.169.254/metadata/identity/oauth2/token` | `curl` or `wget`                         |
| **Azure Key Vault**                   | API Keys, Secrets         | Vault stored secrets                                    | `az keyvault secret show`                |
| **Azure Managed Identity**            | Temporary Access Tokens   | Metadata API                                            | `curl` to fetch tokens                   |
| **Azure DevOps Repositories**         | Hardcoded API Keys        | DevOps Repos                                            | `git grep` for secrets                   |
| **Blob Storage**                      | Config Files with Secrets | `*.json` or `*.config`                                  | `az storage blob download`               |
| **App Service Environment Variables** | API Keys                  | App Configurations                                      | `az webapp config appsettings list`      |
| **Azure Automation Accounts**         | Runbook Variables         | PowerShell stored credentials                           | `az automation variable list`            |
| **Azure Functions**                   | Hardcoded Secrets         | Environment Variables                                   | `az functionapp config appsettings list` |
| **Log Analytics (Azure Monitor)**     | Sensitive Log Data        | Diagnostic Logs                                         | Query logs for exposed keys              |

### Publicly Accessible Azure Endpoints

| **Service**                  | **Default Exposure** | **Public Endpoint Example**                       | **Notes**                                                   |
| ---------------------------- | -------------------- | ------------------------------------------------- | ----------------------------------------------------------- |
| **Blob Storage**             | Optional             | `https://<account>.blob.core.windows.net/`        | Public containers allow anonymous access if not restricted. |
| **Azure Web Apps**           | Public               | `https://<app>.azurewebsites.net/`                | Public unless access restrictions are configured.           |
| **Virtual Machines**         | Optional             | `<public-ip>:22` (SSH), `<public-ip>:3389` (RDP)  | NSG rules and public IP determine exposure.                 |
| **Azure Kubernetes Service** | Public (default)     | `https://<cluster>.<region>.azmk8s.io`            | API server is public unless private cluster is used.        |
| **Azure SQL Database**       | Public (default)     | `yourserver.database.windows.net`                 | Restrict with firewall or use Private Link.                 |
| **Azure CDN**                | Public               | `https://<cdn>.azureedge.net/`                    | Designed to be internet-facing.                             |
| **Azure Front Door**         | Public               | `https://<domain>.azurefd.net/`                   | Public by design.                                           |
| **Azure Functions**          | Public               | `https://<function>.azurewebsites.net/api/<func>` | Use keys or auth to limit exposure.                         |
| **API Management (APIM)**    | Public (default)     | `https://<apim>.azure-api.net/`                   | Lock down with policies and IP restrictions.                |

