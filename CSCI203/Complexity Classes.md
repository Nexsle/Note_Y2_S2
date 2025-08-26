- Looking at a simple problem: finding a telephone number
- In this case, n, the problem size, is the number of entries, in the directory

# Problem 1
- Question: "What is the first name in the book?"
- Does the size of the book matter: NO
- The problem independent of n
- The complexity class of this problem is **constant**

# Problem 2
- Question: "The phone number of Peter Dowe?"
- Now the size of n does matter
- A simple algo might be:
- ![[Pasted image 20250729152447.png]]
- The approach we use to find the right page eliminates roughly all of the reamining pages at each itereation
- This means that, as n grows in size the number of iterations required to find the correct page grows more slowly
- The complexity is related to $\log n+ c$

# Problem 3
- Question: "Who has the phone number 42743555"
- Names are in order but numbers are not
- ![[Pasted image 20250729153633.png]]

# Problem 4
- Question: "Will you rearrange the entries in increasing order of phone number"
- The best one you should be familiar with so far, is quicksort
![[Pasted image 20250729153835.png]]
- Each partitioning takes linear time in the number of entries
- The algo as a while takes $n\log n$ steps

# Problem 5
- Question: "Every number in the book has an extra zero at the end, We have already printed the books. Can you cover each of the extra zeros with white-out"
![[Pasted image 20250729154052.png]]
- There are n entries
- There are n books
- The total number of iterations is $n\times n=n^2$
- The complexity is **quadratic**

# Comparing Classes
![[Pasted image 20250729154207.png]]![[Pasted image 20250729154229.png]]
