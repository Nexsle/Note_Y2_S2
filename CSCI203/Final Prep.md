# Part 1: Algo Complexity
## **1. The Three Notations:**

- **Big-O (O)**: Upper bound - worst case ("at most this bad")
- **Theta (Θ)**: Tight bound - average/typical case ("exactly this")
- **Omega (Ω)**: Lower bound - best case ("at least this good")
`O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)`

**Question 11:** Rank these from fastest to slowest growth:
- A) O(n²)
- B) O(2ⁿ)
- C) O(n log n)
- D) O(n!)
- E) O(log n)
`D - B - A - C - E`


**Question 12:** What's the complexity of binary search on a sorted array of size n?
`Since binary search divides the array into half the complexity is O(logn)`

**Question 13:** If an algorithm runs in O(n²) time for input size n, approximately how much longer will it take if you double the input size to 2n?
`(Since they are asking for scaling factor not big O) It will be 4 times slower`

**Question 14:** True or False: O(2n) is different from O(n)?
`False`

**Question 15:** What's the time complexity of accessing an element in an array by index (e.g., arr\[5])?
`O(1)`

## **2. Master Theorem**
### The Recurrence Relation Form:
`T(n) = a·T(n/b) + f(n)`

**Case 1:** If f(n) is smaller than $n^{(log_b(a))}$

- **Result:** T(n) = Θ($n^{(log_b(a))}$)

**Case 2:** If f(n) equals $n^{(log_b(a))}$

- **Result:** T(n) = Θ($n^{(log_b(a))}· log n$ )

**Case 3:** If f(n) is larger than $n^{(log_b(a))}$

- **Result:** T(n) = Θ(f(n))

```python
def mystery(n):
    if n <= 1:
        return
    for i in range(n):      # O(n) work
        print(i)
    mystery(n // 2)          # 2 recursive calls
    mystery(n // 2)          # with n/2 size
```

**Recurrence:** T(n) = 2·T(n/2) + n

**Using Master Theorem:**

- a = 2 (two recursive calls)
- b = 2 (dividing by 2)
- f(n) = n (the loop)
- n^(log_b(a)) = n^(log₂(2)) = n^1 = n

Since f(n) = n equals n^(log_b(a)) = n:

- **Case 2 applies!**
- **Answer:** T(n) = Θ(n log n)
# Part 2: Data Structures

Now let's tackle **Basic & Tree Structures**. This is where you'll need to know:

- **When to use each structure**
- **Time complexity of operations**
- **How to implement key operations**

### Quick Overview:

|Structure|Insert|Delete|Search|Use Case|
|---|---|---|---|---|
|Array|O(n)|O(n)|O(n)|Direct access by index|
|Linked List|O(1)*|O(1)*|O(n)|Dynamic size, frequent insertions|
|Stack|O(1)|O(1)|-|LIFO operations|
|Queue|O(1)|O(1)|-|FIFO operations|
|BST|O(log n)†|O(log n)†|O(log n)†|Ordered data|
## Key Tree Concepts
### 1.Binary search tree
**Property:** Left subtree < Node < Right subtree
- Complexity: o(h) where h = height
	- Balanced: O(log n)
	- Worst case (skewed) : O(n)

### 2.AVL tree (self balancing BST)
**Property**: |height(left) - height(right)| $\leq$ 1 for every node
- Rotations: single (LL, RR) and double (LR, RL)
- Complexity: always O(log n) guaranteed 
```
50
     /  \
   30    70
  /  \   /  \
 20  40 60  80
```

**AVL Balance Factors:**
```
      50 (BF=0)
     /  \
   30    70 (BF=-1)
  /  \     \
 20  40    80
```
BF = height(left) - height(right)
### 3. BTree of order m
$[⌈m/2⌉-1, m-1]$
**Properties**: 
- $⌈m/2⌉$ children
- Root can have 2 children
- All leaf at same level
- Bottom up create 
![[Pasted image 20251104184803.png]]
![[Pasted image 20251104184822.png]]
## Practice Questions - Part 2A: BST Operations

**Question 1:** Insert the following into an empty BST in order: 50, 30, 70, 20, 40, 60, 80
- Draw the final tree structure
![[Drawing 2025-11-04 22.24.17.excalidraw]]
- What's the height of the tree?
`Height is 3`

**Question 2:** Given this BST:
```
      50
     /  \
   30    70
  /  \     \
 20  40    80
```
Delete node 30. Show the tree after deletion.
![[Drawing 2025-11-04 22.30.31.excalidraw]]

**Question 3:** What's the time complexity to search for a value in:

- A balanced BST with n nodes?
`O(logn)`
- A completely skewed BST (like a linked list)?
`O(n)`
**Question 4:** True or False: In a BST, an inorder traversal (Left-Root-Right) produces values in sorted order.
`True`
**Question 5:** Given this sequence: 10, 5, 15, 3, 7, 12, 20
![[Drawing 2025-11-04 22.33.07.excalidraw]]
- What's the worst-case search time if inserted in this order into a BST?
`O(logn)`
- What if we insert in this order: 3, 5, 7, 10, 12, 15, 20?
`O(n)`

