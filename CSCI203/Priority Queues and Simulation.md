# Stack 
---
- A stack is a data structure which holds multiple elements of a single type
- Elements can be removed from a stack only in the reverse order to that in which they were inserted
- ![[Pasted image 20250812133941.png]]


- push(elt)
	- Pushing an element on the stack
- pop(elt)
	- Removing an element from the stack
- isFull()
	- check if stack is full
- isEmpty()
	- check if stack is empty

# Queues
---
- A queue is a data structure which holds multiple elements of a single type
- Elements can be removed from a queue only in the order in which they were inserted
![[Pasted image 20250812134352.png]]

- enqueue(elt)
	- add an item to the queue
- dequeue(elt)
	- remove an item from the queue
- isFull()
	- check if the queue is full
- isEmpty()
	- check if queue is empty


# Heaps
---
- A heap is an essentially complete binary tree with an additional property
- The value in any node is less thana or equal to the value in its parent node
- ![[Pasted image 20250812134636.png]]

- siftUp: insert a new leaf into the correct position
- siftDown: insert a new root element into the correct position
- Each compares an element of the heap with other elements

# Sorting Algorithms
---
- Insertion sort
	- Consider the list has two parts one is sorted and another is unsorted
	- Complexity: $O(n^2)$![[Pasted image 20250812135024.png]]

- Merge sort
	- Complexity: $n\log n$![[Pasted image 20250812135159.png]]

- Heapsort




# Priority Queues
---
- A priority queue is a data structure for maintaining a set of elements, each with an associated value called a key
- In a normal queue, elements come off in first in first out order, so the first element in the queue is the top element
- In a priority queue, the element with the largest key is always on the top, no matter what order it or the other elements were inserted

# Priority Queues - Basic Operation
---
- insert(pQueue, elt)
	- Insert an element into the queue and place it in the right position in the queue
- remove(pQueue, elt)
	- Extract the element with top priority and remove it from the queue
	- adjust the queue as needed


# Priority Queue - Heap Implementation
---
- We can use a max heap to improve the implementation, since a heap always keeps its maximum element in the first element
- ![[Pasted image 20250812140656.png]]


# Simulation
----
- Continuous
	- Time is broken into discrete chunks
	- Usually used to model a continuous process
- Discrete
	- Time can take any value
	- Usually used to model discrete events


# The Algorithms
----
- Starting to design the algorithm
- Procedures
	- Initialise the simulation
	- process an arrival
	- process a service completion
	- finish the ismilation
- Initialise the simulation
	- time = 0
	- busy = false
	- queue = empty
	- read next_arrival, next_service
- set up for statistic collections

# Single Queue & Multi-server
---
- Keeping track of servers 
- Two possible solutions
	- An array of servers with busy\[i] and end_time\[i]
	- A heap of end times