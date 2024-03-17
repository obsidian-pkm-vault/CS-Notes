---
Author:
  - Xinyang YU
Author Profile:
  - https://linkedin.com/in/xinyang-yu
tags:
  - dsa
Creation Date: 2023-08-30T12:54:00
Last Date: 2024-03-12T12:17:39+08:00
References: 
---
## Abstract
---
![[queue.png|500]]
- [[Data Structure#Linear]]
- Aka [[Array]]/[[Linked List]] with limitations
- Can be used in an online ordering system


### Time Complexity
- O(1) to offer() - push in an element
- O(1) to poll() - pop out an element
- O(1) to peek() - read the element that is the first to be pop out

## Implementation
---

>[!note] Implementation with Circular Array
> - [[Array#Circular Array]]
> - [Visual](https://www.hello-algo.com/chapter_stack_and_queue/queue/#2)
> - push() at the rear index
> - pop() & peek() at the head index

>[!note] Implementation with [[Linked List#Single Linked List]]
>- [Visual](https://www.hello-algo.com/chapter_stack_and_queue/queue/#1)
>- push() from tail node
>- pop() & peek() from the head node

- The difference in the 2 implementation is similar to [[Stack#2 implementation comparison| Stack implementation comparison]]


## Monotonic Queue
---
- Implemented with [[Deque]], I am not sure if it can be implemented with [[Queue (FIFO)]]
>[!example] [Sliding Window Maximum](https://leetcode.cn/problems/sliding-window-maximum/)
>- Finding the biggest element in a sliding window



## Questions
---
- [Leetcode Questions](https://github.com/youngyangyang04/leetcode-master#栈与队列)

