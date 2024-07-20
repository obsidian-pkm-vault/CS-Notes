---
Author:
  - Xinyang YU
Author Profile:
  - https://linkedin.com/in/xinyang-yu
tags:
  - dsa
Creation Date: 2023-08-06T14:45:06+08:00
Last Date: 2024-07-20T16:44:16+08:00
References: 
description: Simple yet Evil
---
## Abstract
---
- [[Algorithm]] that finds the **index of a value** in a **sorted** [[Array]] in `O(logn)`

>[!tip] Avoid Overflow
> Intuitively, we usually use `(right+left)/2` to find the mid point, but `right+left` is risky to [Integer Overflow](https://en.wikipedia.org/wiki/Integer_overflow).
> 
> We can avoid this by using `left + (right-left)/2`.
> 
> 
> 
> Proof: let left be $L$ and right be $R$, $\frac{L+R}{2} = \frac{(R-L) + 2L}{2} = \frac{1}{2} \times ((R-L) + 2L) = \frac{1}{2} \times (R-L) + L$

>[!tip] Array contains duplicate values
> We are unable to determine the **index of the target value** if the elements in the given array **aren't unique**. But we are still able to determine the **first & last appearance** of this particular value, see [First Bad Version](https://leetcode.com/problems/first-bad-version).


## Handling Boundaries
---
### Right Boundary Includes last Element (左闭右闭)
```java
// Assuming nums is an array

// Setting the right boundary [left, right]
int right = nums.length-1;

// The while loop
while (left<=right){...}

// The shrinking of the range
left = mid+1; // When target is bigger
right = mid-1; // When target is smaller
```
- The right boundary **includes** the index of an element of the array

>[!question] Why `left<=right` and not `left<right`
> For ``while (left<right){ ... }``, the loop exits when `left>=right`, we may potentially miss an element which may be the desired value. Since `right` points to an valid index of the array.


>[!important]
>Setting the boundary for `left` and `right` also depends on the question.
>
> Binary search is generally used on **index range**. For questions like ["Kth Smallest Element in a Sorted Matrix"](https://xy241-dsa.notion.site/Kth-Smallest-Element-in-a-Sorted-Matrix-896f67cca6034496af5ed2b56493797c) where `mid` is the potential answer, we set `right = mid` and break the while loop when `left == right`, since `left == right` is the answer. We are using binary search on **number range**.
> 
> We can use binary search to [search for a value in a 2D matrix](https://xy241-dsa.notion.site/74-Search-a-2D-Matrix-a5e993ffe622474e96e9848d88c7e998?pvs=4), given that **each row** is **sorted in non-decreasing order** and the **first integer of each row** is **greater than the last integer of the previous row**. This approach **utilises creative row and column indexing**, where binary search is applied to the **index range**.

### Right Boundary Excludes last Element (左闭右开)
```java
// Assuming nums is an array

// Setting the right boundary [left, right)
int right = nums.length; 

// The while loop
while (left<right){...}

// The shrinking of the range
left = mid+1; // When target is bigger
right = mid; // When target is smaller
```
- The right boundary **excludes** the index of an element of the array

>[!question] Why `left<right` and not `left<=right`
> For ``while (left<=right){ ... }``, the loop exits when `left>right`, we will obtain a mid point that is `nums.length` when desired value is bigger than all of the values inside the array. And `array[nums.length]` will result in an `indexOutRange` error.


## Hidden Power
---
- We can use binary search in optimisation problems,  not just finding an element inside [[Array]]

>[!abstract]
> Assume we have a **monotonic function** `f(x)`. The output of `f(x)` is proportional to its input `x`. That means the bigger the value of `x`, the smaller the output of `f(x)` or the bigger the value of `x`, the bigger the output of `f(x)`. If we want to find the maximum/minimum value of `x` such that the output of `f(x)` is `>=` a constant value $a$, we can make use of binary search!
> 
> The $L$ is the smallest value for `x` and $R$ is biggest value for `x`, the value of `x` acts as the index, and the output of `f(x)` acts as the value at that particular index.

>[!example] **Beer Feast Problem** 🍻
> We are having a beer feast for a group of guests. We have a total supply of 180 mugs of beers. Let `x` be the number of beers we provide to the guests. We have this magical function `f(x)` which calculates a consciousness score of the guests based on the number of beers we give. `x` is inversely proportional to the consciousness score, this means the more beer we give the less conscious guests get. 
> 
> We want to know what is the **maximum number of beers** we can give and the guests can still maintain **at least 50% consciousness**. `f(180)` returns 0% consciousness and `f(0)` returns 100% consciousness. 
> 
> We can make use of binary search to obtain the answer in $O(logn)$. The $L$ is 0 beer and $R$ is 180 beers. We record down the value of `mid` and $L = mid + 1$ when the `f(mid)` is above 50% consciousness and $R = mid -1$ when `f(mid)` is below 50% consciousness. When `f(mid)` gives 50%, the corresponding `mid` value is the the sweet spot for number of beers we can provide. If there isn't a sweet spot, the maximum value of all the `mid` values recorded is the answer.