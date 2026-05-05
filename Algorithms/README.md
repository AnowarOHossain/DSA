# Algorithm Notes

**Author:** Anowar Hossain
**Subject:** Algorithms & Analysis

---

## 1. Introduction to Algorithms
* **Algorithm:** An algorithm is a step-by-step procedure or a set of rules used to solve a specific problem or to accomplish a specific task.
* **Program:** A program is a collection of instructions or code written in a specific programming language.

**Algorithm vs Program:**
| Algorithm | Program |
| :--- | :--- |
| 1. Design | 1. Implementation |
| 2. Domain knowledge | 2. Programmer |
| 3. Any Language | 3. Programming Language |
| 4. Hardware/OS Independent | 4. Hardware & OS Dependent |
| 5. Analyze | 5. Testing |

**Priori Analysis vs Posteriori Testing:**
| Priori Analysis | Posteriori Testing |
| :--- | :--- |
| 1. Algorithm | 1. Program |
| 2. Independent of Language | 2. Language dependent |
| 3. Hardware Independent | 3. Hardware dependent |
| 4. Time & Space Function | 4. Watch time & Bytes |

**Characteristics of Algorithm:**
1. Input - 0 or more.
2. Output - at least 1 output.
3. Definiteness
4. Finiteness
5. Effectiveness

**How to write an Algorithm:**
```text
Algorithm swap(a,b) {
    temp = a;
    a = b;
    b = temp;
}
```

**How to analyze an algorithm:**
1. Time
2. Space
3. Network
4. Power
5. CPU Registers

---

## 2. Space and Time Complexity (Frequency Count)

**Example 1: Swap**
```text
Algorithm swap(a,b) {
    temp = a;   // 1
    a = b;      // 1
    b = temp;   // 1
}
// Time: f(n) = 3 -> O(1)
// Space: S(n) = 3 variables -> O(1)
```

**Example 2: Sum Array**
```text
Algorithm Sum(A,n) {
    s = 0;                     // 1
    for (i = 0; i < n; i++)    // n+1
    {
        s = s + A[i];          // n
    }
    return s;                  // 1
}
// Time: f(n) = 2n + 3 -> O(n)
// Space: Array A(n), n(1), s(1), i(1) -> S(n) = n + 3 -> O(n)
```

**Example 3: Matrix Addition**
```text
Algorithm Add(A,B,n) {
    for(i=0; i<n; i++)              // n+1
    {
        for(j=0; j<n; j++)          // n * (n+1)
        {
            C[i,j] = A[i,j] + B[i,j]; // n * n
        }
    }
}
// Time: f(n) = 2n^2 + 2n + 1 -> O(n^2)
// Space: A(n^2), B(n^2), C(n^2), n(1), i(1), j(1) -> S(n) = 3n^2 + 3 -> O(n^2)
```

**Example 4: Matrix Multiplication**
```text
Algorithm Multiply(A,B,n) {
    for(i=0; i<n; i++) {                        // n+1
        for(j=0; j<n; j++) {                    // n * (n+1)
            C[i,j] = 0;                         // n * n
            for(k=0; k<n; k++) {                // n * n * (n+1)
                C[i,j] = C[i,j] + A[i,k]*B[k,j];  // n * n * n
            }
        }
    }
}
// Time: f(n) = 2n^3 + 3n^2 + 2n + 1 -> O(n^3)
// Space: A(n^2), B(n^2), C(n^2), n(1), i(1), j(1), k(1) -> S(n) = 3n^2 + 4 -> O(n^2)
```

### Advanced Loop Complexities

1. `for(i=1; i<n; i=i+2)` -> Time: $O(n)$
2. `for(i=0; i<n; i++) { for(j=0; j<i; j++) }` -> Time: $1+2+...+n = \frac{n(n+1)}{2}$ -> $O(n^2)$
3. `for(i=1; P<=n; i++) { P = P + i; }` -> $k(k+1)/2 > n$ -> $O(\sqrt{n})$
4. `for(i=1; i<n; i=i*2)` -> $2^k = n$ -> $k = \log_2 n$ -> $O(\log n)$
5. `for(i=n; i>=1; i=i/2)` -> $n/2^k = 1$ -> $O(\log n)$
6. `for(i=0; i*i<n; i++)` -> $i^2 = n$ -> $i = \sqrt{n}$ -> $O(\sqrt{n})$
7. `for(i=1; i<n; i=i*2) { for(j=1; j<n; j=j*2) }` -> $O(\log n \times \log n)$ -> $O(\log^2 n)$

