_Time complexity_ of an algorithm estimates how much time the algorithm will use for some input. The idea is to represent the efficiency as a function whose parameter is the size of the input.

By calculating the time complexity, we can find out whether the algorithm is fast enough without implementing it.

## CALCULATION RULES
Time complexity of an algorithm is denoted `O(...)` where the three dots represent some function. 

Usually, the variable _n_ denotes the input size.

For example, if the input is an array of numbers, _n_ will be the size of the array, and if the input is a string, _n_ will be the length of the string.

### Loops
Common reason why algorithm is slow is that it contains many loops that go through the input.

The more nested loops an algorithm contains, the slower it is.

If there are _k_ nested loops, the time complexity is _O(n^k)_

```
// Time complexity for this loop is O(n)
for (int i = 1; i <= n; i++) {
  // code
}
```
```
// Time complexity for this loop is O(n^2)
for (int i = 1; i <= n; i++) {
  for (int j = 1; j <= n; j++) {
  // code
  }
}
```

### Order of magnitude
Time complexity only shows the order of magnitude, not the exact number of times the code inside a loop is executed

```
for (int i = 1; i <= 3*n; i++) {
  // code
}
```
```
for (int i = 1; i <= n+5; i++) {
  // code
}
```
```
for (int i = 1; i <= n; i += 2) {
  // code
}
```

### Phases
If the algorithm consists of consecutive phases, the total time complexity is the largest time complexity of a single phase. The reason is that the slowest phase is often the bottleneck of the code.

For example, the following code consists of three phases with time complexities `O(n)`, `O(n^2)` and `O(n)`. Thus, the total time complexity is `O(n^2)`.

```
for (int i = 1; i <= n; i++) {
  // code
}
for (int i = 1; i <= n; i++) {
  for (int j = 1; j <= n; j++) {
    // code
  }
}
for (int i = 1; i <= n; i++) {
  // code
}
```

### Several variables
Sometimes the time complexity depends on several factors.

In this case, the time complexity formula contains several variables.
For example, the time complexity of the following code is O(nm):

```
for (int i = 1; i <= n; i++) {
  for (int j = 1; j <= m; j++) {
    // code
  }
}
```

### Recursion
The time complexity of a recusive function depends on the number of times the function is called and the time complexity of a single call. The total time complexity is the product of these values.

```
void f(int n) {
  if (n == 1) return;
  f(n-1);
}
```
The call `f(n)` causes n function calls, and the time complexity of each call is `O(1)`.
Thus, the total time complexity is `O(n)`.
As another example, consider the following function:

```
void g(int n) {
  if (n == 1) return;
  g(n-1);
  g(n-1);
}
```


## COMPLEXITY CLASSES

`O(1)` The running time of a __constant-time__ algorithm does not depend on the input size. A typical constant-time algorithm is a direct formula that calculates the answer.

`O(log n)` A __logarithmic__ algorithm often halves the input size at each step. The running time of such an algorithm is logarithmic, because log2 n equals the number of times n must be divided by 2 to get 1.

`O(square root of n)` A __square root algorithm__ is slower than `O(log n)` but faster than `O(n)`.

`O(n)` A __linear__ algorithm goes through the input a constant number of times. This is often the best possible time complexity, because it is usually necessary to access each input element at least once before reporting the answer.

`O(n log n)` This time complexity often indicates that the algorithm sorts the input, because the time complexity of efficient sorting algorithms is `O(n log n)`. Another possibility is that the algorithm uses a data structure where each operation takes `O(log n)` time.

`O(n^2)` A __quadratic__ algorithm often contains two nested loops. It is possible to go through all pairs of the input elements in `O(n2)` time.

`O(n3)` A __cubic__ algorithm often contains three nested loops. It is possible to go through all triplets of the input elements in `O(n^3)` time.

`O(2n)` This time complexity often indicates that the algorithm iterates through all subsets of the input elements. For example, the subsets of {1, 2, 3} are ;, {1}, {2}, {3}, {1, 2}, {1, 3}, {2, 3} and {1, 2, 3}.

