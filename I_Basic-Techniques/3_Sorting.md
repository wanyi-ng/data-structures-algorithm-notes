## SORTING
__Sorting__ is a fundamental algorithm design problem. Many efficient algorithms use sorting as a subroutine because it is often easier to process data if the elements are in a sorted order.

For example, the problem ”does an array contain two equal elements?” is easy to solve using sorting. If the array contains two equal elements, they will be next to each other after sorting, so it is easy to find them. Also, the problem ”what is the most frequent element in an array?” can be solved similarly.

> The efficient general sorting algorithms work in `O(n log n)` time, and many algorithms that use sorting as a
subroutine also have this time complexity.

### Sorting theory
The basic sorting problem looks like this:

`Given an array that contains n elements, your task is to sort the elements in increasing order.`

For example, the array
```
| 1 | 3 | 8 | 2 | 9 | 2 | 5 | 6 |    =>    | 1 | 2 | 2 | 3 | 5 | 6 | 8 | 9 |
```

### `O(n^2)` algorithms
Simple algorithms for sorting an array are in `O(n^2)` time; they are short and usually consist of two nested loops. A famous sorting algorithm with `O(n^2)` time complexity is __bubble sort__ where the elements "bubble" in the array according to their values.

__Bubble sort__ consists of `n` rounds. On each round, the algorithm iterates through the elements of the array. Whenever two consecutive elements are found that are not in correct order, the algorithm swaps them.

```
for (int i = 0; i < n; i++) {
  for (int j = 0; j < n-1; j++) {
    if (array[j] > array[j+1]) {
      swap(array[j],array[j+1]);
    }
  }
}
```

After the first round of the algorithm, the largest element will be in the correct position, and in general, after `k` rounds, the `k` largest elements will be in the correct positions. Thus, after `n` rounds, the whole array will be sorted.
For example, in the array
```
| 1 | 3 | 8 | 2 | 9 | 2 | 5 | 6
```
the first round of bubble sort swaps elements as follows:
```
| 1 | 3 | 2 | 8 | 9 | 2 | 5 | 6
| 1 | 3 | 2 | 8 | 2 | 9 | 5 | 6
| 1 | 3 | 2 | 8 | 2 | 5 | 9 | 6
| 1 | 3 | 2 | 8 | 2 | 5 | 6 | 9
```

### Inversions
Bubble sort is an example of a sorting algorithm that always swaps _consecutive_ elements in the array. It turns out that the time complexity of such an algorithm is _always_ at least `O(n^2)`, because in the worst case, `O(n^2)`, swaps are required for sorting the array.

A useful concept when analyzing sorting algorithms is an __inversion__: a pair of array elements (array[a], array[b]) such that a < b and array[a] > array[b], i.e., the elements are in the wrong order

### `O(n log n)` algorithms
__Merge sort__ is a recursion based sorting algorithm. It halves the size of the subarray at each step. The recursion consists of `O(log n)` levels, and processing each level takes `O(n)` time. Merging the subarrays `array[a...k]` and `array[k + 1...b]` is possible in linear time, because they are already sorted.

```
| 1 | 3 | 6 | 2 | 8 | 2 | 5 | 9 |
```
The array will be divided into two subarrays as follows:
```
| 1 | 3 | 6 | 2 | 8 | 2 | 5 | 9 |
```
Then, the subarrays will be sorted recursively as follows:
```
| 1 | 2 | 3 | 6 | 2 | 5 | 8 | 9 |
```
Finally, the algorithm merges the sorted subarrays and creates the final
sorted array:
```
| 1 | 2 | 2 | 3 | 5 | 6 | 8 | 9 |
```

### Sorting lower bound
The lower bound for the time complexity can be proved by considering sorting as a process where each comparison of two elements gives more information about the contents of the array.

### Counting sort
The lower bound `n log n` does not apply to algorithms that do not compare array elements but use some other information. An example of such an algorithm is __counting sort__ that sorts an array in `O(n)` time assuming that every element in the array is an integer between `0...c` and `c = O(n)`.

The algorithm creates a _bookkeeping_ array, whose indices are elements of the original array.The algorithm iterates through the original array and calculates how many times each element appears in the array.

For example, the array
1 3 6 9 9 3 5 9
corresponds to the following bookkeeping array:
1 0 2 0 1 1 0 0 3

For example, the value at position 3 in the bookkeeping array is 2, because the element 3 appears 2 times in the original array.

Construction of the bookkeeping array takes `O(n)` time. After this, the sorted array can be created in `O(n)` time because the number of occurrences of each element can be retrieved from the bookkeeping array. Thus, the total time complexity of counting sort is `O(n)`.
Counting sort is a very efficient algorithm but it can only be used when the constant c is small enough, so that the array elements can be used as indices in the bookkeeping array


## Sorting in C++
For example, the C++ standard library contains the function `sort` that can be easily used for sorting arrays and other data structures.

### Comparison operators
__Comparison operator__ is defined for the data type of the elements to be sorted. When sorting, this operator will be used whenever it is necessary to find out the order of the two elements.

Most C++ data types have a built-in comparison operator, and elements of those types can be sorted automatically. For example, numbers are sorted according to their values and strings are sorted in alphabetical order. 

Pairs (`pair`) are sorted primarily according to their first elements (`first`). However, if the first elements of two pairs are equal, they are sorted according to their second elements (second):
```
vector<pair<int,int>> v;
v.push_back({1,5});
v.push_back({2,3});
v.push_back({1,2});
sort(v.begin(), v.end());
```
After this, the order of the pairs is `(1, 2)`, `(1, 5)` and `(2, 3)`. In a similar way, tuples (`tuple`) are sorted primarily by the first element, secondarily by the second element, etc.2:
```
vector<tuple<int,int,int>> v;
v.push_back({2,1,4});
v.push_back({1,5,3});
v.push_back({2,1,3});
sort(v.begin(), v.end());
```
After this, the order of the tuples is `(1, 5, 3)`, `(2, 1, 3)` and `(2, 1, 4)`.