**Question 6:** Insert these values into an empty AVL tree in order: **10, 20, 30**

After inserting 10, 20, 30 into a regular BST, you'd get:
```
10
  \
   20
     \
      30  (skewed - bad!)
```
- What rotation is needed?
`RR rotation`
- Draw the tree after rotation
![[Drawing 2025-11-05 00.23.09.excalidraw]]

**Question 7:** What are the balance factors of each node in this tree?
```
      50
     /  \
   30    70
  /        \
 20        80
```

`(50): 0, (30): 0, (70): 0, (20): 0, (80): 0`

**Question 8:** Starting with an empty AVL tree, insert: **50, 25, 75, 10, 30**
- Show the tree after each insertion
![[Drawing 2025-11-05 00.31.10.excalidraw]]
- Indicate when rotations occur and what type
![[Drawing 2025-11-05 00.33.49.excalidraw]]
`Rotation LR on node 50, 25, 30`

**Question 9:** True or False: An AVL tree with n nodes always has height O(log n)?
`True`

**Question 10:** Which rotation type is needed for this imbalance?
```
      30 (BF=+2)
     /
   20 (BF=+1)
  /
 10
```
`Rotation LL`

**Question 11:** For a **B-Tree of order 5**:

- What is the maximum number of keys in a node?
`4`
- What is the minimum number of keys in a non-root internal node?
`4`
- What is the maximum number of children a node can have?
`5`

---

**Question 12:** Insert the following into an empty **B-Tree of order 3**: **10, 20, 5, 6, 12, 30**

Show the tree after: a) Inserting 10, 20, 5 b) Inserting 6 (this will cause a split) c) Final tree after all insertions

---

**Question 13:** Given this **B-Tree of order 4**:
```
		 [40]
        /    \
   [10, 20]  [50, 60, 70]
```


# Part 3: Sorting Algorithm
### Quick Complexity Reference

| Algorithm         | Best Case  | Average Case | Worst Case | Space    | Stable? |
| ----------------- | ---------- | ------------ | ---------- | -------- | ------- |
| **Merge Sort**    | O(n log n) | O(n log n)   | O(n log n) | O(n)     | Yes     |
| **Heap Sort**     | O(n log n) | O(n log n)   | O(n log n) | O(1)     | No      |
| **Quick Sort**    | O(n log n) | O(n log n)   | O(n²)      | O(log n) | No      |
| **Counting Sort** | O(n+k)     | O(n+k)       | O(n+k)     | O(k)     | Yes     |
| **Radix Sort**    | O(d(n+k))  | O(d(n+k))    | O(d(n+k))  | O(n+k)   | Yes     |
**Key Terms:**

- **Stable:** Equal elements maintain their relative order
- **k:** Range of input values
- **d:** Number of digits

>Merge and heap are asymptotically optimal due to the upperbound for this sorting is O(nlogn) , matches the worst case lower bound of comparison sort
### Summary 
#### 1.Merge sort
- Split in half recursively
- Merge sorted halves
- Always O(n logn)
- Uses extra space O(n)
#### 2.Heap sort
- Build max heap
- Repeatedly extract max and restore heap
- Always O(n logn)
- In place O(1) space

>Max and min number of element in a heap
>For a heap with height h:
>Min: $2^h$
>Max $2^{h+1}-1$

#### 3.Quick sort
- Pick pivot, partition around it
- Recursively sort partitions
- Fast average case, but $O(n^2)$ on sorted data
- Most practical
#### 4.Counting sort
- Count occurrences of each value
- Works when values in small range \[0, k]
- O(n+k) - linear when k is small
#### 5.Radix Sort
- Sort digit by digit 
- Uses counting sort as subroutine
- **O(d(n+k))** where d = number of digits

## Practice Questions - Part 3: Sorting

**Question 16:** Which sorting algorithm would you choose for: a) Sorting 1 million integers in range [0, 100] b) Sorting with guaranteed O(n log n) and O(1) space c) General-purpose sorting with best average performance d) Sorting strings of equal length

`a) since we have a small range i will use couting sort`
`b) Heap sort`
`c) Quick sort`
`d) Quick sort`


---

**Question 17:** Trace **Merge Sort** on array: `[38, 27, 43, 3]`

- Show the divide phase (splitting)
`[38, 27] [43, 3]`
`[27, 38] [3, 43]`
`[3, 27, 38, 43]`
- Show the merge phase (combining)

---

**Question 18:** Given array `[4, 10, 3, 5, 1]`, build a **max-heap**:

