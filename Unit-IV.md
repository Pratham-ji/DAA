# Unit IV - Algorithm Design Techniques

## Greedy Algorithms and Dynamic Programming

-----

## 1. GREEDY ALGORITHMS

### What is a Greedy Algorithm?

A greedy algorithm makes locally optimal choices at each step, hoping to find a global optimum. It never reconsiders its choices - once a decision is made, it’s final.

### Characteristics of Greedy Algorithms:

- **Local Optimization**: Makes the best choice at each step
- **Irrevocable Decisions**: Never backtracks or changes previous decisions
- **Simple Implementation**: Generally easier to implement than other techniques
- **Efficiency**: Usually have better time complexity

### Greedy Choice Property:

A globally optimal solution can be arrived at by making locally optimal (greedy) choices.

### Optimal Substructure Property:

An optimal solution to a problem contains optimal solutions to subproblems.

-----

## 2. ACTIVITY SELECTION PROBLEM

### Problem Statement:

Given n activities with their start and finish times, select the maximum number of activities that can be performed by a single person, assuming that a person can only work on a single activity at a time.

### Greedy Strategy:

Always pick the activity that finishes earliest among the remaining activities.

### Algorithm:

```
Activity-Selection(s, f, n)
1. Sort activities by finish time
2. Select first activity
3. For each remaining activity:
   - If start time ≥ finish time of last selected activity
   - Select this activity
4. Return selected activities
```

### Time Complexity: O(n log n) for sorting + O(n) for selection = O(n log n)

### Example:

Activities: A1(1,4), A2(3,5), A3(0,6), A4(5,7), A5(3,9), A6(5,9), A7(6,10), A8(8,11), A9(8,12), A10(2,14), A11(12,16)

After sorting by finish time: A1, A2, A4, A7, A8, A11
Solution: {A1, A4, A8, A11} - Maximum 4 activities can be selected.

-----

## 3. JOB SEQUENCING PROBLEM

### Problem Statement:

Given n jobs with deadlines and profits, schedule jobs to maximize profit such that each job is completed before its deadline.

### Greedy Strategy:

1. Sort jobs in decreasing order of profit
1. For each job, assign it to the latest possible slot before its deadline

### Algorithm:

```
Job-Sequencing(jobs[], n)
1. Sort jobs by profit (descending)
2. Find maximum deadline
3. Create time slots array
4. For each job:
   - Find latest available slot before deadline
   - If slot available, assign job
5. Return scheduled jobs and total profit
```

### Time Complexity: O(n²)

### Example:

Jobs: J1(4,20), J2(1,10), J3(1,40), J4(1,30)
After sorting by profit: J3(1,40), J4(1,30), J1(4,20), J2(1,10)
Solution: Schedule J3 at slot 1, J4 at slot 1 (but J3 already there, so slot 0), J1 at slot 4, J2 can’t be scheduled
Maximum profit = 40 + 30 + 20 = 90

-----

## 4. HUFFMAN CODES

### Problem Statement:

Given characters and their frequencies, construct optimal prefix codes to minimize the total encoding length.

### Greedy Strategy:

Always merge two nodes with minimum frequencies.

### Algorithm:

```
Huffman-Codes(C)
1. Create leaf node for each character
2. Build min-heap of all leaf nodes
3. While heap has more than one node:
   - Extract two minimum frequency nodes
   - Create new internal node with these as children
   - Frequency = sum of two nodes' frequencies
   - Insert new node back into heap
4. Root of heap is root of Huffman tree
```

### Time Complexity: O(n log n)

### Properties:

- No code is prefix of another (prefix property)
- Optimal encoding length
- More frequent characters get shorter codes

### Example:

Characters: a(5), b(9), c(12), d(13), e(16), f(45)
Huffman codes: f(0), c(100), d(101), a(1100), b(1101), e(111)

-----

## 5. FRACTIONAL KNAPSACK PROBLEM

### Problem Statement:

Given items with weights and values, and a knapsack of capacity W, fill the knapsack to maximize value. Items can be broken into fractions.

### Greedy Strategy:

Sort items by value-to-weight ratio in descending order and take items greedily.

### Algorithm:

```
Fractional-Knapsack(items[], W)
1. Calculate value/weight ratio for each item
2. Sort items by ratio (descending)
3. For each item:
   - If item fits completely, take it
   - Else take fraction that fits
   - Update remaining capacity
4. Return total value
```

### Time Complexity: O(n log n)

### Example:

Items: (60,10), (100,20), (120,30), Capacity = 50
Ratios: 6, 5, 4
Solution: Take item 1 completely (10kg, value 60), item 2 completely (20kg, value 100), and 20kg of item 3 (value 80)
Total value = 240

