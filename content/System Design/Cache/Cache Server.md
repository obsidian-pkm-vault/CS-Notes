---
Author:
  - Xinyang YU
Author Profile:
  - https://linkedin.com/in/xinyang-yu
tags:
  - system_design
Creation Date: 2023-12-31, 20:32
Last Date: 2024-11-06T17:17:47+08:00
References: 
draft: 
---
## Abstract
---
![[cache_server.png]]
- A temporary data store layer, much faster to obtain the data compared to obtaining data from [[Database]]
- The above cache server is using [[#Read-through Cache Strategy]]
- Memcached and Redis are popular Cache Server, they have API which can be interacted with programming languages
```python
# The cached data has a key 'myKey', and value 'hi there'
# The cached data will stay in the Cacahe server for 3600s

SECONDS = 1
cache.set('myKey, 'hi there', 3600 * SECONDS)
cache.get('myKey')
```

>[!success] Better performance
> The ability to reduce compute/database workloads, and scale the [[Cache Server]] independently. Thus better [[System Design#Scalability (可扩展性)]].

>[!question] When to use cache server?
> Use [[Cache Server]] when data is **read frequently** but **modified infrequently**.
> 
> Cache server is not ideal for **persisting data** since cached data is stored in [[Main Memory]].

>[!important] Expiration policy
> It is a good practice to set how long it takes for the cached data to expire and get removed from [[Cache Server]]. Or cached data will stay in the [[Main Memory]] forever.
> 
> Not to make the expiration date too short as this will cause the system to reload data from the [[Database]] too frequently. Not to make the expiration date too long as the data can become **stale**.

>[!important] Consistency
> Basically keep the data in [[Database]] and [[Cache Server]] in sync. Inconsistency can happen because **data-modifying operations** on the database and cache server are not in **a single transaction**.
> 
> When scaling across **multiple regions**, maintaining consistency between the database and cache server is **challenging**.

>[!important] Mitigating failures
> A single [[Cache Server]] is a [[System Design#Single Point of Failure]]. Multiple cache servers across different data centers are recommended to avoid single point of failure.
> 
> It is recommended to **over-provision** the required memory by certain percentages. This provides a **buffer** as the memory usage increases







