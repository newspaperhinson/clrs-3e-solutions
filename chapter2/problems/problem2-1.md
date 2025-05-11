# Problem 2-1: Insertion sort on small arrays in merge sort

## Problem Description
> Although merge sort runs in $\Theta{(n \log_2{n})}$ worst-case time and insertion sort runs in $\Theta{(n^2)}$ worst-case time, the constant factors in insertion sort can make it faster in practice for small problem sizes on many machines. Thus, it makes sense to coarsen the leaves of the recursion by using insertion sort within merge sort when subproblems become sufficiently small. Consider a modification to merge sort in which $n/k$ sublists of length $k$ are sorted using insertion sort and then merged using the standard merging mechanism, where $k$ is a value to be determined.
>
> **a.** Show that insertion sort can sort the $n/k$ sublists, each of length $k$, in $\Theta{(nk)}$ worst-case time.
>
> **b.** Show how to merge the sublists in $\Theta{(n \log_2{(n/k)})}$ worst-case time
>
> **c.** Given that the modified algorithm runs in $\Theta{(nk + n\log_2{(n/k)})}$ worst-case time, what is the largest value of $k$ as a function of $n$ for which the modified algorithm has the same running time as standard merge sort, in terms of $\Theta$-notation?
>
> **d.** How should we choose $k$ in practice?

### a.

To execute insertion sort on sublists with length $k$, $n/k$ times. The worst-case time complexity follows:
$$
T(n) = \frac{n}{k} \Theta{(k^2)} = \Theta{(n/k \times k^2)} = \Theta{(nk)}
$$

### b.
For merging $n/k$ arrays with length $k$ into a single array with length $n$, one can merge the arrays in pairs. A merge tree can be constructed with $\log_2{(n/k)}$ number of layers and each layers cost $n$ time. Therefore, the merging costs $\Theta{(n \log_2{(n/k)})}$ worst-case time.

### c.
In order to have $\Theta{(n \log_2{n})}$ for the modified algorithms:
$$
\Theta{(nk+n\log_2{(n/k)})} = \Theta{(nk+n\log_2{n} - n\log_2{k})} = \Theta{(n \log_2{n})}
$$
Since the $n\log_2{k}$ term is less dominant than the term $nk$, one can consider the effect of $nk$ on the running time only. Treating $k$ as a function of $n$ while having the running time of $\Theta{(n\log_2{n})}$. The largest value of $k$ which satisfies $k(n) \in \Theta{(\log_2{n})}$.

### d.
Choose $k$ where the time for executing insertion sort on the array with length $k$ is faster than executing merge sort on the same array.