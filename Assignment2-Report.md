# High-level Description
---

## Dijkstra's Algorithm

**ALGORITHM**: Shortest Path using Dijkstra

```
DIJKSTRA(start, goal):
    initialize all distances to INF
    initialize all vertices as unvisited
    distance[start] = 0
    insert start into min-heap with priority 0

    while heap is not empty:
        current = extract vertex with minimum distance from heap

        if current is already visited:
            continue

        mark current as visited
        increment expandedNodes

        if current == goal:
            break  // early termination

        for each edge from current to neighbor:
            newDist = distance[current] + edge.weight

            if neighbor not visited and newDist < distance[neighbor]:
                distance[neighbor] = newDist
                parent[neighbor] = current

                if neighbor in heap:
                    decrease priority of neighbor to newDist
                else:
                    insert neighbor into heap with priority newDist

    reconstruct path using parent array
    output path, distance, and expandedNodes
```

**Key Components**:
- **Min-Heap (Priority Queue)**: Custom implementation using array-based binary heap
- **Distance Array**: Stores shortest distance from start to each vertex
- **Parent Array**: Stores predecessor for path reconstruction
- **Visited Array**: Tracks which vertices have been processed

---

## A* Algorithm

**ALGORITHM**: Shortest Path using A* with Euclidean Heuristic

```
A_STAR(start, goal):
    initialize all g-scores to INF
    initialize all f-scores to INF
    initialize all vertices as unvisited
    gScore[start] = 0
    fScore[start] = heuristic(start, goal)  // Euclidean distance
    insert start into min-heap with priority fScore[start]

    while heap is not empty:
        current = extract vertex with minimum f-score from heap

        if current is already visited:
            continue

        mark current as visited
        increment expandedNodes

        if current == goal:
            break  // early termination

        for each edge from current to neighbor:
            newG = gScore[current] + edge.weight

            if neighbor not visited and newG < gScore[neighbor]:
                gScore[neighbor] = newG
                fScore[neighbor] = gScore[neighbor] + heuristic(neighbor, goal)
                parent[neighbor] = current

                if neighbor in heap:
                    decrease priority of neighbor to fScore[neighbor]
                else:
                    insert neighbor into heap with priority fScore[neighbor]

    reconstruct path using parent array
    output path, gScore[goal], and expandedNodes
```

**Evaluation Function**:
$$f(v) = g(v) + h(v)$$
where:
- $g(v)$ = actual distance from start to vertex $v$
- $h(v)$ = Euclidean distance from vertex $v$ to goal
- $f(v)$ = estimated total distance from start → $v$ → goal

**Heuristic Function**:
$$h(v) = \sqrt{(x_v - x_{goal})^2 + (y_v - y_{goal})^2}$$

**Admissibility**: The Euclidean heuristic is admissible because:
- The straight-line distance between two points is always ≤ any path between them
- Therefore $h(v)$ never overestimates the actual remaining distance
- This guarantees A* finds the optimal path

**Consistency**: The Euclidean heuristic is consistent because:
- For any edge $(u, v)$ with weight $w$: $h(u) \leq w + h(v)$
- Triangle inequality holds: straight-line distance from $u$ to goal ≤ distance from $u$ to $v$ + distance from $v$ to goal
- Consistency implies admissibility and ensures optimal path finding

---

## DFS Algorithm for Longest Path

**ALGORITHM**: Longest Simple Path using DFS with Backtracking

```
DFS(start, goal):
    initialize all vertices as unvisited
    visited[start] = true
    currentPath[0] = start
    longestDistance = -1

    DFS_RECURSIVE(start, goal, 0, visited, currentPath, 1,
                  longestDistance, longestPath, longestPathLength)

    output longestPath and longestDistance

DFS_RECURSIVE(current, goal, currentDist, visited, currentPath, pathLen,
              longestDist, longestPath, longestLen):

    if current == goal:
        if currentDist > longestDist:
            longestDist = currentDist
            longestLen = pathLen
            copy currentPath to longestPath
        return

    for each edge from current to neighbor:
        if neighbor is not visited:
            visited[neighbor] = true           // Mark
            currentPath[pathLen] = neighbor    // Add to path

            DFS_RECURSIVE(neighbor, goal, currentDist + edge.weight,
                         visited, currentPath, pathLen + 1,
                         longestDist, longestPath, longestLen)

            visited[neighbor] = false          // Backtrack - unmark

    return
```

