- A binary tree is a tree in which each node has a maximum of two child nodes, the left child and the right child
- ![[Pasted image 20250819135440.png]]
- **Level** of a node represents the generation of a node. If the root node is at level 0, so its next child node is at level 1
- **Depth** of a node is the length of the simple path from root to the node
- **Height** of a tree is a the length of the longest simple path from the root to a leaf
- **Height** of a node is the maximum depth of any node in the subtree rooted at that node
- **Key** represents a value of a node based on which a search operation is to be carried out


# Binary Search Tree
---
- Insert
	- Insert an element in a tree
- Find 
	- Searches an element in a tree
- Delete
	- Delete an element in a tree
- Traversals
	- Preorder - Traverses a tree in a pre-order manner, i.e., root , left, right
	- Inorder - Traverses a tree in an in-order manner i.e., left root right
	- Postorder - Traverses a tree in a post-order manner, i.e., left right root


# Building a BST
---
- To build a BST - we add nodes, one at a time by:
	- Searching the existing BST for the value to be inserted
	- If, the value is not found
		- create the new node
		- add the new node to the tree as the appropriate child of the last node examined


# Sorting with BSTs
---
- If we perform an in order traversal of a binary search tree, the nodes of the tree will be listed in sorted order
- ![[Pasted image 20250819143739.png]]


# Balancing a BST
---
- Operations on BSTs are only O(log(n)) for balanced trees
- Try "left and right subtree must be of the same height"
	- this is easy to achieve but not very useful
	- too soft
- Try "every node must have left and right subtree of the same height"
	- This is impossible unless the tree is complete


# AVL Trees
---
- The balancing condition of AVL tree;
	- Balance factor = height(left subtree) - height(right subtree)
	- The height of empty tree is defined as -1
- It should be -1, 0 or 1. Other than this will cause restructuring the tree. Balancing performed is carried in the following operations
	- Right rotation (RR)
	- Left rotation (LL)
	- Right left double rotation(RL)
	- Left right double rotation(LR)


# Right rotation (RR)
---
![[Pasted image 20250819145401.png]]


# 2-3-4 Tree
---
![[Pasted image 20250826135555.png]]
- A 2-3-4 balanced tree have three types of nodes
	- 2-nodes has one key and two child nodes
	- 3-node has 2 keys and three child
	- 4-node has three key and 4 child node

- Search 
	- compare the item to be searched with the keys of the node
	- Move to the appropriate direction
- Insertion
	- A node cannot hold more than 3 keys, if full before insertion, we split the node so that the new node can be inserted
- Deletion
	- Depending upon the location of the node containing the target to be deleted

- The tree has the following properties
	- Every internal node has between two and four children
	- the keys within each node are ordered from the smallest to largest
	- Internal node have one less key than they have children
	- All the leaves of the tree are at the same depth



# Insertion into a 2-4 Tree
---
- Find leaf where the item is to be inserted
- Insert the item
- Update node
	- Into 2-node -> 3-node
	- into 3-node -> 4 node
	- into 4-node -> 5 node
		- If an immediately adjacent sibling is not full, send a key from the parent down to this sibling
		- if all such siblings are full, split the node into two by passing the median key up to the parents


# 2-4 Tree Efficiency
---
- Height: O($\log n$)
- Searching:
	- Each node checked takes O(1)
	- Search takes O($\log n$)
- Insertion
	- Split takes O(1)
	- At most $\log n$ splits
	- Insertion takes O($\log n$)
- Deletion
	- Merge takes O(1)
	- at most $\log n$
	- deletion takes O$(\log n)$


# Quadtrees
---
- most often used to partition a 2D space
- Each internal node has exactly four children![[Pasted image 20250826145606.png]]


# Octree
---
- A tree data  structure where each internal node has exactly 8 children
- it is primarily used for spatial partitioning in three dimensional space, recursively subdividing a bounding cube into 8 congruent sub-cubes

# K-D trees
---
- Recursively split P into two sets of the same size, alternatingly along a vertical or horizontal line
- through the median in x or y coordinates
[K-Dimensional Tree Showcase](https://medium.com/@katyayanivemula90/what-is-a-k-dimensional-tree-8265cc737d77)

- Search complexity
	- A kd tree for a set of n points in the plane can be constructed in $O(n\log n)$ time and uses $O(n)$ space
	- A rectangular range query can be answered in $O(\sqrt{ n }+k)$ where k = # reported points



