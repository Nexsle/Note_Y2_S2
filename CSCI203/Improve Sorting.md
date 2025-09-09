## String Search Problem
---
Example
- t = AGCATGCTGCAGTCATGCTTAGGCTA
- s = GCT
- s appear three times in T, starting from locations 6, 17, 23
![[Pasted image 20250909140253.png]]
$O(|s| \times |t|)$ number of comparisons

### Linear Time Search
---
Try hashing
- Hash s into hash_s
- Then we only need to compare the hash instead of the whole string s


### Rolling Hash
---
Define a hash function which, given h("harr") can compute h("arry") in constant time

Use ASCII code
Pick a random prime number > the size of the alphabet: 257

We now compute h("harr")
- $257^3 ∗ 104 + 257^2 ∗ 97 + 257^1 ∗ 114 + 257^0 ∗ 114 = 1,771,793,837$


Formula
- $𝑝^{𝑘−1} ∗ c_{1} + p^{k-2}*c_{2}+\dots+p*c_{k-1}+c_{k}$
- Remove the first char and add the last char
- $h'=p(h-qc_{i})+c_{j}$


# Decision Tree
---
A full binary tree that represents only the comparisons between elements
![[Pasted image 20250909145452.png]]
Leaves of the tree must cover all possible input permutation (n! case)

The tree has n! leaves
We know that the height is h = $\log_{2}^{(No. \ of \ leaves)}$
The longest path is at least $\log_{2}^{n!}$

# Bucket Sort
---
![[Pasted image 20250909151156.png]]
Assume all inputs are drawn from uniform distribution with average case O(n)

# Counting sort
---
Example
- A = \[4, 2, 2, 8, 3, 3, 1]
- Init C = \[0,0,0,0,0,0,0,0,0]
- Scan A
	- See 4 -> C\[4] = 1
	- See 2 -> C\[2] = 1
	- ....
- C = \[0,1,2,2,1,0,0,0,1]
Compute cumulative counts
C = \[0,1,2,2,1,0,0,0,1] => C=\[0,1,3,5,6,6,6,6,7]

Build Output (Stable)


# Radix Sort
---
Works on digital number
Use to sort n d-digit numbers where each digit is chosen from k possible values, takes O(d(n+k)) time if the counting sort it uses to takes O(n+k) time