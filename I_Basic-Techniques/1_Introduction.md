## INTRODUCTION

Competitive programming:
  1. the design of algorithms
  2. the implementation of algorithms

### Design of algorithms (problem solving + mathematical thinking)
Skills for analyzing problems and solving them creatively
Algorithm for solving a problem has to be both correct and efficient, and the core of the problem is often about inventing an efficient algorithm

### Implementation of algorithms
Good programming skills
Solutions are graded by testing an implemented algorithm using a set of test cases
Idea of the algorithm is correct AND implementation has to be correct


## PROGRAMMING LANGUAGES

Most popular programming languages used in contests are C++, Python, and Java
C++ code template for competitive programming

```
#include <bits/stdc++.h>
using namespace std;
int main() {
  // solution comes here
}
```


## INPUT & OUTPUT
In most contests, standard streams are used for reading input and writing output.
The input for the program usually consists of numbers and strings that are separated with spaces and newlines.


## WORKING WITH NUMBERS

### Integers
Most used integer type in competitive programming is `int` (32-bit type)
64-bit type `long long`

### Modular arithmetic
modulo _m_ is the remainder when the answer is divided by _m_

Usually we want the remainder to always be between `0`...`m − 1`. However, in
C++ and other languages, the remainder of a negative number is either zero or
negative.

An easy way to make sure there are no negative remainders is to first
calculate the remainder as usual and then add `m` if the result is negative:
```
x = x%m;
if (x < 0) x += m;
```
However, this is only needed when there are subtractions in the code and the
remainder may become negative.

### Floating point numbers
Floating point types in competitive programming:
64-bit `double`
80-bit `long double` (as an extension in the g++ compiler)

In most cases, `double` is enough, but `long double` is more accurate.
It's risky to compare floating point numbers with the `==` operator, because it
is possible that the values should be equal but they are not because of precision
errors. A better way to compare floating point numbers is to assume that two
numbers are equal if the difference between them is less than `ε`, where `ε` is a
small number.
> Note that while floating point numbers are inaccurate, integers up to a certain
limit can still be represented accurately.


## SHORTENING CODE
Type names
Macros


## MATHEMATICS

### Sum formulas
_Arithmetic progression_ is a sequence of numbers where the difference between any two consecutive numbers is constant. For example, `3, 7, 11, 15`.
_Geometric progression_ is a sequence of numbers where the ratio between two consecutive numbers is constant. For example, `3, 6, 12, 24`.
_Harmonic sum_ is a sum of all positive unit fractions.

### Set theory
_Set_ is a collection of elements For example,
> _X_ = {2, 4, 7}
This set contains elements `2, 4, 7`

### Logic
The value of a logical expression is either __true__ (1) or __false__ (0)
Logical operators:
- negation
- conjuction
- disjunction
- implication
- equivalence

_Predicate_ is an expression that is true or false depending on parameters.
_Quantifier_ connects a logical expression to the elements of a set

### Functions
- factorial `n!`
- Fibonacci numbers (recursively) / Binet's formula

### Logarithms
- log of x
- natural logarithm