**While Loop Complexity:**
```text
a = 1;
while(a < b) {
    stmt;
    a = a * 2;
}
// a = 2^k -> 2^k >= b -> k = log_2 b -> O(log b)
```

---

## 3. Asymptotic Notations
Functions: Constant ($O(1)$) < Logarithmic ($O(\log n)$) < Linear ($O(n)$) < Quadratic ($O(n^2)$) < Cubic ($O(n^3)$) < Exponential ($O(2^n)$) < $O(n^n)$.

1. **Big-Oh ($O$): Upper bound.**
   $f(n) \le C \times g(n)$ for all $n \ge n_0$. Use the nearest upper value.
2. **Big-Omega ($\Omega$): Lower bound.**
   $f(n) \ge C \times g(n)$ for all $n \ge n_0$. Use the nearest lower value.
3. **Theta ($\Theta$): Average/Exact bound.**
   $C_1 \times g(n) \le f(n) \le C_2 \times g(n)$.

**Properties:**
* **General:** If $f(n)$ is $O(g(n))$, then $a \times f(n)$ is $O(g(n))$.
* **Reflexive:** $f(n)$ is $O(f(n))$.
* **Transitive:** If $f(n)$ is $O(g(n))$ and $g(n)$ is $O(h(n))$, then $f(n)$ is $O(h(n))$.
* **Symmetric (Theta only):** If $f(n)$ is $\Theta(g(n))$, then $g(n)$ is $\Theta(f(n))$.
* **Addition:** If $f(n)=O(g(n))$ and $d(n)=O(e(n))$, then $f(n)+d(n) = O(\max(g(n), e(n)))$.

**Comparing Functions with Logarithms:**
Apply log on both sides to compare large functions easily.
* Formulas: $\log(ab) = \log a + \log b$; $\log(a^b) = b \log a$.
* Example: $f(n) = n^{\log n}$ vs $g(n) = 2^n$. Apply log: $\log^2 n$ vs $n$. So, $g(n)$ is greater.

---

## 4. Divide & Conquer
**Key algorithms:** Binary Search, Min/Max, Merge Sort, Quick Sort, Strassen's Matrix Multiplication.

**Master Theorem for Decreasing Functions:** $T(n) = aT(n-b) + f(n)$ where $f(n) = O(n^k)$.
1. If $a < 1$: $O(n^k)$
2. If $a = 1$: $O(n^{k+1})$
3. If $a > 1$: $O(n^k \times a^{n/b})$

**Master Theorem for Dividing Functions:** $T(n) = aT(n/b) + f(n)$ where $f(n) = \Theta(n^k \log^p n)$.
1. If $\log_b a > k$: $\Theta(n^{\log_b a})$
2. If $\log_b a = k$:
   * $p > -1$: $\Theta(n^k \log^{p+1} n)$
   * $p = -1$: $\Theta(n^k \log\log n)$
   * $p < -1$: $\Theta(n^k)$
3. If $\log_b a < k$: If $p \ge 0$, $\Theta(n^k \log^p n)$.

### Binary Search
Iterative and Recursive approaches.
* Time Complexity: Best $O(1)$, Worst/Average $O(\log n)$.

### Merge Sort
* $T(n) = 2T(n/2) + n$. (Using Master Theorem: $a=2, b=2, k=1 \implies \log_2 2 = 1 = k$).
* Complexity: $\Theta(n \log n)$.
* Pros: Good for large data, Linked Lists, External sorting, Stable.
* Cons: Requires extra space (not in-place), Recursive.

### Quick Sort
* Time Complexity: Best/Average $O(n \log n)$, Worst $O(n^2)$.
* It selects a pivot and places elements smaller to the left and larger to the right.

### Strassen's Matrix Multiplication
Standard matrix multiplication takes $O(n^3)$. Divide and conquer (normal) takes $T(n) = 8T(n/2) + n^2 \implies O(n^3)$.
Strassen reduces the 8 multiplications to 7.
* Recurrence: $T(n) = 7T(n/2) + n^2$.
* Complexity: $O(n^{\log_2 7}) \approx O(n^{2.81})$.

---

## 5. Greedy Method
**Optimization problem:** Feasible solution -> Optimal Solution.
* Algorithms: Knapsack problem, Job Sequencing with Deadlines, Optimal Merge Pattern, Huffman Coding.