**Search Strategy**:
- **Exhaustive Search**: Explores all possible simple paths from start to goal
- **Backtracking**: After exploring a path, unmarks vertices to allow them in other paths
- **No Pruning**: Must check all paths to ensure finding the longest one

**Complexity Analysis**:
- **Worst Case**: $O(V!)$ - factorial time complexity
  - In a complete graph, there are $V!$ possible vertex orderings
  - Must explore all simple paths to guarantee finding the longest
- **Best Case**: $O(V + E)$ when only one path exists
- **Space**: $O(V)$ for recursion stack depth (maximum path length is $V-1$)

**Observed Performance**:
- For the sample graph (20 vertices, 100 edges):
  - Found longest path of length 1595.000
  - Path visits all 20 vertices
  - Execution time < 1 second (sparse graph with limited branching)

---

# Complexity Analysis
---

## Dijkstra's Algorithm

**Time Complexity**: $O((V + E) \log V)$
- **Heap Operations**: Each vertex extracted once: $O(V \log V)$
- **Edge Relaxation**: Each edge processed once: $O(E \log V)$ (heap decrease-key)
- **Total**: $O((V + E) \log V)$

**Space Complexity**: $O(V)$
- Distance, parent, visited arrays: $O(V)$
- Min-heap: $O(V)$

**Justification**:
Binary heap operations (insert, extract-min, decrease-key) are $O(\log V)$. Since we extract $V$ vertices and relax $E$ edges, the total complexity is $O((V + E) \log V)$.

---

## A* Algorithm

**Time Complexity**: $O((V + E) \log V)$
- Same as Dijkstra in worst case
- **Best Case**: Can be much faster with good heuristic

**Space Complexity**: $O(V)$
- gScore, fScore, parent, visited arrays: $O(V)$
- Min-heap: $O(V)$

**Justification**:
Same operations as Dijkstra, but heuristic guides search toward goal. In worst case (poor heuristic), complexity matches Dijkstra. With good heuristic, explores fewer nodes.

---

## DFS for Longest Path

**Time Complexity**: $O(V!)$ worst case, $O(V + E)$ best case
- **Worst**: Must explore all $V!$ permutations in complete graph
- **Average**: Depends on graph density and connectivity
- **Best**: Linear when only one path exists

**Space Complexity**: $O(V)$
- Recursion stack: $O(V)$ depth
- Path arrays: $O(V)$
- Visited array: $O(V)$

**Justification**:
Exponential because we must explore all simple paths. Each path can have up to $V$ vertices, and branching factor can be up to $V-1$ at each step.

---

## Comparison: Dijkstra vs A*

**Expanded Nodes**:
- **Dijkstra**: 5 nodes expanded
- **A***: 2 nodes expanded (60% reduction!)

**Why A* Outperforms Dijkstra**:
1. **Heuristic Guidance**: A* uses Euclidean distance to prioritize vertices closer to goal
2. **Informed Search**: $f(v) = g(v) + h(v)$ focuses exploration toward goal
3. **Early Pruning**: Vertices far from goal get lower priority, reducing expansions

**When A* Excels**:
- Graphs with clear spatial structure (like our coordinate-based graph)
- When goal is in a specific direction from start
- When heuristic is accurate (admissible and consistent)

**When A* ≈ Dijkstra**:
- Complete graphs where all vertices are equally likely
- Poor or zero heuristic ($h(v) = 0$ reduces A* to Dijkstra)
- Goal requires exploring most of the graph anyway

**Result**: For this sample, A* found the same optimal path (length 85.000) but with 60% fewer node expansions, demonstrating the power of informed search.

---

# Data Structures Used
---

## 1. Dynamic Arrays

**Purpose**: Store vertices, edges, and algorithm state
- `Vertex* vertices`: Stores vertex labels and coordinates
- `Edge** adjList`: Adjacency list (array of edge arrays)
- `int* adjCount`: Edge count per vertex
- `int* reverseMap`: Maps array indices to vertex labels

**Reason**:
- No STL allowed, so manual dynamic allocation required
- Allocates exactly `vertexCount` elements (not fixed 1000)
- Memory efficient: only allocates what's needed
- $O(1)$ access time for lookups

---

## 2. Min-Heap (Priority Queue)

**Purpose**: Efficiently extract vertex with minimum priority in Dijkstra and A*

**Implementation**:
- Array-based binary heap
- `HeapNode* heap`: Stores (vertex, priority) pairs
- `int* heapPos`: Reverse lookup - position of vertex in heap

