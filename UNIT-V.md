# Unit V - Hashing, String Matching and NP-Completeness.

## 1. INTRODUCTION TO HASHING

### What is Hashing?

Hashing is a technique that maps data of arbitrary size to fixed-size values using a hash function. It’s primarily used for fast data retrieval, insertion, and deletion operations.

### Key Components:

1. **Hash Function**: Maps keys to array indices
1. **Hash Table**: Array that stores the actual data
1. **Collision Resolution**: Method to handle when multiple keys hash to same index

### Applications:

- Database indexing
- Caching systems
- Password storage
- Digital signatures
- Data deduplication

### Advantages:

- Average O(1) time complexity for search, insert, delete
- Efficient space utilization
- Fast data access

### Disadvantages:

- Worst-case O(n) time complexity
- No ordering of elements
- Requires good hash function design

-----

## 2. HASH FUNCTIONS

### Properties of Good Hash Function:

1. **Uniform Distribution**: Should distribute keys uniformly across hash table
1. **Deterministic**: Same key should always produce same hash value
1. **Efficient**: Should be quick to compute
1. **Avalanche Effect**: Small change in key should cause large change in hash value

### Common Hash Functions:

#### Division Method:

```
h(k) = k mod m
```

- Simple and fast
- Choose m as prime number not close to power of 2
- Example: k=123, m=11 → h(123) = 123 mod 11 = 2

#### Multiplication Method:

```
h(k) = ⌊m(kA mod 1)⌋
```

where A is constant (0 < A < 1), often A = (√5-1)/2 ≈ 0.618

- Less sensitive to choice of m
- m is usually power of 2

#### Mid-Square Method:

1. Square the key
1. Extract middle digits
1. Use as hash value

#### Folding Method:

1. Divide key into parts of equal size
1. Add the parts
1. Use sum as hash value

### Universal Hashing:

A collection of hash functions such that for any two distinct keys, the probability of collision is at most 1/m.

-----

## 3. COLLISION HANDLING

### What is Collision?

When two or more keys hash to the same index in hash table.

### Types of Collision Resolution:

## 3.1 OPEN ADDRESSING

All elements stored in hash table itself. When collision occurs, probe for next available slot.

### Linear Probing:

```
h(k,i) = (h'(k) + i) mod m
```

where i = 0, 1, 2, … and h’(k) is auxiliary hash function

**Algorithm:**

```
Insert(T, k):
1. i = 0
2. repeat
   j = h(k,i)
   if T[j] == NIL:
      T[j] = k
      return j
   else:
      i = i + 1
3. until i == m
4. error "hash table overflow"
```

**Advantages:** Simple implementation, good cache performance
**Disadvantages:** Primary clustering (consecutive occupied slots)

### Quadratic Probing:

```
h(k,i) = (h'(k) + c₁i + c₂i²) mod m
```

where c₁ and c₂ are constants

**Advantages:** Reduces primary clustering
**Disadvantages:** Secondary clustering, may not probe all slots

### Double Hashing:

```
h(k,i) = (h₁(k) + i·h₂(k)) mod m
```

where h₁ and h₂ are auxiliary hash functions

**Requirements:**

- h₂(k) must be relatively prime to m
- h₂(k) ≠ 0

**Advantages:** Eliminates primary and secondary clustering
**Disadvantages:** More computation required

## 3.2 CHAINING

Each slot in hash table contains a linked list of elements that hash to that slot.

**Algorithm:**

```
Chained-Hash-Insert(T, x):
1. Insert x at head of list T[h(key[x])]

Chained-Hash-Search(T, k):
1. Search for element with key k in list T[h(k)]

Chained-Hash-Delete(T, x):
1. Delete x from list T[h(key[x])]
```

**Load Factor:** α = n/m (n = number of elements, m = table size)

**Time Complexity:**

- Average case: O(1 + α)
- Worst case: O(n) when all elements hash to same slot

**Advantages:**

- Simple implementation
- No clustering
- Can handle more elements than table size

**Disadvantages:**

- Extra memory for pointers
- Poor cache performance

-----

## 4. STRING MATCHING ALGORITHMS

### Problem Statement:

Given a text T of length n and pattern P of length m, find all occurrences of P in T.

## 4.1 NAIVE STRING MATCHING ALGORITHM

### Algorithm:

