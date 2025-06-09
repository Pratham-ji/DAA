# Unit-I: Introduction to Algorithms & Searching

## 1. INTRODUCTION TO ALGORITHMS

### 1.1 What is an Algorithm?

An **algorithm** is a finite sequence of well-defined, unambiguous instructions for solving a computational problem or performing a task.

**Key Characteristics:**

- **Finiteness**: Must terminate after finite number of steps
- **Definiteness**: Each step must be precisely defined
- **Input**: Zero or more inputs
- **Output**: One or more outputs
- **Effectiveness**: Operations must be basic enough to be carried out exactly

**Algorithm vs Program:**

- Algorithm: Abstract step-by-step procedure
- Program: Implementation of algorithm in specific programming language

**Example Algorithm (Finding Maximum):**

```
Algorithm: FindMax(A[1...n])
1. max = A[1]
2. for i = 2 to n do
3.    if A[i] > max then
4.       max = A[i]
5. return max
```

### 1.2 Rate of Growth & Commonly Used Growth Rates

**Rate of Growth** refers to how the running time of an algorithm increases with input size.

**Common Growth Rates (Best to Worst):**

1. **Constant - O(1)**
- Time remains same regardless of input size
- Example: Array access, basic arithmetic
1. **Logarithmic - O(log n)**
- Time increases logarithmically
- Example: Binary search, balanced tree operations
1. **Linear - O(n)**
- Time increases linearly with input
- Example: Linear search, single loop
1. **Linearithmic - O(n log n)**
- Combination of linear and logarithmic
- Example: Merge sort, heap sort
1. **Quadratic - O(n²)**
- Time proportional to square of input
- Example: Bubble sort, nested loops
1. **Cubic - O(n³)**
- Time proportional to cube of input
- Example: Matrix multiplication
1. **Exponential - O(2ⁿ)**
- Time doubles with each additional input
- Example: Tower of Hanoi, subset generation
1. **Factorial - O(n!)**
- Extremely slow growth
- Example: Traveling salesman (brute force)

### 1.3 Types of Analysis

#### 1.3.1 Best Case Analysis (Ω - Omega)

- **Definition**: Minimum time required for algorithm execution
- **Represents**: Most favorable input condition
- **Example**: In linear search, best case is when element is found at first position - O(1)

#### 1.3.2 Average Case Analysis (Θ - Theta)

- **Definition**: Expected time for random input
- **Calculation**: Average of all possible inputs
- **Example**: In linear search, on average element found at middle - O(n/2) = O(n)

#### 1.3.3 Worst Case Analysis (O - Big O)

- **Definition**: Maximum time required for algorithm execution
- **Most Important**: Usually considered for algorithm comparison
- **Example**: In linear search, worst case when element not found - O(n)

### 1.4 Asymptotic Notations

#### 1.4.1 Big O Notation (O)

- **Upper Bound**: f(n) = O(g(n)) if there exist positive constants c and n₀ such that f(n) ≤ c·g(n) for all n ≥ n₀
- **Meaning**: Algorithm will not perform worse than this bound

#### 1.4.2 Big Omega Notation (Ω)

- **Lower Bound**: f(n) = Ω(g(n)) if there exist positive constants c and n₀ such that f(n) ≥ c·g(n) for all n ≥ n₀
- **Meaning**: Algorithm will not perform better than this bound

#### 1.4.3 Big Theta Notation (Θ)

- **Tight Bound**: f(n) = Θ(g(n)) if f(n) = O(g(n)) and f(n) = Ω(g(n))
- **Meaning**: Algorithm’s exact growth rate

**Properties of Asymptotic Notations:**

- **Reflexive**: f(n) = O(f(n))
- **Transitive**: If f(n) = O(g(n)) and g(n) = O(h(n)), then f(n) = O(h(n))
- **Symmetric**: f(n) = Θ(g(n)) if and only if g(n) = Θ(f(n))

### 1.5 Master Theorem

**Purpose**: Provides direct method to solve recurrence relations of divide-and-conquer algorithms.

**Form**: T(n) = aT(n/b) + f(n)
where a ≥ 1, b > 1, and f(n) is asymptotically positive

**Three Cases:**

1. **Case 1**: If f(n) = O(n^(log_b(a-ε))) for some ε > 0
- **Then**: T(n) = Θ(n^log_b(a))
1. **Case 2**: If f(n) = Θ(n^log_b(a))
- **Then**: T(n) = Θ(n^log_b(a) × log n)
1. **Case 3**: If f(n) = Ω(n^(log_b(a+ε))) for some ε > 0, and af(n/b) ≤ cf(n) for some c < 1
- **Then**: T(n) = Θ(f(n))

**Examples:**

- T(n) = 2T(n/2) + n → Case 2 → T(n) = Θ(n log n) (Merge Sort)
- T(n) = 4T(n/2) + n → Case 1 → T(n) = Θ(n²) (some divide-and-conquer algorithms)

-----

## 2. SEARCHING ALGORITHMS

### 2.1 Linear Search

**Concept**: Sequential search through array elements one by one.

**Algorithm:**

```
LinearSearch(A[1...n], key)
1. for i = 1 to n do
2.    if A[i] = key then
3.       return i
4. return -1
```

**Analysis:**

- **Best Case**: O(1) - element found at first position
- **Worst Case**: O(n) - element not found or at last position
- **Average Case**: O(n/2) = O(n)
- **Space Complexity**: O(1)

**Advantages:**

- Works on both sorted and unsorted arrays
- Simple implementation
- No preprocessing required

**Disadvantages:**

