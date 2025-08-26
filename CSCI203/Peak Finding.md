# Getting Started
----
If we have an array of numbers we can define a peak as any number that satisfies the following condition
- The first (or last) number is a peak if it is **greater than or equal to** its neighbor
- For any other position it is a peak if it is greater than or equal to both its neighbors
- Consider the following array
![[Pasted image 20250729141914.png]]
- The following peak are
![[Pasted image 20250729142014.png]]

# Finding Peaks
----
- There will always be at least one peak 
- The largest value in the array must be peak
- Using binary search
![[Pasted image 20250729144415.png]]

# Making the Problem Harder
----
![[Pasted image 20250729144934.png]]

## Possible Approach 
- Global max is always a peak
- If table has m rows and n columns we have to look at $m\times n$ and compare with 4 neighbors

## Steepest Ascent
- This algo takes an arbitrary elements in the array and compares it to its immediate neighbors
	- If its smaller than any neighbor, select the largest neighbor and repeat the process
	- Otherwise we have found a peak
- ![[Pasted image 20250729145443.png]]

## 2D Peak Finding
![[Pasted image 20250729150244.png]]
- Efficiency
	- Each complete iteration eliminates half of the data
	- Best case: we find a peak straight away
	- Worst case: we work down to a single column
	- Takes $\log_{2}n$ iterations