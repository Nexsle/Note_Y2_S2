- Let us assume that we need to store a large number, N of text strings
- How can we store these string so that 
	- We can use a minimum amount of storage
	- We can access any string quickly and efficiently
	- We avoid the overhead of dynamic memory

# Option 1
----
- Using an array of strings
	- array\[1..N] of string
- Minimum amount of storage?
	- Yest
- Access any string quickly and efficiently?
	- Yes
- Avoid dynamic memory
	- No-strings are dynamic


# Option 2
----
- Using doubly dimensioned array of char
	- array\[1..N, 1..L] of char
- Minimum amount of storage
	- No we use N x L char 
- What if all of the strings are 1 char long except for 1
	- which is 1000000 char long?
- Access quickly?
	- Yes
- Avoid dynamic mem?
	- Yes


# Option 3
---
- Use 3 array
	- text\[], a char array which stores the strings packed tightly together
	- start\[], an integer array which stores the starting pos of each string in text\[]
	- length\[], an integer array which contains the length of each string in text\[]



# Example
---
“The quick brown fox jumps over the extraordinarily lazy dog”

- Text contains 10 words so set N to 10
- Average length is 5 so set A to 5

![[Pasted image 20250805135324.png]]


- Minimum amount of storage?
	- Nearly - we use N x A char plus 2 x N integers which is a bit more than the minimum required
- Access any string quickly and efficiently
	- Yes, the ith entry is text\[j..k] where
		- j = start\[i]
		- k=start\[i] + length\[i] -1 
- Avoids dynamic mem?
	- Yes


# Option 3a
----
- store the end pos of each string rather than its length
- uses no more memory and we can now access the ith string as text\[start\[i]..end\[i]]


# Option 3b
----
- we see that end\[i] = start\[i+1] - 1
- we can use this to save more mem
- The ith string is now text\[start\[i]..start\[i+1]-1]
- 