- Inefficient for large datasets
- Time complexity is linear

### 2.2 Binary Search

**Concept**: Divide and conquer approach for searching in sorted arrays.

**Prerequisites**: Array must be sorted

**Algorithm:**

```
BinarySearch(A[1...n], key)
1. low = 1, high = n
2. while low ≤ high do
3.    mid = (low + high) / 2
4.    if A[mid] = key then
5.       return mid
6.    else if A[mid] < key then
7.       low = mid + 1
8.    else
9.       high = mid - 1
10. return -1
```

**Analysis:**

- **Best Case**: O(1) - element found at middle
- **Worst Case**: O(log n) - element not found
- **Average Case**: O(log n)
- **Space Complexity**: O(1) for iterative, O(log n) for recursive

**Recurrence Relation**: T(n) = T(n/2) + 1 = O(log n)

**Advantages:**

- Very efficient for large sorted datasets
- Logarithmic time complexity
- Suitable for static datasets

**Disadvantages:**

- Requires sorted array
- Not suitable for linked lists
- Insertion/deletion requires array reorganization

### 2.3 Exponential Search

**Concept**: First find range where element exists, then apply binary search.

**Algorithm:**

```
ExponentialSearch(A[1...n], key)
1. if A[1] = key then return 1
2. bound = 1
3. while bound < n and A[bound] < key do
4.    bound = bound * 2
5. return BinarySearch(A[bound/2...min(bound, n)], key)
```

**Analysis:**

- **Time Complexity**: O(log i) where i is position of element
- **Best Case**: O(1)
- **Worst Case**: O(log n)
- **Space Complexity**: O(1)

**Applications:**

- When size of array is unknown
- Better than binary search when element is near beginning

### 2.4 Interpolation Search

**Concept**: Improvement over binary search for uniformly distributed sorted arrays.

**Formula**: pos = low + [(key - A[low]) / (A[high] - A[low])] × (high - low)

**Algorithm:**

```
InterpolationSearch(A[1...n], key)
1. low = 1, high = n
2. while low ≤ high and key ≥ A[low] and key ≤ A[high] do
3.    pos = low + [(key - A[low]) / (A[high] - A[low])] × (high - low)
4.    if A[pos] = key then return pos
5.    if A[pos] < key then low = pos + 1
6.    else high = pos - 1
7. return -1
```

**Analysis:**

- **Best Case**: O(1)
- **Average Case**: O(log log n) for uniformly distributed data
- **Worst Case**: O(n) for non-uniform distribution
- **Space Complexity**: O(1)

-----

## 3. RECURSIVE ALGORITHMS

### 3.1 Tower of Hanoi

**Problem**: Move n disks from source rod to destination rod using auxiliary rod, following rules:

1. Move only one disk at a time
1. Larger disk cannot be placed on smaller disk

**Algorithm:**

```
TowerOfHanoi(n, source, destination, auxiliary)
1. if n = 1 then
2.    move disk from source to destination
3. else
4.    TowerOfHanoi(n-1, source, auxiliary, destination)
5.    move disk n from source to destination  
6.    TowerOfHanoi(n-1, auxiliary, destination, source)
```

**Analysis:**

- **Recurrence**: T(n) = 2T(n-1) + 1
- **Solution**: T(n) = 2ⁿ - 1
- **Time Complexity**: O(2ⁿ)
- **Space Complexity**: O(n) due to recursion stack

**Minimum Moves Required**: 2ⁿ - 1

### 3.2 Fibonacci Sequence

**Definition**: F(n) = F(n-1) + F(n-2) where F(0) = 0, F(1) = 1

**Recursive Algorithm:**

```
Fibonacci(n)
1. if n ≤ 1 then
2.    return n
3. else
4.    return Fibonacci(n-1) + Fibonacci(n-2)
```

**Analysis:**

- **Recurrence**: T(n) = T(n-1) + T(n-2) + 1
- **Time Complexity**: O(2ⁿ) - exponential
- **Space Complexity**: O(n) - recursion stack

**Optimized Approaches:**

1. **Dynamic Programming**: O(n) time, O(n) space
1. **Iterative**: O(n) time, O(1) space
1. **Matrix Exponentiation**: O(log n) time

**Iterative Solution:**

```
FibonacciIterative(n)
1. if n ≤ 1 then return n
2. prev2 = 0, prev1 = 1
3. for i = 2 to n do
4.    current = prev1 + prev2
5.    prev2 = prev1, prev1 = current
6. return prev1
```

-----

## EXAM PREPARATION TIPS

### Expected Question Types:

1. **Algorithm Analysis Questions**
- Calculate time/space complexity
- Compare algorithms
- Best/worst/average case analysis
1. **Implementation Questions**
- Write pseudocode for searching algorithms
- Trace algorithm execution
- Modify existing algorithms
1. **Problem-Solving Questions**
- Apply Master theorem
- Solve recurrence relations
- Design efficient algorithms

### Key Formulas to Remember:

- **Master Theorem**: T(n) = aT(n/b) + f(n)
- **Binary Search**: T(n) = T(n/2) + 1 = O(log n)
- **Tower of Hanoi**: T(n) = 2T(n-1) + 1 = O(2ⁿ)
- **Fibonacci**: T(n) = T(n-1) + T(n-2) + 1 = O(2ⁿ)

### Practice Problems:

1. Implement binary search recursively and iteratively
1. Calculate complexity using Master theorem
1. Trace Tower of Hanoi for n=3
1. Compare linear vs binary search for different scenarios
1. Analyze fibonacci using different approaches
