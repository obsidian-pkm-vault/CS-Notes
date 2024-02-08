---
Author:
  - Xinyang YU
Author Profile:
  - https://linkedin.com/in/xinyang-yu
tags:
  - system_design
Creation Date: 2023-12-11T23:00:51+08:00
Last Date: 2024-02-08T13:16:33+08:00
References: 
---
## Abstract
---
![[latency_number_visual.png|500]]

Put those times on a human scale by setting **1ns CPU time = 1s human time**
- a **clock cycle** is **~0.1-0.2s**, which is more or less instantaneous for humans. This could be, for example, the time to add 2 small numbers that you already have in transistors.
- If you need to read them off of a page in front of you (**L1/L2 cache**), that could take a few **seconds**
- A [[System Call (系统调用)]] takes a few **minutes**
- [[Context Switch]] is an **hour** or two
- [[HTTP Request]] takes **several hours**
- You need to wait **a day** to **read something from SSD**
- **Writing to SSD** it's gonna be in the mail for around **a week**
- **Seek time of HDD** is like **2 months**
- **Data over the network from another continent** that's a **few years**
- **TLS handshake** is like **a decade**
- **Transfer 1GB over network in same cloud region** - that's like **3 centuries**


>[!bigbrain]- Main Memory faster than System Call
> Writing to [[Main Memory]] involves simply accessing and modifying data within the [[Process (进程)]]'s [[Address Space#Stack Segment]] which can be done with minimal overhead.
> 
> For [[System Call (系统调用)]], it involves transitioning from [[User Space]] to [[Kernel Space]] and [[Privilege Level]] changes etc.