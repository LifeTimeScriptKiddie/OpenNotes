---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/clouds/azure/tool-blood-hound/","noteIcon":"","created":"2025-04-15T14:11:19.596-04:00"}
---





Start the dataserver!
```
sudo neo4j console

sudo apt-get install bloodhound
```


Download azurehound
```
https://github.com/bloodhoundad/azurehound/releases
```

# 2. Run azurehound

Usernames were given. TenantID was retrieved once we login with the given credentials. 
```bash
az login -u Jose.Rodriguez@megabigtech.com -p Bigt3ch123!                                                                             

[
  {
    "cloudName": "AzureCloud",
    "homeTenantId": "2590ccef-687d-493b-ae8d-441cbab63a72",
    "id": "ceff06cb-e29d-4486-a3ae-eaaec5689f94",
    "isDefault": true,
    "managedByTenants": [],
    "name": "Microsoft Azure Sponsorship",
    "state": "Enabled",
    "tenantDefaultDomain": "megabigtech.com",
    "tenantDisplayName": "Default Directory",
    "tenantId": "2590ccef-687d-493b-ae8d-441cbab63a72",
    "user": {
      "name": "Jose.Rodriguez@megabigtech.com",
      "type": "user"
    }
  }
]


└─$ ./azurehound  -u "Jose.Rodriguez@megabigtech.com" -p 'Bigt3ch123!' list --tenant "2590ccef-687d-493b-ae8d-441cbab63a72" -o output.json  
```

# 3. Custom Query
[[Tool - BloodHound AzureHoundCustomQuery\|Tool - BloodHound AzureHoundCustomQuery]]