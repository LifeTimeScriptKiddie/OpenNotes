---
{"dg-publish":true,"permalink":"/0-learn-like-a-systems-engineer/clouds/azure/azure-general/tenant-subscription-resource/","noteIcon":"","created":"2025-04-15T14:11:19.584-04:00"}
---




# 1. Tenant

https://www.devopsschool.com/blog/understanding-tenants-subscriptions-regions-and-geographies-in-azure/

![](https://i.imgur.com/Rn9dh3C.png)

==Here AAD needs to be replaced with Entra ID. ==
>A Tenant, as it relates to Azure, refers to a single instance of Azure Active Directory, or, as it is often called “Azure AD”. Azure AD is a key piece of Microsoft’s cloud platform as it provides a single place to manage users, groups and the permissions they hold in relation to applications published in Azure AD.


## 1.1 Tenant ID

> Your Microsoft 365 tenant ID is a globally unique identifier (GUID) that is different than your organization name or domain. You can use this identifier when you configure OneDrive policies.

Tenant ID can be identified from a various locations.

https://learn.microsoft.com/en-us/sharepoint/find-your-office-365-tenant-id

```
Get-AzSubscription
```
![](https://i.imgur.com/XLUxum0.png)

Home --> Entra ID 
![](https://i.imgur.com/3YHWa4n.png)

Home --> Tenant Properties

![](https://i.imgur.com/CxIQrYZ.png)

---

# 2. Subscription

![](https://i.imgur.com/fAiM5Zm.png)


https://www.devopsschool.com/blog/understanding-tenants-subscriptions-regions-and-geographies-in-azure/
>A Subscription in Azure is a logical container into which any number of resources (Virtual Machines, Web Apps, Storage Accounts, etc) can be deployed. It can also be used for coarse-grained access control to these resources, though the correct approach these days is to leverage Role Based Access Control (RBAC) or Management Groups.

https://learn.microsoft.com/en-us/entra/fundamentals/how-subscriptions-associated-directory

![](https://i.imgur.com/TeIkrIR.png)





## 2.1 Subscription ID
https://wmatthyssen.com/2019/09/06/azure-tip-how-to-quickly-find-your-azure-subscription-id-guid/


An Azure Subsciption ID is **a 32-digit GUID, which is associated with an Azure Subscription**. 

```
Get-AzSubscription
```
![](https://i.imgur.com/XLUxum0.png)

From the Home --> Subscription page. 
![](https://i.imgur.com/hKt1cn8.png)






---
# 3. Resource Group / Resource


![](https://i.imgur.com/fAiM5Zm.png)


# 3.1 Resource Group
https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview
==resource group== - A container that holds related resources for an Azure solution. The resource group includes those resources that you want to manage as a group. You decide which resources belong in a resource group based on what makes the most sense for your organization.


## 3.2 Resource
==resource== - A manageable item that is available through Azure. Virtual machines, storage accounts, web apps, databases, and virtual networks are examples of resources. Resource groups, subscriptions, management groups, and tags are also examples of resources.