```
Naive-String-Matcher(T, P):
1. n = length[T]
2. m = length[P]
3. for s = 0 to n-m:
   4. if P[1..m] == T[s+1..s+m]:
      5. print "Pattern occurs with shift" s
```

### Time Complexity:

- Best case: O(n) when first character never matches
- Worst case: O(nm) when pattern almost matches at every position
- Average case: O(n)

### Example:

```
Text:    "ABABCABABA"
Pattern: "ABABA"
Shifts:  0,1,2,3,4,5
At shift 5: Match found
```

### Disadvantages:

- Inefficient for large texts
- Doesn’t utilize information from previous comparisons

## 4.2 RABIN-KARP ALGORITHM

### Concept:

Uses hashing to find pattern matches. Compare hash values instead of characters.

### Rolling Hash:

For pattern of length m and base d:

```
hash(P) = P[0]×d^(m-1) + P[1]×d^(m-2) + ... + P[m-1]×d^0
```

### Spurious Hits:

When hash values match but strings don’t match.

### Algorithm:

```
Rabin-Karp-Matcher(T, P, d, q):
1. n = length[T], m = length[P]
2. h = d^(m-1) mod q
3. p = 0, t = 0
4. // Preprocessing
5. for i = 1 to m:
   6. p = (d×p + P[i]) mod q
   7. t = (d×t + T[i]) mod q
8. // Matching
9. for s = 0 to n-m:
   10. if p == t:
       11. if P[1..m] == T[s+1..s+m]:
           12. print "Pattern occurs with shift" s
   13. if s < n-m:
       14. t = (d(t - T[s+1]×h) + T[s+m+1]) mod q
```

### Time Complexity:

- Average case: O(n + m)
- Worst case: O(nm) when many spurious hits occur

### Rolling Hash Calculation:

```
t[s+1] = (d(t[s] - T[s+1]×h) + T[s+m+1]) mod q
```

### Example:

```
Text: "2359023141"
Pattern: "31"
d = 10, q = 13
p = (3×10 + 1) mod 13 = 5
t₀ = (2×10 + 3) mod 13 = 10
t₁ = (10×(10-2×10) + 5) mod 13 = 7
...continue until match found
```

## 4.3 KNUTH-MORRIS-PRATT (KMP) ALGORITHM

### Key Insight:

When mismatch occurs, use information about pattern to skip unnecessary comparisons.

### Prefix Function:

π[q] = max{k : k < q and P[1..k] is suffix of P[1..q]}

### Computing Prefix Function:

```
Compute-Prefix-Function(P):
1. m = length[P]
2. π[1] = 0
3. k = 0
4. for q = 2 to m:
   5. while k > 0 and P[k+1] ≠ P[q]:
      6. k = π[k]
   7. if P[k+1] == P[q]:
      8. k = k + 1
   9. π[q] = k
10. return π
```

### KMP Algorithm:

```
KMP-Matcher(T, P):
1. n = length[T], m = length[P]
2. π = Compute-Prefix-Function(P)
3. q = 0
4. for i = 1 to n:
   5. while q > 0 and P[q+1] ≠ T[i]:
      6. q = π[q]
   7. if P[q+1] == T[i]:
      8. q = q + 1
   9. if q == m:
      10. print "Pattern occurs with shift" i-m
      11. q = π[q]
```

### Time Complexity:

- Preprocessing: O(m)
- Matching: O(n)
- Total: O(n + m)

### Example:

```
Pattern: "ABABACA"
π array: [0,0,1,2,3,0,1]

Text: "ABABABACABA"
Matching process shows how mismatches are handled efficiently
```

-----

## 5. NP-COMPLETENESS

### Complexity Classes:

#### P (Polynomial Time):

Set of decision problems solvable in polynomial time by deterministic Turing machine.

- Examples: Sorting, Shortest path, Matrix multiplication

#### NP (Nondeterministic Polynomial Time):

Set of decision problems verifiable in polynomial time.

- If given a solution, can verify it in polynomial time
- Examples: Hamiltonian cycle, Subset sum, Graph coloring

#### NP-Complete:

Problems that are:

1. In NP
1. Every problem in NP can be reduced to it in polynomial time

#### NP-Hard:

Problems at least as hard as NP-complete problems, but may not be in NP.

### Relationship:

