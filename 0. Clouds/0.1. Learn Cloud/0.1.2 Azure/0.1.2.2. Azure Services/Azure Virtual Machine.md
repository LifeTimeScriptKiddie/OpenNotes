---
{"dg-publish":true,"permalink":"/0-learn-like-a-systems-engineer/clouds/azure/azure-services/azure-virtual-machine/","noteIcon":"","created":"2025-04-15T14:11:19.586-04:00"}
---
We can access VM via azure portal. 
![](https://i.imgur.com/qDn4qG8.png)

![](https://i.imgur.com/4CicjRW.png)

![](https://i.imgur.com/6d6xcgD.png)


Different Zones
![](https://i.imgur.com/1zaYGwl.png)





| Command                                  | Description                                                                      | Example                                                                                          |
| ---------------------------------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| `az vm list`                             | Lists all VMs in a subscription or resource group.                               | `az vm list --output table`                                                                      |
| `az vm show`                             | Displays detailed information about a specific VM.                               | `az vm show --resource-group <rg-name> --name <vm-name>`                                         |
| `az vm get-instance-view`                | Gets runtime information about a VM, including power state and health status.    | `az vm get-instance-view --resource-group <rg-name> --name <vm-name>`                            |
| `az vm list-ip-addresses`                | Lists the public and private IP addresses associated with VMs in a subscription. | `az vm list-ip-addresses --resource-group <rg-name>`                                             |
| `az vm list-sizes`                       | Lists available sizes for VMs in a specific region.                              | `az vm list-sizes --location <region>`                                                           |
| `az vm list-skus`                        | Lists compute SKUs available in a specific region.                               | `az vm list-skus --location <region>`                                                            |
| `az vm open-port`                        | Opens specific ports to inbound traffic for a VM.                                | `az vm open-port --port 22 --resource-group <rg-name> --name <vm-name>`                          |
| `az vm capture`                          | Captures the state of a VM for imaging.                                          | `az vm capture --resource-group <rg-name> --name <vm-name> --vhd-name-prefix <prefix>`           |
| `az vm diagnostics get-default-config`   | Retrieves the default diagnostics configuration for a VM.                        | `az vm diagnostics get-default-config`                                                           |
| `az vm disk list`                        | Lists all managed disks attached to a VM.                                        | `az vm disk list --resource-group <rg-name>`                                                     |
| `az vm encryption show`                  | Shows encryption status for a VM's disks.                                        | `az vm encryption show --resource-group <rg-name> --name <vm-name>`                              |
| `az vm extension list`                   | Lists the extensions installed on a VM.                                          | `az vm extension list --resource-group <rg-name> --vm-name <vm-name>`                            |
| `az vm identity show`                    | Shows the identity of a VM, including any managed identities.                    | `az vm identity show --resource-group <rg-name> --name <vm-name>`                                |
| `az vm run-command list`                 | Lists all available run commands for a VM.                                       | `az vm run-command list --resource-group <rg-name> --name <vm-name>`                             |
| `az vm monitor metrics list-definitions` | Lists the available metrics that can be monitored for a VM.                      | `az vm monitor metrics list-definitions --resource-group <rg-name> --name <vm-name>`             |
| `az vm secret list`                      | Lists all secrets associated with a VM.                                          | `az vm secret list --resource-group <rg-name> --name <vm-name>`                                  |
| `az vm assess-patches`                   | Assesses patch compliance for a VM.                                              | `az vm assess-patches --resource-group <rg-name> --name <vm-name>`                               |
| `az network nsg show`                    | Shows the network security group (NSG) associated with a VM's NIC.               | `az network nsg show --resource-group <rg-name> --name <nsg-name>`                               |
| `az network nic show`                    | Displays detailed information about a network interface attached to a VM.        | `az network nic show --resource-group <rg-name> --name <nic-name>`                               |
| `az network public-ip show`              | Shows details of the public IP associated with a VM.                             | `az network public-ip show --resource-group <rg-name> --name <public-ip-name>`                   |
| `az vm identity assign`                  | Assigns a managed identity to a VM.                                              | `az vm identity assign --resource-group <rg-name> --name <vm-name>`                              |
| `az disk show`                           | Displays detailed information about a specific disk attached to a VM.            | `az disk show --resource-group <rg-name> --name <disk-name>`                                     |
| `az vm generalize`                       | Generalizes a VM for image creation.                                             | `az vm generalize --resource-group <rg-name> --name <vm-name>`                                   |
| `az vm monitor metrics tail`             | Streams real-time metric values for a VM.                                        | `az vm monitor metrics tail --resource-group <rg-name> --name <vm-name> --metric CPUUtilization` |

[Commands from Microsoft](https://learn.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest)

---
Azure VM can be found by checking resources. 

```
az resource list
```


```
Install-Module -Name Az -Repository PSGallery -Force
Connect-AzAccount
Get-AzVM -ResourceGroupName "content-static-2" -Name "SECURITY-PC" -UserData
```

  

`az vm` or  `Get-AzVM` can be used. 
```


az vm user-data show --name <VMName> --resource-group <ResourceGroupName>

az vm list --query "[].{Name:name, OS:storageProfile.osDisk.osType, CustomData:osProfile.customData}" --output table


Get-AzVM | Select-Object -Property Name, OSProfile, StorageProfile.ImageReference, StorageProfile.OsDisk, OSProfile.CustomData

(Get-AzVM -ResourceGroupName <ResourceGroupName> -Name <VMName>).OSProfile.CustomData

```

Query to get vm user data
```
 Get-AzVM -ResourceGroupName "content-static-2" -Name "SECURITY-PC" -UserData
```