-----

## 6. DYNAMIC PROGRAMMING

### What is Dynamic Programming?

A method for solving complex problems by breaking them down into simpler subproblems and storing the results to avoid redundant calculations.

### Key Principles:

1. **Optimal Substructure**: Optimal solution contains optimal solutions to subproblems
1. **Overlapping Subproblems**: Same subproblems are solved multiple times

### Approaches:

1. **Top-Down (Memoization)**: Recursive with caching
1. **Bottom-Up (Tabulation)**: Iterative table filling

-----

## 7. OVERLAPPING SUBSTRUCTURE PROPERTY

### Definition:

A problem has overlapping subproblems if it can be broken down into subproblems which are reused several times.

### Example - Fibonacci Sequence:

```
F(n) = F(n-1) + F(n-2)
```

F(5) calls F(4) and F(3)
F(4) calls F(3) and F(2)
F(3) is computed twice - this is overlapping substructure

### Naive Recursive Approach:

- Time Complexity: O(2^n)
- Space Complexity: O(n)

### Dynamic Programming Approach:

- Time Complexity: O(n)
- Space Complexity: O(n) or O(1)

-----

## 8. OPTIMAL SUBSTRUCTURE PROPERTY

### Definition:

A problem exhibits optimal substructure if an optimal solution to the problem contains optimal solutions to the subproblems.

### How to Identify:

1. Show that a solution to the problem consists of making a choice
1. Suppose that for a given problem, you are given the choice that leads to an optimal solution
1. Given this choice, determine which subproblems ensue
1. Show that the solutions to the subproblems used within the optimal solution must themselves be optimal

### Examples:

- **Shortest Path**: If P is shortest path from u to v, then any subpath of P is also shortest
- **Activity Selection**: If activity k is in optimal solution, then activities before k and after k form optimal solutions for their respective subproblems

-----

## 9. TABULATION vs MEMOIZATION

### Memoization (Top-Down):

```
Memo-Fibonacci(n, memo[])
1. If n ≤ 1, return n
2. If memo[n] is not computed:
   - memo[n] = Memo-Fibonacci(n-1) + Memo-Fibonacci(n-2)
3. Return memo[n]
```

**Advantages:**

- Natural recursive structure
- Only computes needed subproblems
- Easy to implement from recursive solution

**Disadvantages:**

- Function call overhead
- May cause stack overflow for deep recursion

### Tabulation (Bottom-Up):

```
Tabulation-Fibonacci(n)
1. Create table dp[0...n]
2. dp[0] = 0, dp[1] = 1
3. For i = 2 to n:
   - dp[i] = dp[i-1] + dp[i-2]
4. Return dp[n]
```

**Advantages:**

- No recursion overhead
- Better space utilization
- Avoids stack overflow

**Disadvantages:**

- May compute unnecessary subproblems
- Less intuitive than memoization

-----

## 10. COMPARISON: GREEDY vs DYNAMIC PROGRAMMING

|Aspect              |Greedy Algorithm                            |Dynamic Programming                                              |
|--------------------|--------------------------------------------|-----------------------------------------------------------------|
|**Decision Making** |Local optimal choice                        |Considers all possibilities                                      |
|**Backtracking**    |No backtracking                             |May require backtracking                                         |
|**Optimization**    |May not always give optimal solution        |Always gives optimal solution                                    |
|**Time Complexity** |Generally better                            |May be exponential without optimization                          |
|**Space Complexity**|Usually O(1) or O(n)                        |Often O(n) or O(n²)                                              |
|**Implementation**  |Simpler                                     |More complex                                                     |
|**When to Use**     |When greedy choice leads to optimal solution|When problem has optimal substructure and overlapping subproblems|

-----

## IMPORTANT EXAM POINTS

### For Greedy Algorithms:

1. **Always prove correctness** - Show that greedy choice leads to optimal solution
1. **Know the standard problems** - Activity selection, Job sequencing, Huffman coding, Fractional knapsack
1. **Understand when greedy fails** - 0/1 Knapsack, some shortest path problems

### For Dynamic Programming:

1. **Identify the two properties** - Optimal substructure and overlapping subproblems
1. **Master both approaches** - Memoization and Tabulation
1. **Practice state definition** - How to define dp[i] or dp[i][j]
1. **Understand time/space trade-offs**

### Common Exam Question Types:

1. **Algorithm Implementation** - Write pseudocode for given problem
1. **Complexity Analysis** - Time and space complexity calculation
1. **Problem Classification** - Identify if problem suits greedy or DP
1. **Correctness Proof** - Prove that greedy choice is optimal
1. **Comparison Questions** - Compare greedy vs DP approaches
