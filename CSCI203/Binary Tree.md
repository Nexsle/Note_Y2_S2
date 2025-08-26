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

# Left rotation(LL)
---