- Show the array after heapify
`[10, 5, 3, 4, 1]
- What's the first element extracted in heap sort?
`10`

---

**Question 19:** Why does Quick Sort have O(n²) worst case?

- When does this happen?
`When all the element in the array is alr sorted or reverse sorted`
- How can we avoid it?
`Shuffle before sortin`
`Randommized pivot`

---

**Question 20:** True or False: a) Merge sort is faster than counting sort for all inputs b) Heap sort is stable c) Quick sort uses O(n) extra space d) Counting sort is a comparison-based sort
`a) false, if range is small then counting is faster`
`b) false, does not preserve order of equal element`
`c) false`
`d) false`


# Part 4: Graph Algo
Graph represent relationship between objects

## Graph Representations
### 1.Adjacency matrix
- 2D array: `matrix[i][j] = 1` if edge from i to j exist
- Space $O(V^2)$ where V = vertices
- Good for dense graphs, quick edge lookup
### 2.Adjacency List
- Array of lists: each vertex has a list of neighbor
- Space: $O(V+E)$ where E = edges
- Good for sparse graphs


## Graph Traversal Algo
## 1.BFS
- Uses queue (FIFO)
- Explore level by level
- Use for: shortest path in unweighted graph
- Complexity: $O(V+E)$
## 2.DFS
- Uses stack
- Explores as deep as possible before backtracking
- Use for: cycle detection, 
- **Complexity:** O(V + E)
## Edge classification
- Tree edge: part of dfs tree
- Back edge: point to ancestor (indicates cycle)
- Forward edge: points to descendants
- Cross edge: between subtrees

 


## Practice Questions - Part 4A: Graph Basics

**Question 21:** For a graph with 5 vertices and 8 edges:

- What's the space complexity of adjacency matrix?
`O(25)`
- What's the space complexity of adjacency list?
`O(13)`
- Which representation would you choose?
`Adjecency list`

**Question 24:** True or False: a) BFS finds the shortest path in weighted graphs b) DFS can detect cycles using back edges c) BFS uses a stack d) Both BFS and DFS have O(V + E) time complexity

`a)False`
`b)True`
`c)False, queue`
`d)True`

---

**Question 25:** Which algorithm (BFS or DFS) would you use for: a) Finding shortest path in an unweighted graph b) Detecting if a graph has a cycle c) Topological sorting d) Finding if two vertices are connected

`a)BFS`
`b)DFS`
`c)DFS cause we need to detect if it has a cycle`
`d)Unsure`


## Shortest Path Algo
### Algorithm Comparison

|Algorithm|Works With|Time Complexity|Use Case|
|---|---|---|---|
|**BFS**|Unweighted|O(V + E)|Shortest path when all edges = 1|
|**Dijkstra's**|Non-negative weights|O((V + E) log V)|GPS, routing, networks|
|**Bellman-Ford**|Any weights (even negative)|O(VE)|Detects negative cycles|

### Dijkstra's Algo
Key idea: greedy approach - always pick the closes unvisited vertex
Steps:
1. Init distances: start = 0, others = $\infty$
2. Pick vertex with smallest distance
3. Update distances to all neighbour
4.  Mark vertex as visited
5. Repeat untill all vertices are visited
DOES NOT WORK WITH NEGATIVE WEIGHT

### Bellman-Ford Algo
Key idea: relax all edges $V-1$ times
Steps:
1. Init distances: start = 0, others = $\infty$
2. Relax all edges $V-1$ times
	- For each edge (u, v, weight):
		- If dist\[u] + weight < dist\[v]
			- dist\[v] = dist\[u] + weight
3. Check for negative cycles





# Part 5: Dynamic Programming
## Concepts
DP works when a problem has
1. Optimal substructure - Optimal solution contains optimal solutions to subproblems
2. Overlapping subproblems - same subproblems are solved multiple times

Two Approaches

1. Top-down(Memoization) - Recursive + cache result
2. Bottom-up(Tabulation) - build table iteratively


Fibonacci 
Top-down with memoization
```python
def fib(n, memo ={}):
	if n in memo:
		return memo[n]
	if n <= 1:
		return n
	memo[n] = fib(n-1, memo) + fib(n-2, memo)
	return memo[n]	
```
Time: O(n) since each fib(i) is only calc once

Bottom up with Tabulation
```python
def fib(n):
	if n <= 1:
		return n
	dp = [0] * (n+1)
	dp[1] = 1
	for i in range(2, n+1)
		dp[i] = dp[i-1] + dp[i-2]
	return dp[n]
```
Time: O(n), Space: O(n)



Coin Change
**Problem:** Given coins \[1, 5, 6, 9] and amount 11, find minimum coins needed. **Recurrence Relation:** 
``` 
dp[i] = minimum coins to make amount i 
dp[i] = min(dp[i - coin] + 1) for each coin 
```


Knapsack Problem
**Problem:** Items with weights and values, maximize value without exceeding capacity.

**Example:** 
- Items: weights=\[2,1,3,2], values=\[12,10,20,15] 
- Capacity: 5

**Recurrence:** 
```python
dp[i][w] = max value using first i items with capacity w 
dp[i][w] = max( 
	dp[i-1][w], // don't take item i 
	dp[i-1][w-weight[i]] + value[i] // take item i 
	) 
```