**Fractional Knapsack Problem:**
Calculate profit/weight ratio ($P_i / W_i$), sort in descending order. Pick maximum ratios first. For the last item, take the fraction that fits.
* Objective: $\max \sum x_i p_i$ subject to $\sum x_i w_i \le m$.

**Job Sequencing with Deadlines:**
Sort jobs in descending order of profit. Place them in the maximum available time slot before their deadline.

**Optimal Merge Pattern:**
Pick the two smallest elements, merge them, put the result back. Repeat until one element is left. Cost is the sum of all internal node values.

**Huffman Coding:**
Used for data compression. Calculate frequency, build a tree from the two lowest frequencies, assign `0` to left edges and `1` to right edges.
* Message size = Total Bits of original characters.
* Compressed size = (Frequency $\times$ Code Length) + Table Size.

---

## 6. Dynamic Programming
**Principle of Optimality.** Top-Down Approach (Memoization) vs Bottom-Up Approach (Tabulation).

**Algorithms:**
1. Fibonacci Series (Top-down is $O(2^n)$, Bottom-up is $O(n)$).
2. Multistage Graph.
3. All pairs shortest path (Floyd-Warshall).
4. Single source shortest path (Bellman-Ford).
5. 0/1 Knapsack Problem.

**Floyd-Warshall Algorithm:**
Finds the shortest path between all pairs of vertices.
* Formula: $A^k[i,j] = \min \{ A^{k-1}[i,j], \ A^{k-1}[i,k] + A^{k-1}[k,j] \}$
* Complexity: $O(V^3)$.

**Bellman-Ford Algorithm:**
Used for graphs with negative weights. Relaxes all edges $|V|-1$ times.
* Complexity: $\Theta(|V||E|)$ which is $O(n^2)$ for sparse graphs.

**0/1 Knapsack Problem:**
Items are either completely picked (1) or left (0). No fractions.
* Formula: $V[i,w] = \max( V[i-1, w], \ V[i-1, w-w_i] + p_i )$

---

## 7. Graph Algorithms (Spanning Trees & Shortest Path)

### Minimum Cost Spanning Tree
A subset of edges from a connected weighted graph that connects all vertices together with the minimum possible total edge weight.
* $|V| = n$, Edges $= n - 1$.

**Prim's Algorithm:**
Takes a graph as input and finds a subset of the edges that form a tree including every vertex, with the minimum sum of weights. Grows the tree from a starting node.

**Kruskal's Algorithm:**
Sorts all edges in non-decreasing order. Adds edges to the tree if they do not form a cycle. Uses Disjoint Sets (Union-Find) to detect cycles.

### Dijkstra's Algorithm
Finds the shortest path from a single source node to all other nodes. (Greedy approach). Does not work with negative weights.
* Formula (Relaxation): `if (d[v] + c(u,v) < d[v]) d[v] = d[u] + c(u,v)`
* Complexity: $O(V^2)$ with arrays, $O((V+E)\log V)$ with Min-Heap.

---

## 8. Disjoint Sets
Used primarily in Kruskal's algorithm and cycle detection.
* Operations: `Make Set`, `Find`, `Union`.
* **Array Representation:** Represents elements. Root nodes hold `-1` (or negative count for weighted union), children point to their parent's index.
* **Weighted Union & Collapsing Find:** Optimizations to keep the tree flat, improving time complexity.

---

## 9. Searching Algorithms

### Linear Search
* **Time Complexity:** $O(n)$
* **Space Complexity:** $O(1)$
* Works on unsorted and sorted arrays
* Sequential comparison with each element

### Binary Search
* **Time Complexity:** $O(\log n)$ 
* **Space Complexity:** $O(1)$ iterative, $O(\log n)$ recursive
* **Prerequisite:** Array must be sorted
* **Recurrence:** $T(n) = T(n/2) + O(1)$ leads to $O(\log n)$
* **Variations:** First occurrence, Last occurrence, Insert position

---

## 10. Sorting Algorithms (Detailed)

### Bubble Sort
* **Time:** $O(n^2)$ average & worst, $O(n)$ best
* **Space:** $O(1)$
* **Stable:** Yes
* Compare adjacent elements and swap if they are in wrong order

### Selection Sort
* **Time:** $O(n^2)$
* **Space:** $O(1)$
* **Stable:** No
* Find minimum and swap with current position

### Insertion Sort
* **Time:** $O(n^2)$ average & worst, $O(n)$ best
* **Space:** $O(1)$
* **Stable:** Yes
* Insert each element in its correct position

