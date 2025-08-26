# Insertion sort
----
- Strategy
	- Start with the second element in the list
	- insert it in the right place in the preceding list
	- repeat with the next unsorted element
	- keep going until we have placed the last element in the list
![[Pasted image 20250805141008.png]]

- to sort a list of n numbers requires n-1 iteration
- in the worst case this means comparing with every such element
- Typically the entire sort will require around $\frac{n^2}{2}$ comparison

# Merge sort
---
- Approach
	- it uses a second array to hold the intermediate result
	- it works recursively by dividing the unsorted array into two parts and merging them in order
- Because this procedure divides all the way down before merging backup, the final result is a sorted array

- At each level, merge operates on all n items in the array
- as each level divides the array in two, there are $\log n$ levels


# Heaps
----
- Heap is an essentially complete binary tree with an additional property
- Max-heap: the value in any node is less than or equal to the value in its parent node
- Min-heap: the value in any node is greater than or equal to the value in its parent node
![[Pasted image 20250805143738.png]]

- If we made a non heap how can we convert it into one
- We need two basic functions to manage heaps
	- Sift up: insert a new leaf into the correct position
	- Sift down: insert a new root element into the correct position
![[Pasted image 20250805144902.png]]


# Heapsort
---
- Uses the property of a heap 
- Strategy
	- 1.Convert the array into a heap
	- 2.Repeatedly:
		- a. Swap the first and last elements of the heap
		- b. Reduce the size of the heap by 1
		- c. Restore the heap property of the smaller heap



# Time Efficiency
----
![[Pasted image 20250805154036.png]]
 ![[Pasted image 20250805154736.png]]
 