# Unit-II: Sorting Algorithms

## Detailed Notes for Exam Preparation

-----

## 1. INTRODUCTION TO SORTING

### 1.1 What is Sorting?

**Sorting** is the process of arranging elements in a particular order (ascending or descending) according to some criteria.

**Types of Sorting:**

- **Internal Sorting**: All data fits in main memory
- **External Sorting**: Data too large for main memory, uses external storage
- **Stable Sorting**: Maintains relative order of equal elements
- **In-place Sorting**: Uses O(1) extra memory space

-----

## 2. BASIC SORTING ALGORITHMS

### 2.1 Bubble Sort

**Concept**: Repeatedly compare adjacent elements and swap if they are in wrong order.

**Algorithm:**

```
BubbleSort(A[1...n])
1. for i = 1 to n-1 do
2.    for j = 1 to n-i do
3.       if A[j] > A[j+1] then
4.          swap(A[j], A[j+1])
```

**Optimized Version:**

```
OptimizedBubbleSort(A[1...n])
1. for i = 1 to n-1 do
2.    swapped = false
3.    for j = 1 to n-i do
4.       if A[j] > A[j+1] then
5.          swap(A[j], A[j+1])
6.          swapped = true
7.    if swapped = false then break
```

**Analysis:**

- **Best Case**: O(n) - when array is already sorted (optimized version)
- **Worst Case**: O(n²) - when array is reverse sorted
- **Average Case**: O(n²)
- **Space Complexity**: O(1)
- **Stable**: Yes
- **In-place**: Yes

**Number of Comparisons**: n(n-1)/2 in worst case
**Number of Swaps**: n(n-1)/2 in worst case

### 2.2 Selection Sort

**Concept**: Find minimum element and place it at the beginning, repeat for remaining array.

**Algorithm:**

```
SelectionSort(A[1...n])
1. for i = 1 to n-1 do
2.    min_idx = i
3.    for j = i+1 to n do
4.       if A[j] < A[min_idx] then
5.          min_idx = j
6.    swap(A[i], A[min_idx])
```

**Analysis:**

- **Best Case**: O(n²) - always performs same number of comparisons
- **Worst Case**: O(n²)
- **Average Case**: O(n²)
- **Space Complexity**: O(1)
- **Stable**: No (can be made stable with modifications)
- **In-place**: Yes

**Number of Comparisons**: n(n-1)/2 always
**Number of Swaps**: n-1 always

### 2.3 Insertion Sort

**Concept**: Build sorted array one element at a time by inserting each element in its correct position.

**Algorithm:**

```
InsertionSort(A[1...n])
1. for i = 2 to n do
2.    key = A[i]
3.    j = i - 1
4.    while j ≥ 1 and A[j] > key do
5.       A[j+1] = A[j]
6.       j = j - 1
7.    A[j+1] = key
```

**Analysis:**

- **Best Case**: O(n) - when array is already sorted
- **Worst Case**: O(n²) - when array is reverse sorted
- **Average Case**: O(n²)
- **Space Complexity**: O(1)
- **Stable**: Yes
- **In-place**: Yes

**Applications**: Best for small arrays, nearly sorted arrays, online algorithms

-----

## 3. ADVANCED SORTING ALGORITHMS

### 3.1 Quick Sort

**Concept**: Divide-and-conquer algorithm that partitions array around a pivot element.

**Algorithm:**

```
QuickSort(A[1...n], low, high)
1. if low < high then
2.    pi = Partition(A, low, high)
3.    QuickSort(A, low, pi-1)
4.    QuickSort(A, pi+1, high)

Partition(A[1...n], low, high)
1. pivot = A[high]
2. i = low - 1
3. for j = low to high-1 do
4.    if A[j] ≤ pivot then
5.       i = i + 1
6.       swap(A[i], A[j])
7. swap(A[i+1], A[high])
8. return i + 1
```

**Analysis:**