### Merge Sort
* **Time:** $O(n \log n)$ all cases
* **Space:** $O(n)$
* **Stable:** Yes
* Divide array in half, sort recursively, merge

### Quick Sort
* **Time:** $O(n \log n)$ average, $O(n^2)$ worst
* **Space:** $O(\log n)$
* **Stable:** No
* Partition based on pivot, sort recursively

### Heap Sort
* **Time:** $O(n \log n)$
* **Space:** $O(1)$
* **Stable:** No
* Build max/min heap, extract elements

### Counting Sort
* **Time:** $O(n + k)$ where $k$ is range
* **Space:** $O(k)$
* **Stable:** Yes
* Count frequency of each element

### Radix Sort
* **Time:** $O(d(n + k))$ where $d$ is number of digits
* **Space:** $O(n + k)$
* **Stable:** Yes
* Sort by each digit from least to most significant

### Bucket Sort
* **Time:** $O(n + k)$ average, $O(n^2)$ worst
* **Space:** $O(n + k)$
* **Stable:** Yes
* Distribute elements into buckets, sort each bucket

---

## 11. Recursion and Backtracking

### Recursion Basics
* **Base Case:** Condition to stop recursion
* **Recursive Case:** Function calls itself with simpler problem
* **Call Stack:** Each call creates a stack frame
* **Time Complexity:** Depends on number of calls and work per call

**Example: Factorial**
* $T(n) = T(n-1) + O(1) = O(n)$

**Example: Fibonacci**
* Naive: $T(n) = T(n-1) + T(n-2) = O(2^n)$
* Optimized with memoization: $O(n)$

### Backtracking
* **Concept:** Build solution incrementally, remove invalid solutions
* **Use Cases:** N-Queens, Sudoku, Permutations, Combinations, Maze

**N-Queens Problem:**
Place $n$ queens on $n \times n$ chessboard such that no two attack each other.
* Time Complexity: $O(N!)$

**Sudoku Solver:**
Fill empty cells respecting Sudoku rules.
* Time Complexity: $O(9^{n})$ in worst case

---

## 12. Pattern Matching / String Matching

### KMP (Knuth-Morris-Pratt) Algorithm
* **Time:** $O(n + m)$ where $n$ is text length, $m$ is pattern
* **Space:** $O(m)$ for LPS array
* Build LPS (Longest Proper Prefix which is also Suffix)
* No backtracking in text

### Boyer-Moore Algorithm
* **Time:** $O(n/m)$ best case, $O(nm)$ worst case
* **Space:** $O(\sigma)$ where $\sigma$ is alphabet size
* Faster for large alphabets and patterns
* Search from right to left in pattern

### Rabin-Karp Algorithm
* **Time:** $O(n + m)$ average, $O(nm)$ worst
* **Space:** $O(1)$
* Uses rolling hash for pattern matching
* Good for multiple pattern matching

### Z-Algorithm
* **Time:** $O(n)$
* **Space:** $O(n)$
* Computes Z-array: length of longest substring starting at position $i$ which matches prefix

---

## 13. Graph Traversals (Detailed)

### Breadth-First Search (BFS)
* **Time:** $O(V + E)$
* **Space:** $O(V)$ for queue
* Uses queue data structure
* Explores vertices level by level
* Finds shortest path in unweighted graph

### Depth-First Search (DFS)
* **Time:** $O(V + E)$
* **Space:** $O(V)$ for recursion stack
* Uses stack (or recursion)
* Explores as far as possible along each branch
* **Edge Classification:** Tree edge, Back edge, Forward edge, Cross edge

### Topological Sorting
* **Used For:** Dependency resolution, scheduling
* **Methods:** DFS-based, Kahn's algorithm (BFS-based)
* **Time:** $O(V + E)$
* Only for Directed Acyclic Graphs (DAG)

### Strongly Connected Components (SCC)
* **Kosaraju's Algorithm:** $O(V + E)$
  1. Perform DFS, push vertices to stack
  2. Create transposed graph
  3. Pop vertices from stack, perform DFS on transposed graph
* **Tarjan's Algorithm:** $O(V + E)$
  - Single DFS pass using low and discovery times

---

## 14. Bit Manipulation

**Common Bit Operations:**
| Operation | Syntax | Result |
|-----------|--------|--------|
| AND | `a & b` | 1 if both are 1 |
| OR | `a \| b` | 1 if at least one is 1 |
| XOR | `a ^ b` | 1 if different |
| NOT | `~a` | Flip all bits |
| Left Shift | `a << b` | Multiply by $2^b$ |
| Right Shift | `a >> b` | Divide by $2^b$ |

