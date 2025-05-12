# Problem 2-3: Correctness of Horner's rule

## Problem Description
> The following code fragment implements Horner's rule for evaluating a polynomial
>
> $$
> \begin{aligned}
> P(x) &= \sum_{k=0}^{n}a_kx^k \\
> &= a_0 + x(a_1+x(a_2+\dots+x(a_{n-1}+xa_n)))
> \end{aligned}
> $$
>
> given the coefficients $a_0,a_1,\dots,a_n$ and a value for $x$:
>
> ```
> y=0
> for i=n downto 0
>   y = a_i + x*y
> ```
>
> **a.** In terms of $\Theta$-notation, what is the running time of this code fragment for Horner's rule?
>
> **b.** Write pseudocode to implement the naive polynomial-evaluation algorithm that computes each term of the polynomial from scratch. What is the running timeof this algorithm? How does it compare to Horner's rule?
>
> **c.** Consider the following loop invariant:
>
> At the start of each iteration of the **for** loop of lines 2-3,
> $$
> y=\sum_{k=0}^{n-(i+1)}a_{k+i+1}x^k
> $$
> Interpret a summation with no terms as equaling 0. Following the structure of the loop invariant proof presented in this chapter, use this loop invariant to show that, at termination, $y=\sum_{k=0}^{n}a_kx^k$.
>
> **d.** Conclude by arguing that the given code fragment correctly evaluates a polynomial characterized by the coefficients $a_0,a_1,\dots,a_n$.

## Solutions
### a.
Running time: $\Theta{(n)}$.

### b.
```
y = 0
for k = 0 to n
    y_i = a_k
    for i = 0 upto k
        y_i *= x
    y += y_i
```
The runtime is $\Theta{(n^2)}$. It is slower than Horner's rule.

### c.

**Initialization:** The loop starts at $i=n$ where $y=0$, for $i=n$ we have summation from $k=0$ to $-1$ which means no summation is done and hence $y=0$.

**Maintenance:** Suppose this is true for some $i$,
$$
\begin{aligned}
y&=a_i+x\sum_{k=0}^{n-(i+1)}a_{k+i+1}x^k \\
&=a_i+x\sum_{k=1}^{n-i}a_{k+i}x^{k-1} \\
&=\sum_{k=0}^{n-i}a_{k+i}x^k
\end{aligned}
$$

**Termination:** the loop ends when $i=-1$, the body is executed exactly $n$ times and we get the correct summation.

### d.
In part (c), we conclude that the loop terminate at $y = \sum_{k=0}^{n}a_kx^k$ which is the polynimial expansion itself.