- **Best Case**: O(n log n) - when pivot divides array into equal halves
- **Worst Case**: O(n²) - when pivot is always smallest or largest element
- **Average Case**: O(n log n)
- **Space Complexity**: O(log n) - recursion stack
- **Stable**: No
- **In-place**: Yes

**Recurrence Relations:**

- **Best/Average**: T(n) = 2T(n/2) + O(n) = O(n log n)
- **Worst**: T(n) = T(n-1) + O(n) = O(n²)

**Pivot Selection Strategies:**

1. **First Element**: Simple but poor for sorted arrays
1. **Last Element**: Most common implementation
1. **Random Element**: Better average performance
1. **Median-of-Three**: Choose median of first, middle, last

### 3.2 Randomized Quick Sort

**Concept**: Choose pivot randomly to avoid worst-case scenario consistently.

**Algorithm:**

```
RandomizedQuickSort(A[1...n], low, high)
1. if low < high then
2.    random_idx = Random(low, high)
3.    swap(A[random_idx], A[high])
4.    pi = Partition(A, low, high)
5.    RandomizedQuickSort(A, low, pi-1)
6.    RandomizedQuickSort(A, pi+1, high)
```

**Analysis:**

- **Expected Time**: O(n log n)
- **Worst Case**: O(n²) but probability is very low
- **Space Complexity**: O(log n)

### 3.3 Merge Sort

**Concept**: Divide array into halves, recursively sort them, then merge sorted halves.

**Algorithm:**

```
MergeSort(A[1...n], low, high)
1. if low < high then
2.    mid = (low + high) / 2
3.    MergeSort(A, low, mid)
4.    MergeSort(A, mid+1, high)
5.    Merge(A, low, mid, high)

Merge(A[1...n], low, mid, high)
1. Create temporary arrays L[1...mid-low+1] and R[1...high-mid]
2. Copy A[low...mid] to L and A[mid+1...high] to R
3. i = 1, j = 1, k = low
4. while i ≤ |L| and j ≤ |R| do
5.    if L[i] ≤ R[j] then
6.       A[k] = L[i], i++
7.    else A[k] = R[j], j++
8.    k++
9. Copy remaining elements of L and R to A
```

**Analysis:**

- **Best Case**: O(n log n)
- **Worst Case**: O(n log n)
- **Average Case**: O(n log n)
- **Space Complexity**: O(n) - for temporary arrays
- **Stable**: Yes
- **In-place**: No

**Recurrence Relation**: T(n) = 2T(n/2) + O(n) = O(n log n)

### 3.4 Heap Sort

**Concept**: Build max heap, repeatedly extract maximum element and place at end.

**Key Operations:**

- **Heapify**: Maintain heap property
- **Build-Max-Heap**: Convert array to max heap
- **Extract-Max**: Remove and return maximum element

**Algorithm:**

```
HeapSort(A[1...n])
1. BuildMaxHeap(A)
2. for i = n downto 2 do
3.    swap(A[1], A[i])
4.    heap_size = heap_size - 1
5.    MaxHeapify(A, 1)

MaxHeapify(A, i)
1. left = 2*i, right = 2*i + 1
2. largest = i
3. if left ≤ heap_size and A[left] > A[largest] then
4.    largest = left
5. if right ≤ heap_size and A[right] > A[largest] then
6.    largest = right
7. if largest ≠ i then
8.    swap(A[i], A[largest])
9.    MaxHeapify(A, largest)

BuildMaxHeap(A[1...n])
1. heap_size = n
2. for i = n/2 downto 1 do
3.    MaxHeapify(A, i)
```

**Analysis:**

- **Best Case**: O(n log n)
- **Worst Case**: O(n log n)
- **Average Case**: O(n log n)
- **Space Complexity**: O(1)
- **Stable**: No
- **In-place**: Yes

-----

## 4. COUNTING SORT

### 4.1 Counting Sort

