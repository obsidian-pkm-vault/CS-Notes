---
Author:
  - Xinyang YU
Author Profile:
  - https://linkedin.com/in/xinyang-yu
tags:
  - problem_solving
Creation Date: 2023-08-16T22:24:16+08:00
Last Date: 2024-02-14T10:19:14+08:00
References: 
---
## Probability Problem
---

![[probability_problem.png|300]]
- With [[Problem Solving#5. Draw a picture]]. We can associate the 2 numbers with a point on the x-y axis. `0<=x<=1`, `0<=y<=1`
- With [[6. Ask a simpler version of the problem]]

>[!question] What is the region on the graph that x/y will round down to 0?
>![[xy round down to 0.png|500]]
>- Answer: y needs to be bigger than x, so it is the area above the y=x

>[!question] What is the region on the graph that x/y will round down to 2?
>![[xy round down to 2.png|500]]
>- Answer: x needs to be equal or greater than y twice && x needs to be smaller than y 3 times. Thus it is the area below y=x/2, above y=x/3x

>[!success] Answer is basically sum of the triangles on the graph

>[!code] Take advantage of Python codes to obtain an answer
> ```python
> !pip3 install numpy
> 
> import numpy as np
> 
> data_size = 10**6
> 
> x = np.random.random(data_size)
> y = np.random.random(data_size)
> ratios = x / y
> round_down_ratio = np.floor(ratios)
> even_ratio_res = (round_down_ratio % 2 == 0).mean()
> ```
