# 1.  Key types!
https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management-choose

```mermaid
graph TD
A[Azure Key Management]
B[Azure Key Valut Standard]
C[Azure Key Valut Premium]
D[Azure Managed HSM]
E[Azure Dedicated HSM]
F[Azure Payment HSM]

A-->B
A-->C
A-->D
A-->E
A-->F


```

The following is the flow chart to choose right key for Azure Environment. 
HSM stands for Hardware Security Module


![](https://i.imgur.com/hSP2I2f.png)




# 2. Enumerate
```mermaid
graph TD
    A[Start: Check Key Vault Access for User] --> B[List all Key Vaults]
    B --> C[Get User Object ID]
    C --> D[Check Access Policies for each Key Vault]
    D --> E{User Object ID Found?}
    E -- Yes --> F[User has access to Key Vault]
    E -- No --> G[User does not have access to Key Vault]

```

| **Step**                     | **Description**                                                | **Command**                                                                                               |
| ---------------------------- | -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **List all Key Vaults**      | Lists all the Key Vaults in the subscription.                  | `az keyvault list --query "[].{Name:name, Location:location}" --output table`                             |
| **Get UserPrincipalName**    |                                                                | `az ad user list --query "[].{Name:displayName, UPN:userPrincipalName}" --output table`                   |
| **Get User Object ID**       | Retrieves the Object ID for the specific user.                 | `az ad user show --id <UserPrincipalName> --query "id"`                                                   |
| **Check Access Policies**    | Shows the access policies of a specific Key Vault.             | `az keyvault show --name <KeyVaultName> --query "properties.accessPolicies"`                              |
| **Filter for User's Access** | Filters the Key Vault’s access policies to check for the user. | `az keyvault show --name <KeyVaultName> --query "properties.accessPolicies[?objectId=='<UserObjectId>']"` |


## 2.1 Azure Key Secrets
https://learn.microsoft.com/en-us/cli/azure/keyvault?view=azure-cli-latest
```
az keyvault list --query "[].{Name:name, Location:location}" --output table

`az ad user list --query "[].{Name:displayName, UPN:userPrincipalName}" --output table`

`az ad user show --id <UserPrincipalName> --query "id"`

`az keyvault show --name <KeyVaultName> --query "properties.accessPolicies"`

`az keyvault show --name <KeyVaultName> --query "properties.accessPolicies[?objectId=='<UserObjectId>']"`


az keyvault secret list --vault-name <name>

az keyvault secret show --vault-name <vault-Name> --name <keyname>

az keyvault secret download  --vault-name <vault-Name> --name <keyname> --file <filename>




```


Good examples are located [../PwnedLabs/5. Unmask Privileged Access in Azure](<../../../0.2. Attack Cloud/0.2.3. Azure/PwnedLabs/5. Unmask Privileged Access in Azure.md>)
