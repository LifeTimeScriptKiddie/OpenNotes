# 1. Check the getuserrealm.srf endpoint for domain information


```bash
#Check the getuserrealm.srf endpoint for domain information
curl -s "https://login.microsoftonline.com/getuserrealm.srf?login=$DOMAIN&json=1" | jq .


#Test if the domain is managed or not
curl -s "https://login.microsoftonline.com/getuserrealm.srf?login=$DOMAIN&json=1" | jq .


#Get the NameSpaceType for the domain
curl -s "https://login.microsoftonline.com/getuserrealm.srf?login=$DOMAIN&json=1" | jq -r '.NameSpaceType'

#Check for federation on the domain
curl -s "https://login.microsoftonline.com/getuserrealm.srf?login=$DOMAIN&xml=1"

#Get the TenantID for a managed domain
curl -s "https://login.microsoftonline.com/$DOMAIN/v2.0/.well-known/openid-configuration" | jq -r '.token_endpoint' | cut -d'/' -f4

#Check GetCredentialType endpoint for username enumeration
curl -s -X POST "https://login.microsoftonline.com/common/GetCredentialType" --data "{\"Username\":\"$USERNAME@$DOMAIN\"}" | jq '.IfExistsResult'



```

