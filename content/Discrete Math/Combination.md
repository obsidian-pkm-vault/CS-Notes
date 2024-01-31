---
Author:
  - Xinyang YU
Author Profile:
  - https://linkedin.com/in/xinyang-yu
tags:
  - discrete_math
Creation Date: 2024-01-28, 15:23
Last Date: 2024-01-31T08:54:20+08:00
References: 
draft: 
description: 
sr-due: 2024-02-01
sr-interval: 1
sr-ease: 170
---
## Abstract
---
- The **selection of items** from a larger set **without considering the order** of selection
- The number of combinations can be calculated using the [[#Binomial Coefficient]]

## Binomial Coefficient
---
- $\binom{n}{k}$ is the **number of ways**, **disregarding order**, that $k$ objects **can be chosen** from among $n$ objects
</br>


- Also known as the number of **k-element** [[Set#Subset]] (or **k-combinations**) of a **n-element** [[Set]] 
- $\binom{2}{1} = 2$, because given a set of 2 elements $\{1,2\}$ for example, there are 2 subsets of 1 elements: $\{1\}$ and $\{2\}$ 

>[!question] So why is it called Binomial Coefficient?
>- $\binom{n}{k}$ gives the [[#Coefficient]] of one of the **term** of the **expansion** [[#Binomial]] $(a+b)^n$ 
>- The term is expressed as $a^{n-k} \times b^{k}$


### Binomial
- **Bi** means two
- A mathematical expression or algebraic equation that consists of **two terms** connected by a **plus** or **minus** sign, general form is $(a+b)$ or $(a-b)$
### Coefficient
- Constant [[Factor]] that multiplies a variable
- For example,  $5$ is the coefficient of $5x$





### Formula 1
$$
\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}
$$
- Formula 1 uses [[Recursion]]
- The idea is to fix an element `x` in the set. If `x` is included in the subset, we have to choose `k − 1` elements from `n − 1` elements, or if `x` is not included in the subset, we have to choose `k` elements from `n − 1` elements
- There are two independent paths here, so we perform [[Counting#Rule of Sum]]
- Since there is recursion involved, there is base case to terminate the recursion too. The base cases are $\binom{n}{0} = \binom{n}{n} = 1$. Because there is always **exactly one way** to construct an **empty subset** and a subset that contains **all the elements**
</br>

- Below is an implementation of formula 1 in Java
<div class="onecompilerCode-wrapper">
<iframe
 class="onecompilerCode"
 frameBorder="0" 
 src="https://onecompiler.com/embed/java/422rh3h5s?codeChangeEvent=true&theme=dark&hideLanguageSelection=true&hideNew=true&hideNewFileOption=true&availableLanguages=true&hideTitle=true&hideStdin=true" 
 ></iframe>
 </div>

>[!help]- Is the code editor above not showing the correct source code?
> Here is a backup, please report the issue [here](https://github.com/xy-241/CS-Notes/issues) or comment down below, so I can look into the issue. Thanks :)
>```java
> class Binom {
>   public static void main(String[] args) {
>     long startTime = System.currentTimeMillis();
>       
>     long res = binom(50,6);
>     
>     long endTime = System.currentTimeMillis();
>     long elapsedTime = endTime - startTime;
>     
>     
>     System.out.println("Elapsed time: " + elapsedTime + " milliseconds");
>     System.out.println(res);
>   }
>   
>   public static int binom(int n, int k) {
>     if (n == k) return 1; // C(n,n)
>     if (k == 0) return 1; // C(n,0)
>  
>     return binom(n-1, k) + binom(n-1, k-1);
>   }
> }
>```

>[!caution] Exponential Time Complexity
>For $\binom{20}{10}$, formula 1 takes a **few ms**, while [[#Formula 2]] only takes **0ms**

>[!success] No Overflow Issue
>As long as the given $n$ is within the range of `long`, we will not face any overflow issue
### Formula 2
$$
\binom{n}{k} = \frac{n!}{k!(n-k)!}
$$
- $n!$ includes counting that have the same set of elements but different order but combination doesn't consider the order, so we introduce the [[Factor|Divisor]] $k!$ and $(n-k)!$ avoid overcounting
- $\frac{n!}{(n-k)!}$ means how many ways to choose $k$ elements from $n$ element where the **order matters** 
- $\frac{n!}{k!(n-k)!}$ removes the counting that has the same set of elements
</br>

- Below is an implementation of formula 1 in Java
<div class="onecompilerCode-wrapper">
<iframe
 class="onecompilerCode"
 frameBorder="0" 
 src="https://onecompiler.com/embed/java/422v86gfy?codeChangeEvent=true&theme=dark&hideLanguageSelection=true&hideNew=true&hideNewFileOption=true&availableLanguages=true&hideTitle=true&hideStdin=true" 
 ></iframe>
 </div>

>[!help]- Is the code editor above not showing the correct source code?
> Here is a backup, please report the issue [here](https://github.com/xy-241/CS-Notes/issues) or comment down below, so I can look into the issue. Thanks :)
> ```java
> class Binom {
>   public static void main(String[] args) {
>     long startTime = System.currentTimeMillis();
>       
>     long res = binom(20,10);
>     
>     long endTime = System.currentTimeMillis();
>     long elapsedTime = endTime - startTime;
>     
>     
>     System.out.println("Elapsed time: " + elapsedTime + " milliseconds");
>     System.out.println(res);
>   }
>   
>   public static long binom(int n, int k) {
>     long permutation = calFactorial(n) / calFactorial(n-k);
>     long combination = permutation / calFactorial(k);
>  
>     return combination;
>   }
>   
>   public static long calFactorial(long x) {
>     long res = 1;
>     for (int i=1; i<=x; i++) {
>       if (Long.MAX_VALUE / i < res) {
>         throw new ArithmeticException("Overflow during factorial calculation");
>       }
> 
>       res *= i;
>     }
>     return res;
>   }
> }
> ```

>[!success] Linear Time Complexity
>For $\binom{20}{10}$, [[#Formula 1]] takes a **few ms**, while Formula 2 only takes **0ms**

>[!warning] Overflow Issue
>Try change the $n$ from $20$ to $21$ in the editor above, you should get an overflow error. Because $21!$ is out of the range the `long` can cover
>
>We can handle this with [Scientific notation - Wikipedia](https://en.wikipedia.org/wiki/Scientific_notation), but this introduces extra logic 

## Binomial Coefficient Properties 
---
### Symmetry Property
$$
\binom{n}{k} = \binom{n}{n-k}
$$
#### Proof
For $\binom{n}{k}$:
$$
\binom{n}{k} = \frac{n!}{k!(n-k)!}
$$

For $\binom{n}{n-k}$:
$$
\binom{n}{n-k} = \frac{n!}{(n-k)![n-(n-k)]!}
$$
$$
\frac{n!}{(n-k)![n-(n-k)]!} = \frac{n!}{(n-k)!(n-n+k)!}
$$
$$
\frac{n!}{(n-k)!(n-n+k)!} = \frac{n!}{(n-k)!(0+k)!}
$$
$$
\frac{n!}{(n-k)!(0+k)!} = \frac{n!}{(n-k)!k!}
$$
Therefore $\binom{n}{k} = \binom{n}{n-k}$, because:
$$
\frac{n!}{k!(n-k)!} = \frac{n!}{(n-k)!k!}
$$

### Sum of Coefficient
$$
(a+b)^{n}= \sum_{k=0}^{n} \binom{n}{k}a^{n-k}b^{k}
$$


## References
---
- [Competitive Programmer’s Handbook](https://cses.fi/book/book.pdf)