`O(n!)` This time complexity often indicates that the algorithm iterates through all permutations of the input elements. For example, the permutations of {1, 2, 3} are (1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2) and (3, 2, 1).

An algorithm is __polynomial__ if its time complexity is at most `O(n^k)` where _k_ is a constant. All the above time complexities except `O(2^n)` and `O(n!)` are polynomial.
In practice, the constant `k` is usually small, and therefore a polynomial time complexity roughly means that the algorithm is _efficient_.
Most algorithms in this book are polynomial. Still, there are many important problems for which no polynomial algorithm is known, i.e., nobody knows how to solve them efficiently. __NP-hard__ problems are an important set of problems, for which no polynomial algorithm is known.


## ESTIMATING EFFICIENCY
The time complexity of an algorithm can typically be calculated before implementing it to check if it is efficient enough for the problem.
input size | required time complexity
n ≤ 10     | O(n!)
n ≤ 20     | O(2n)
n ≤ 500    | O(n3)
n ≤ 5000   | O(n2)
n ≤ 106.   | O(n log n) or O(n)
n is large | O(1) or O(log n)


## MAXIMUM SUBARRAY SUM
The maximum sum subarray problem, aka the maximum segment sum problem, is the task of finding a contiguous subarray with the largest sum, within a given one-dimensional array `A[1...n]` of numbers. It can be solved in `O(n)` time and `O(1)` space.

For example, in the array

```
-1 | 2 | 4 | -3 | 5 | 2 | -5 | 2
```
This subarray produces the maximum sum 10:
```
-1 | 2 | 4 | -3 | 5 | 2 | -5 | 2
   |--------------------|
```
> Assuming an empty subarray is allowed, the maximum subarray sum is always at least 0

### Algorithm 1
The straightforward way to solve the problem is to go through all possible subarrays, calculate the sum of the values in each subarray and maintain the maximum sum.
```
int best = 0;
for (int a = 0; a < n; a++) {
  for (int b = a; b < n; b++) {
    int sum = 0;
    for (int k = a; k <= b; k++) {
      sum += array[k];
    }
    best = max(best,sum);
  }
}
cout << best << "\n";
```
Variables `a` and `b` fix the first and last index of the subarray, and the sum of the values is calculated to variable `sum`.

Variable `best` contains the maximum sum found during the search.

The time complexity of the algorithm is `O(n^3)` because it consists of three nested loops that go through the input.

### Algorithm 2
By removing one loop from __Algorithm 1__ it makes it more efficient. This is possible by calculating the sum at the same time when the right end of the subarray moves. Thus, making the time complexity `O(n^2)`
```
int best = 0;
for (int a = 0; a < n; a++) {
  int sum = 0;
  for (int b = a; b < n; b++) {
    sum += array[b];
    best = max(best,sum);
  }
}
cout << best << "\n";
```

### Algorithm 3
It is possible to solve the problem in `O(n)` time by using just one loop.

The idea is to calculate, for each array position, the maximum sum of a subarray that ends at that position. As a result, the answer for the problem is the maximum of those sums.

Consider the subproblem of finding the maximum-sum subarray that ends at
position k. There are two possibilities:
1. The subarray only contains the element at position `k`.
2. The subarray consists of a subarray that ends at position `k − 1`, followed by
the element at position `k`.

In the latter case, since we want to find a subarray with maximum sum, the
subarray that ends at position `k − 1` should also have the maximum sum. Thus,
we can solve the problem efficiently by calculating the maximum subarray sum
for each ending position from left to right.
```
int best = 0, sum = 0;
for (int k = 0; k < n; k++) {
  sum = max(array[k],sum+array[k]);
  best = max(best,sum);
}
cout << best << "\n";
```
The algorithm only contains one loop that goes through the input, making the time complexity `O(n)`. This is also the best possible time complexity, because any algorithm for the problem has to examine all array elements at least once.

### Efficiency comparison
All algorithms are efficient when the input size is small, but larger inputs bring out remarkable differences in the running times of the algorithms.

__Algorithm 1__ becomes slow when `n = 10^4`, and __Algorithm 2__
becomes slow when `n = 10^5`. Only __Algorithm 3__ is able to process even the largest
inputs instantly.