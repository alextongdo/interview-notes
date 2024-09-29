# Data Structures & Algorithms

## Runtime Trick
Given the constraint for the length of the input $n$, we can make an educated guess about the necessary runtime complexity.
| Length of Input  | Runtime |
| ------------- | ------------- |
| $0\leq n\leq11$  | $O(n!),~O(n^6)$  |
| $12\leq n\leq18$ | $O(2^n\times n^2)$  |
| $19\leq n\leq22$ | $O(2^n\times n)$ |
| $23\leq n\leq100$ | $O(n^4)$ |
| $150\leq n\leq400$ | $O(n^3)$ |
| $500\leq n\leq2000$ | $O(n^2\times \log N)$ |
| $2500\leq n\leq10000$ | $O(n^2)$ |
| $15000\leq n\leq1 \text{M}$ | $O(n\times \log N)$ |
| $1.5\text{M}\leq n\leq100 \text{M}$ | $O(n),~O(\log n),~O(1)$ |