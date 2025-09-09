# Dictionary
---
### Implementation 0: The direct access table
![[Pasted image 20250902141354.png]]

- Simply a big array where the index of the array is the key

### Fixing the problems
- Problem 1: keys must be non-negative int
- Solution
	- define a function prehash(key)
		- Function when given a key need to store returns a non negative int



# Hashing
---
![[Pasted image 20250902142948.png]]


### Open addressing
- alternative to Chaining
- We wish to hash n items into an array with M slots
- clearly $m\geq n$
- Insert into the table using an iterative tech known as probing

### Probing
- Linear probing
```
If slot h(key) is taken: Try h(key) + 1, h(key) + 2, h(key) + 3... (wrap around at end of table)
```
**Pros:** Simple, cache-friendly  
**Cons:** Creates clusters (primary clustering)
![[Pasted image 20250902155021.png]]


- Double hashing
```
Use two hash functions: h₁(key) and h₂(key)
If slot h₁(key) is taken:
Try h₁(key) + h₂(key), h₁(key) + 2×h₂(key), h₁(key) + 3×h₂(key)...
```

```
Key = "apple"
h₁("apple") = 5, h₂("apple") = 3, table size m = 10

Attempt 0: p("apple",0) = (5 + 0×3) mod 10 = 5
Attempt 1: p("apple",1) = (5 + 1×3) mod 10 = 8
Attempt 2: p("apple",2) = (5 + 2×3) mod 10 = 1  ← wraps around
Attempt 3: p("apple",3) = (5 + 3×3) mod 10 = 4
```

