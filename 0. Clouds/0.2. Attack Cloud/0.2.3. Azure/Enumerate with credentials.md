---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/clouds/azure/enumerate-with-credentials/","noteIcon":"","created":"2025-04-15T14:11:19.593-04:00"}
---








```mermaid
graph TD
    A[Initial Access: Azure Credentials Found] --> B[Login to Azure using PowerShell Az Module or Azure CLI]
    B --> C[Enumerate Tenant Information]
    C --> D[Discover Subscriptions]
    D --> E[Enumerate Resources in Subscription]
    E --> F[Check for Role Assignments and Permissions]
    F --> G[Enumerate Administrative Units]
    G --> H[Check for Roles in Administrative Units]
    H --> I[Exploit Administrative Unit Permissions]
    F --> J[Enumerate Virtual Machines]
    F --> K[Enumerate Storage Accounts]
    F --> L[Enumerate Service Principals]
    J --> M[Lateral Movement: Attempt Access to VMs]
    K --> N[Download Blob Storage Content]
    L --> O[Privilege Escalation via Service Principals]
    M --> P[Post-Exploitation on VMs]
    N --> Q[Exfiltrate Data from Storage Accounts]
    O --> R[Set New Secrets for Service Principals]
    R --> S[Re-Login using New Privileges]
    S --> T[Further Resource Enumeration and Privilege Escalation]
```



```bash
az account list 
az account tenant list # Current tenant info
az account subscription list # Current subscription info
az ad signed-in-user show # Current signed-in user
az ad signed-in-user list-owned-objects # Get owned objects by current user
az account management-group list #Not allowed by default
az resource list

# Role assignment
$ az account show --query user.type -o tsv
$ az role assignment list --assignee <APP_ID> --all

$ az role assignment list --assignee $(az account show --query user.name -o tsv) --all


```