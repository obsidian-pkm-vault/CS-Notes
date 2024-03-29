---
Author:
  - Xinyang YU
Author Profile:
  - https://linkedin.com/in/xinyang-yu
tags:
  - OS
  - c
Creation Date: 2023-10-16T10:11:00
Last Date: 2024-03-28T20:17:42+08:00
References:
  - "C Intro Example: https://youtu.be/YSn8_XdGH7c?si=9rgRNBUgseCMOiTl"
---
## Abstract
---
- Limit the number of [[Process (进程)]]/[[Thread]] running on a particular resource at any time with a **non-negative integer**

### Simultaneous Multi-Locking
- Semaphore can be used to **lock a resource** at more than one [[Process (进程)]]/[[Thread]] at the **same time**
- For example, maximum 5 database connections & online game queueing system 
### Decoupled Locking & Releasing 
- The locking & releasing can be decoupled into 2 different [[Process (进程)]]/[[Thread]]
- We can use this property to control how many times a [[Process (进程)]]/[[Thread]] runs (locking) based on the number of [[Interrupts (中断)]] (releasing)

## Code Snippets
---
- `sem_t semaphore;` & `sem_init(&semaphore, 0, 1);`
- Decrement the value when a [[Process (进程)]]/[[Thread]] running - `sem_wait(&semaphore);`
- Increase the value when a [[Process (进程)]]/[[Thread]] finishes running - `sem_post(&semaphore);`
```c
#include <semaphore.h>

int main() {
  sem_t semaphore;
  // 0 means it is not shared with other processes, 1 means only 1 thread can run at a time
  sem_init(&semaphore, 0, 1);
  
  sem_wait(&semaphore); // semmaphore--
  sem_post(&semaphore); // semmaphore++
  
  sem_destroy(&semaphore);
  return 0;
}
```

