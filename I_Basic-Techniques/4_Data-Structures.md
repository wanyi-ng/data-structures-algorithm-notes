## DATA STRUCTURES

A __data structure__ is a way to store data in the memory of a computer. It is important to choose an appropriate data structure for a problem, because each data structure has its own advantages and disadvantages.

### Dynamic arrays
__Dynamic array__ is an array whose size can be changed during execution of the program. The most popular dynamic array in C++ is the `vector` structure, which can be used almost like an ordinary array.

The following code creates an empty vector and adds three elements to it:
```
vector<int> v;
v.push_back(3); // [3]
v.push_back(2); // [3,2]
v.push_back(5); // [3,2,5]
```
After this, the elements can be accessed like in an ordinary array:
```
cout << v[0] << "\n"; // 3
cout << v[1] << "\n"; // 2
cout << v[2] << "\n"; // 5
```
The function size returns the number of elements in the vector. The following code iterates through the vector and prints all elements in it:
```
for (int i = 0; i < v.size(); i++) {
  cout << v[i] << "\n";
}
```
A shorter way to iterate through a vector is as follows:
```
for (auto x : v) {
  cout << x << "\n";
}
```
The function back returns the last element in the vector, and the function pop_back removes the last element:
```
vector<int> v;
v.push_back(5);
v.push_back(2);
cout << v.back() << "\n"; // 2
v.pop_back();
cout << v.back() << "\n"; // 5
```
The following code creates a vector with five elements:
```
vector<int> v = {2,4,2,5,1};
```
Another way to create a vector is to give the number of elements and the initial value for each element:
```
// size 10, initial value 0
vector<int> v(10);
// size 10, initial value 5
vector<int> v(10, 5);
```

The internal implementation of a vector uses an ordinary array. If the size of the vector increases and the array becomes too small, a new array is allocated and all the elements are moved to the new array. However, this does not happen often and the average time complexity of `push_back` is `O(1)`.
The string structure is also a dynamic array that can be used almost like a vector. In addition, there is special syntax for strings that is not available in other data structures. Strings can be combined using the `+` symbol. The function `substr(k, x)` returns the substring that begins at position `k` and has length `x`, and the function `find(t)` finds the position of the first occurrence of a substring `t`.
The following code presents some string operations:
```
string a = "hatti";
string b = a+a;
cout << b << "\n"; // hattihatti
b[5] = ’v’;
cout << b << "\n"; // hattivatti
string c = b.substr(3,4);
cout << c << "\n"; // tiva
```


## SET STRUCTURES

A __set__ is a data structure that maintains a collection of elements. The basic
operations of sets are element insertion, search and removal.

The C++ standard library contains two set implementations: The structure set is based on a balanced binary tree and its operations work in `O(log n)` time.

The structure `unordered_set` uses hashing, and its operations work in `O(1)` time
on average.

The benefit of the `set` structure is that it maintains the order of the elements and
provides functions that are not available in `unordered_set`. On the other hand,
`unordered_set` can be more efficient.

The following code creates a set that contains integers, and shows some of the operations. The function `insert` adds an element to the set, the function `count` returns the number of occurrences of an element in the set, and the function `erase` removes an element from the set.

```
set<int> s;
s.insert(3);
s.insert(2);
s.insert(5);
cout << s.count(3) << "\n"; // 1
cout << s.count(4) << "\n"; // 0
s.erase(3);
s.insert(4);
cout << s.count(3) << "\n"; // 0
cout << s.count(4) << "\n"; // 1
```

A set can be used mostly like a vector, but it is not possible to access the elements using the `[]` notation. The following code creates a set, prints the number of elements in it, and then iterates through all the elements:
```
set<int> s = {2,5,6,8};
cout << s.size() << "\n"; // 4
for (auto x : s) {
  cout << x << "\n";
}
```

An important property of sets is that all their elements are distinct. Thus, the function count always returns either 0 (the element is not in the set) or 1 (the element is in the set), and the function insert never adds an element to the set if it is already there. The following code illustrates this:
```
set<int> s;
s.insert(5);
s.insert(5);
s.insert(5);
cout << s.count(5) << "\n"; // 1
```

C++ also contains the structures multiset and `unordered_multiset` that otherwise work like set and `unordered_set` but they can contain multiple instances of an element. 

For example, in the following code all three instances of the number 5 are added to a multiset:
```
multiset<int> s;
s.insert(5);
s.insert(5);
s.insert(5);
cout << s.count(5) << "\n"; // 3
```

The function erase removes all instances of an element from a multiset:
```
s.erase(5);
cout << s.count(5) << "\n"; // 0
Often, only one instance should be removed, which can be done as follows:
s.erase(s.find(5));
cout << s.count(5) << "\n"; // 2
```