**Operations**:
- `heapInsert(vertex, priority)`: $O(\log V)$
- `heapExtractMin()`: $O(\log V)$
- `heapDecreaseKey(vertex, newPriority)`: $O(\log V)$
- `heapifyUp/Down()`: Maintain heap property

**Reason**:
- Priority queue essential for Dijkstra/A*
- Min-heap provides $O(\log V)$ operations vs $O(V)$ linear search
- `heapPos` array enables $O(1)$ vertex lookup for decrease-key
- Custom implementation required (no STL allowed)

---

## 3. Adjacency List

**Purpose**: Represent directed weighted graph

**Structure**:
- For each vertex $v$, `adjList[v]` points to array of outgoing edges
- `adjCount[v]` stores number of edges from $v$

**Reason**:
- **Space Efficient**: $O(V + E)$ vs $O(V^2)$ for adjacency matrix
- **Iteration Efficient**: Only iterate through edges that exist
- **Sparse Graphs**: Sample has 20 vertices, 100 edges (not dense)
- For each vertex, directly access all neighbors in $O(\text{degree}(v))$

---

## 4. Boolean Arrays

**Purpose**: Track vertex state
- `bool* visited`: Mark vertices as processed (Dijkstra/A*/DFS)

**Reason**:
- $O(1)$ lookup and update
- Minimal space: 1 byte per vertex
- Essential for cycle prevention in DFS

---

## 5. Path Arrays

**Purpose**:
- `int* parent`: Store predecessor for path reconstruction (Dijkstra/A*)
- `int* currentPath`: Current path being explored (DFS)
- `int* longestPath`: Best path found so far (DFS)

**Reason**:
- Parent array enables $O(V)$ path reconstruction after algorithm completes
- Path arrays in DFS track and compare different paths during exploration
- Simple array structure with $O(1)$ access

---

# Compilation
---
```
Compilation Command:
g++ -o assignment2 main.cpp Graph.cpp -std=c++11

Execution:
./assignment2
Enter filename: a2-sample.txt
```

---

# Outputs
---
```
Enter filename: a2-sample.txt
Vertices: 20, Edges: 100
Start: 2, Goal: 13
Euclidean distance (start-goal): 77.878

###### Shortest path by Dijkstra's Algorithm: ######
Shortest path: 2 13
Shortest length: 85.000
Number of expanded nodes: 5

###### Shortest path by A* Algorithm: ######
Shortest path: 2 13
Shortest length: 85.000
Number of expanded nodes: 2

###### Longest path by DFS Algorithm: ######
Longest path: 2 17 9 16 4 18 14 8 6 19 3 12 5 20 1 15 11 7 10 13
Longest length: 1595.000
```

---

# Analysis and Observations
---

## Shortest Path Results

**Path Found**: 2 → 13 (Direct edge)
- **Length**: 85.000
- **Euclidean Distance**: 77.878
- **Explanation**: Direct edge weight (85.000) > straight-line distance, which is expected since edge weights satisfy $w \geq$ Euclidean distance

**Algorithm Efficiency**:
- **Dijkstra**: Expanded 5 nodes before reaching goal
- **A***: Expanded only 2 nodes (60% reduction)
- Both found the optimal path with same length

## Longest Path Results

**Path Found**: 2 → 17 → 9 → 16 → 4 → 18 → 14 → 8 → 6 → 19 → 3 → 12 → 5 → 20 → 1 → 15 → 11 → 7 → 10 → 13
- **Length**: 1595.000
- **Visits**: All 20 vertices (Hamiltonian path)
- **Characteristic**: No vertex repeated, satisfying the simple path constraint

**Observation**: The longest simple path visits every vertex exactly once, demonstrating the exhaustive nature of the DFS search.

## Performance Comparison

| Algorithm | Path Length | Expanded Nodes | Time Complexity |
|-----------|-------------|----------------|-----------------|
| Dijkstra  | 85.000      | 5              | $O((V+E)\log V)$ |
| A*        | 85.000      | 2              | $O((V+E)\log V)$ |
| DFS       | 1595.000    | N/A*           | $O(V!)$         |

*DFS explores paths, not individual node expansions

The results demonstrate:
1. **Heuristic Value**: A* reduced node expansions by 60% using Euclidean heuristic
2. **Optimality**: Both Dijkstra and A* guaranteed optimal shortest path
3. **Problem Difficulty**: Longest path requires exponential search, but completes quickly on sparse graph