**Bit Tricks:**
* Check if power of 2: $(n \& (n-1)) == 0$
* Count set bits: $\text{popcount}(n)$
* Rightmost set bit: $n \& (-n)$
* Clear rightmost set bit: $n \& (n-1)$
* Check $i$-th bit: $(n >> i) \& 1$
* Set $i$-th bit: $n \| (1 << i)$
* Toggle $i$-th bit: $n ^ (1 << i)$

---

## 15. Mathematical Algorithms

### Greatest Common Divisor (GCD)
**Euclidean Algorithm:**
* $\gcd(a, b) = \gcd(b, a \mod b)$
* **Time:** $O(\log(\min(a, b)))$

### Least Common Multiple (LCM)
* $\text{lcm}(a, b) = \frac{a \times b}{\gcd(a, b)}$

### Prime Checking
**Naive Approach:** Check divisibility up to $n$. Time: $O(n)$

**Optimized:** Check divisibility up to $\sqrt{n}$. Time: $O(\sqrt{n})$

### Sieve of Eratosthenes
* Find all primes up to $n$
* **Time:** $O(n \log \log n)$
* **Space:** $O(n)$
* Mark multiples of each prime as composite

### Modular Arithmetic
* $(a + b) \mod m = ((a \mod m) + (b \mod m)) \mod m$
* $(a \times b) \mod m = ((a \mod m) \times (b \mod m)) \mod m$
* Modular exponentiation: $a^b \mod m$ using binary exponentiation

---

## 16. String Algorithms

### Palindrome Checking
* **Method 1:** Compare string with its reverse. Time: $O(n)$
* **Method 2:** Expand around center. Time: $O(n^2)$ worst case

### Anagram Checking
* **Method 1:** Sort both strings, compare. Time: $O(n \log n)$
* **Method 2:** Count character frequencies. Time: $O(n)$

### Longest Common Subsequence (LCS)
* **Dynamic Programming Approach:**
  * $\text{LCS}[i][j] = 1 + \text{LCS}[i-1][j-1]$ if $s_1[i] == s_2[j]$
  * $\text{LCS}[i][j] = \max(\text{LCS}[i-1][j], \text{LCS}[i][j-1])$ otherwise
* **Time:** $O(m \times n)$

### Longest Common Substring
* Similar DP approach but resets when characters don't match
* **Time:** $O(m \times n)$

### Edit Distance (Levenshtein Distance)
* Minimum operations (insert, delete, replace) to convert one string to another
* **DP Formula:** $\text{dp}[i][j] = \min(dp[i-1][j] + 1, dp[i][j-1] + 1, dp[i-1][j-1] + cost)$
* **Time:** $O(m \times n)$

---

## 17. NP-Hard and NP-Complete Problems

**P:** Problems solvable in polynomial time.
**NP:** Problems verifiable in polynomial time.
**NP-Hard:** At least as hard as any NP problem.
**NP-Complete:** Both NP and NP-Hard.

**Common NP-Complete Problems:**
* Boolean Satisfiability (SAT)
* Traveling Salesman Problem (TSP)
* Knapsack Problem (0/1)
* Graph Coloring
* Hamiltonian Path
* Vertex Cover

**Important:** If any NP-Complete problem is solved in polynomial time, then $P = NP$.

---

## 18. Approximation Algorithms

Provides near-optimal solution when exact solution is hard to find.

**Approximation Ratio:** $\frac{\text{Approximate Solution}}{\text{Optimal Solution}}$

**Examples:**
* **Traveling Salesman Problem:** 2-approximation using minimum spanning tree
* **Vertex Cover:** 2-approximation using maximal matching
* **Set Cover:** $\log(n)$-approximation using greedy approach

---

## 19. Randomized Algorithms

Use randomness to make decisions during execution.

**Examples:**
* **Randomized Quick Sort:** Random pivot selection to avoid worst case
* **Randomized Selection:** Find $k$-th smallest element
* **Monte Carlo:** May give wrong answer (Las Vegas variant always correct)
* **Las Vegas:** Always gives correct answer but runtime varies

**Complexity:**
* Expected time complexity analyzed using probability

---

## Handwritten Notes

I have documented my learning journey Algorithms with handwritten notes. You can access the PDFs here:

- [📄 Algorithms Handwritten Notes] (https://drive.google.com/file/d/11MPKn7mrogqpHeiRZYoC12RbRJ_GUqNf/view?usp=sharing)

