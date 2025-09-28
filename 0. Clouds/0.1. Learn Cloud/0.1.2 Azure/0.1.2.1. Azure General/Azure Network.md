---
{"dg-publish":true,"permalink":"/0-learn-like-a-systems-engineer/clouds/azure/azure-general/azure-network/","noteIcon":"","created":"2025-04-15T14:11:19.583-04:00"}
---






https://learn.microsoft.com/en-us/cli/azure/network/public-ip?view=azure-cli-latest


```
az network public-ip list
az network public-ip list -g MyResourceGroup --query "[?dnsSettings.domainNameLabel=='MyLabel']"



az network public-ip show
az network public-ip show -g MyResourceGroup -n MyIp --query "{fqdn: dnsSettings.fqdn,address: ipAddress}"

```