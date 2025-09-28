---
dg-publish: true
---
![](https://i.imgur.com/FWu0aWR.png)


https://stackoverflow.com/questions/58029850/where-to-use-cosmosdb

>- extremely expensive (we all know that)
    - all changes introduced by MS were backwards compatible but they used to crash things in the UI (e.g. partitions with a single __partitionKey partition).
    - unclear roadmap and release dates. E.g. auto-scaling was always a promise without a clear release date.
    - the emulator sucks, new functionality on the engine is always late in emulations or some don´t exist in the emulator
    - backups sucked early on, later versions allowed to do manual backups. Copying a cloud db to the local emulator resorted in writing your own app for backups.
    - they introduced the serverless version (which is not more serverless than the regular version but only limited in comparison, should have been called cheap-o version)
    - horrendous connection failures under stress, apps need to have 50% available CPU all the time not to crash the connections, these do recover well on the SDK but introduce delays that can be confused with throttling
    - DNS failures unless you use service / private endpoints, these also recover well but introduce delays that can be confused with throttling
    - very bad observability support, e.g. app insights does only report on http requests, not tcp connections so you can see some stuff happening at connection level, but not at query level
    - worse possible SDK roadmap, where new versions were introduced not mentioning that old ones are deprecated, so that when you call in for support the first thing they tell you is that you should be using the latest SDK never mentionioning in the first place that the upgrade is mandatory and not a suggestion as shown in their web pages otherwise you don´t get any support from MS if you don´t upgrade.
    - MongoDB compatibility barely working with 50% of all sql semantics.
    - RDBMS support introduced too late, e.g. Postgre for CosmosDB should have been an option from the beginning or something with SQL Sever over Cosmos would have been nice.
    - Auto-indexing is nice, but disabling indexing for all fields not used is hard. So you need to invest a lot of time to optimize it.
    - There is no external profiler like SQL Server. You need to have the developers optimize by running real queries.