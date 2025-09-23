A graph, G = (V, E) consists of a set V of points, called vertices or nodes, and a set of E, edges
![[Pasted image 20250916135202.png]]

## Sparse vs dense graph
---
- Sparse
	- Those for which |E| is much less than $|V|^2$
- Dense
	- Those for which |E| is close to $|V|^2$

## Abstract Notation
---
$G = \{ Adj(v_{1}),Adj(v_{2}),\dots,Adj(v_{|V|}) \}$
Adj(v): is the set of vertices directly reachable from vertex v


## Adjacency List
---
An adjacency list, L of length |V| 
![[Pasted image 20250916141029.png]]


## Adjacency Matrix
---
An adjacency matrix is a $|V| \times|V|$ array containing zeros and ones
- |V| is the number of vertices in V
- A 1 is stored in location: (i, j) if there is an edge between $v_{i}$ and $v_{j}$
- A 0 is stored if not
If G is a non directed graph, the array is symmetric

![[Pasted image 20250916142056.png]]


## Breadth-First Search(BFS)
---
Our goal is to list all the vertices that are reachable from one starting node
$O(|V|+|E|)$ time

Strategy
- List all nodes reachable from s in 0 moves
- List all nodes reachable from s in 1 moves
- ....

- BFS will always find the shortest path from s to x


## Depth First Search
---
Goal is same as BFS
The edges traversed in performing a DFS or BFS form a tree