```
P ⊆ NP
NP-Complete ⊆ NP
NP-Complete ⊆ NP-Hard
```

### P vs NP Problem:

Biggest unsolved problem in computer science: Does P = NP?

- If P = NP: Efficient algorithms exist for all NP problems
- If P ≠ NP: Some problems are inherently intractable

-----

## 6. POLYNOMIAL TIME AND POLYNOMIAL TIME VERIFICATION

### Polynomial Time Algorithm:

Running time is O(n^k) for some constant k.

### Polynomial Time Verification:

An algorithm V is polynomial-time verification algorithm for problem if:

1. V runs in polynomial time
1. For any instance x: x ∈ L iff there exists certificate y such that V(x,y) = 1

### Certificate:

Additional information that makes verification easy.

### Examples:

- **Hamiltonian Cycle**: Certificate is the actual cycle
- **Subset Sum**: Certificate is the subset that sums to target
- **Graph Coloring**: Certificate is the actual coloring

-----

## 7. NP-COMPLETE AND NP-HARD PROBLEMS

### How to Prove NP-Completeness:

1. Show problem is in NP (polynomial-time verifiable)
1. Show problem is NP-hard (reduce known NP-complete problem to it)

### First NP-Complete Problem:

**Boolean Satisfiability (SAT)** - Cook’s Theorem (1971)

### Common NP-Complete Problems:

#### Subset Sum Problem:

**Input:** Set S of integers, target sum t
**Question:** Is there subset of S that sums to t?

#### Traveling Salesman Problem (Decision Version):

**Input:** Graph G, weight function w, bound k
**Question:** Is there Hamiltonian cycle with total weight ≤ k?

#### Graph Coloring:

**Input:** Graph G, integer k
**Question:** Can vertices be colored with k colors such that no adjacent vertices have same color?

#### Hamiltonian Cycle:

**Input:** Graph G
**Question:** Does G contain Hamiltonian cycle?

#### Clique Problem:

**Input:** Graph G, integer k
**Question:** Does G contain clique of size k?

#### Vertex Cover:

**Input:** Graph G, integer k
**Question:** Does G have vertex cover of size ≤ k?

### Reduction:

If problem A reduces to problem B in polynomial time, then:

- If B has polynomial solution, so does A
- If A has no polynomial solution, neither does B

-----

## 8. IMPORTANCE OF NP-COMPLETENESS

### Theoretical Importance:

1. **Classification**: Helps classify computational problems
1. **Difficulty Assessment**: Identifies inherently difficult problems
1. **Algorithm Design**: Guides approach to problem solving

### Practical Importance:

1. **Recognition**: Helps recognize when to stop looking for efficient algorithms
1. **Approximation**: Motivates development of approximation algorithms
1. **Heuristics**: Encourages use of heuristic methods

### What to Do with NP-Complete Problems:

1. **Approximation Algorithms**: Find near-optimal solutions
1. **Heuristic Methods**: Use problem-specific knowledge
1. **Randomized Algorithms**: Use probabilistic approaches
1. **Parameterized Complexity**: Fix some parameters
1. **Special Cases**: Identify tractable subcases

-----

## EXAM PREPARATION POINTS

### For Hashing:

1. **Hash Function Design** - Know different methods and their trade-offs
1. **Collision Resolution** - Master both open addressing and chaining
1. **Load Factor Analysis** - Understand impact on performance
1. **Time Complexity** - Average vs worst case scenarios

### For String Matching:

1. **Algorithm Comparison** - Naive vs Rabin-Karp vs KMP
1. **KMP Prefix Function** - How to compute and use
1. **Rolling Hash** - Rabin-Karp implementation details
1. **Time Complexity Analysis** - Best, average, worst cases

### For NP-Completeness:

1. **Definitions** - P, NP, NP-Complete, NP-Hard
1. **Proof Techniques** - How to show NP-completeness
1. **Problem Examples** - Know standard NP-complete problems
1. **Practical Implications** - What it means for algorithm design

### Common Exam Question Types:

1. **Hash Function Implementation** - Design hash function for given scenario
1. **Collision Resolution** - Trace through insertion/search operations
1. **String Matching Trace** - Step-by-step algorithm execution
1. **NP-Completeness Proof** - Show problem is NP-complete
1. **Complexity Classification** - Classify problems into P, NP, etc.
