# Problem 2-2: Correctness of bubblesort

## Problem Description
> Bubblesort is a pupular, but ineficient, sorting algorithm. It workds by repeatedly swapping adjacent elements that are out of order.
>
> ```
> BUBBLESORT(A)
> for i = 1 to A.length - 1
>   for j = A.length downto i + 1
>       if A[j] < A[j-1]
>           exchange A[j] with A[j-1]
> ```
>
> **a.** Let $A'$ denote the output of BUBBLESORT($A$). To prove that BUBBLESORT is correct, we need to prove that it terminates and that
> $$
> A'[1] \leq A'[2] \leq \dots \leq A'[n] \tag{2.3}
> $$
> where $n$ = $A.length$. In order to show that BUBBLESORT actually sorts, what else do we need to prove?
>
> The next two parts will prove inequality $(2.3)$.
> 
> **b.** State precisely a loop invariant for the **for** loop in lines 2-4, and prove that this loop invariant holds. Your proof should use the structure of the loop invariant proof presented in this chapter.
>
> **c.** Using the termination condition of the loop invariant proved in part (b), state a loop invariant for the **for** loop in lines 1-4 that will allow you to prove inequality $(2.3)$. Your proof should use the structure of the loop invariant proof presented in this chapter.
>
> **d.** What is the worst-case running time of bubblesort? How does it compare to the running time of insertion sort?

## Solutions
### a.
We need to prove $A'$ is a permutation of $A$, which means $A'$ and $A$ contains the same elements.

### b.
**Loop invariant:** The position of smallest element in the subarray $A[j..n]$ is at most $j$.

**Initialization:** The loop starts with $j = n$. $A[n..n]$ contains one element only and its position is equals to $n$.

**Maintenance:** Suppose $j=k$, we compare $A[k-1]$ and $A[k]$ and swap them if $A[k] < A[k-1]$, which means $A[k-1]$ will always be the smaller element among them. Since the position of the smallest element is at most $k$ before swapping. After swapping, the position of the smallest element is at most $k-1$.

**Termination:** The loop terminates when $j=i$, the position of the smallest element in $A[i..n]$ is $i$.

### c.
**Loop invariant:** The subarray $A[1..i-1]$ contains the $i-1$ smallest elements in $A$ in non-decreasing order.

**Initialization:** The loop starts with $i = 1$. $A[1..0]$ contains zero element and is trivially sorted.

**Maintenance:** Suppose $i=k$ and $A[1..k-1]$ is sorted and contains $k-1$ smallest elements, the smallest element in $A[k..n]$ is $k$ after the inner loop using the result of part (b). Hence, the subarray $A[1..k]$ contains the $k$ smallest elements and is sorted in non-decreasing order. The loop invariant is maintained.

**Termination:** The loop terminates when $i=n$, we have $A[1..n-1]$ contains the smallest $n-1$ smallest elements and in non-decreasing order. Therefore, the $n$ th element is the largest element. Hence the array $A$ becomes sorted and inequality $(2.3)$ holds. 

### d.
The worst-case running time of bubblesort is $\Theta{(n^2)}$. The outer loop execute $n$ times while the $i$ th inner loop execute $n-i$ times. Comparing to the best-case running time of insertion sort $\Theta{(n)}$, that of bubblesort is also $\Theta{(n^2)}$.