**Concept**: Non-comparison based sorting for integers with limited range.

**Prerequisites**:

- Elements are integers
- Range of elements is known and small

**Algorithm:**

```
CountingSort(A[1...n], k) // k is maximum value
1. Create count array C[0...k] initialized to 0
2. for i = 1 to n do
3.    C[A[i]] = C[A[i]] + 1
4. for i = 1 to k do
5.    C[i] = C[i] + C[i-1]
6. Create output array B[1...n]
7. for i = n downto 1 do
8.    B[C[A[i]]] = A[i]
9.    C[A[i]] = C[A[i]] - 1
10. Copy B to A
```

**Analysis:**

- **Time Complexity**: O(n + k) where k is range of input
- **Space Complexity**: O(k)
- **Stable**: Yes
- **In-place**: No

**Applications**: When range is small, digital sorting algorithms

-----

## 5. EXTERNAL SORTING

### 5.1 External Sorting Concepts

**Need**: When data is too large to fit in main memory.

**Approach**:

1. Divide data into chunks that fit in memory
1. Sort each chunk internally
1. Merge sorted chunks using external merge

**Multi-way Merge Sort**:

- Divide file into sorted runs
- Merge multiple runs simultaneously
- Use priority queue for efficient merging

**Performance Factors**:

- **I/O Cost**: Dominant factor in external sorting
- **Number of Passes**: Minimize disk accesses
- **Buffer Management**: Efficient use of available memory

-----

## 6. RADIX SORT AND BUCKET SORT

### 6.1 Radix Sort

**Concept**: Sort numbers digit by digit using stable sorting (usually counting sort).

**Algorithm (LSD - Least Significant Digit):**

```
RadixSort(A[1...n], d) // d is number of digits
1. for i = 1 to d do
2.    CountingSortByDigit(A, i)
```

**Analysis:**

- **Time Complexity**: O(d(n + k)) where d is digits, k is range of each digit
- **Space Complexity**: O(n + k)
- **Stable**: Yes

### 6.2 Bucket Sort

**Concept**: Distribute elements into buckets, sort each bucket, then concatenate.

**Algorithm:**

```
BucketSort(A[1...n])
1. Create n empty buckets
2. for i = 1 to n do
3.    insert A[i] into bucket[⌊n*A[i]⌋]
4. for i = 0 to n-1 do
5.    sort bucket[i] using insertion sort
6. concatenate buckets in order
```

**Analysis:**

- **Average Case**: O(n + k) where k is number of buckets
- **Worst Case**: O(n²) when all elements go to same bucket
- **Space Complexity**: O(n + k)

-----

## 7. COMPARISON AND CLASSIFICATION

### 7.1 Sorting Algorithm Classification

#### 7.1.1 Online vs Stable Sort

- **Online Sort**: Can process input as it arrives (Insertion Sort)
- **Stable Sort**: Maintains relative order of equal elements (Merge Sort, Insertion Sort, Bubble Sort)

#### 7.1.2 In-place vs Out-of-place Sort

- **In-place**: Uses O(1) extra space (Quick Sort, Heap Sort, Selection Sort)
- **Out-of-place**: Uses O(n) extra space (Merge Sort, Counting Sort)

### 7.2 Recursive vs Iterative Nature

**Recursive Sorts:**

- Quick Sort: T(n) = T(k) + T(n-k-1) + O(n)
- Merge Sort: T(n) = 2T(n/2) + O(n)
- Heap Sort: Uses recursion in heapify

**Iterative Sorts:**

- Bubble Sort, Selection Sort, Insertion Sort
- Can be converted to iterative versions

### 7.3 Time and Space Complexity Comparison

|Algorithm     |Best Case  |Average Case|Worst Case |Space   |Stable|
|--------------|-----------|------------|-----------|--------|------|
|Bubble Sort   |O(n)       |O(n²)       |O(n²)      |O(1)    |Yes   |
|Selection Sort|O(n²)      |O(n²)       |O(n²)      |O(1)    |No    |
|Insertion Sort|O(n)       |O(n²)       |O(n²)      |O(1)    |Yes   |
|Quick Sort    |O(n log n) |O(n log n)  |O(n²)      |O(log n)|No    |
|Merge Sort    |O(n log n) |O(n log n)  |O(n log n) |O(n)    |Yes   |
|Heap Sort     |O(n log n) |O(n log n)  |O(n log n) |O(1)    |No    |
|Counting Sort |O(n + k)   |O(n + k)    |O(n + k)   |O(k)    |Yes   |
|Radix Sort    |O(d(n + k))|O(d(n + k)) |O(d(n + k))|O(n + k)|Yes   |

### 7.4 Number of Swaps and Comparisons

**Bubble Sort:**

- Comparisons: O(n²) in all cases
- Swaps: O(n²) in worst case, O(1) in best case

**Selection Sort:**

- Comparisons: O(n²) always
- Swaps: O(n) always

**Insertion Sort:**

- Comparisons: O(n) in best case, O(n²) in worst case
- Shifts: O(n²) in worst case

**Quick Sort:**

- Comparisons: O(n log n) average, O(n²) worst case
- Swaps: O(n log n) average

-----

## 8. PRACTICAL CONSIDERATIONS

### 8.1 When to Use Which Algorithm

**Small Arrays (n < 50):**

- Insertion Sort: Simple and efficient
- Selection Sort: Minimal swaps needed

**Large Arrays:**

- Quick Sort: Average case performance
- Merge Sort: Guaranteed O(n log n), stable
- Heap Sort: Guaranteed O(n log n), in-place

**Nearly Sorted Arrays:**

- Insertion Sort: O(n) performance
- Bubble Sort (optimized): Early termination

**Limited Memory:**

- Heap Sort: O(1) space
- Quick Sort: O(log n) space

**Stability Required:**

- Merge Sort: Guaranteed stable
- Insertion Sort: Stable and simple

### 8.2 Hybrid Approaches

**Introsort**: Quick Sort + Heap Sort + Insertion Sort

- Start with Quick Sort
- Switch to Heap Sort if recursion depth exceeds limit
- Use Insertion Sort for small subarrays

**Timsort**: Merge Sort + Insertion Sort

- Used in Python and Java
- Optimized for real-world data patterns

-----

## EXAM PREPARATION GUIDE

### Expected Question Types:

1. **Algorithm Implementation**
- Write complete pseudocode (4-5 marks)
- Trace algorithm execution step by step (3-4 marks)
1. **Complexity Analysis**
- Calculate time/space complexity (3-4 marks)
- Compare different sorting algorithms (2-3 marks)
1. **Problem Solving**
- Choose best algorithm for given constraints (2-3 marks)
- Modify algorithms for specific requirements (3-4 marks)

### Key Points to Remember:

1. **Quick Sort Partitioning**: Understand how pivot selection affects performance
1. **Merge Sort Merging**: Know the merge process in detail
1. **Heap Operations**: Heapify, Build-Heap, Extract-Max
1. **Stability**: Which algorithms preserve relative order
1. **Space Complexity**: In-place vs out-of-place algorithms

### Practice Problems:

1. Trace Quick Sort with different pivot selection strategies
1. Show merge process in Merge Sort step by step
1. Build max heap and perform heap sort
1. Compare sorting algorithms for different input patterns
1. Calculate exact number of comparisons and swaps for small examples

### Common Exam Questions:

1. “Compare Quick Sort and Merge Sort in terms of time complexity, space complexity, and stability.”
1. “Trace the execution of [algorithm] on array [1,3,2,5,4]”
1. “Which sorting algorithm would you choose for [specific scenario]? Justify.”
1. “Derive the recurrence relation for [divide-and-conquer algorithm]”
1. “Explain why Quick Sort has O(n²) worst case but O(n log n) average case.”
