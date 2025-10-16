# DP Algo
Developing steps to an optimization problems

1. Identify how an optimal solution can be built from smaller sub-solutions
2. Recursively define the value of an optimal solution
3. Use a bottom up(tabulation) or top down (memorization) approach
4. Construct an optional solution

---
# Memoization
The recognition that we only need to perform a given calculation once is central to Dynamic Programming

```
memo: dictionary = {}
Procedure fibDP(n: integer): integer
	f: integer
	if (n in memo) return memo[n]
	if (n<=2) then
		f = 1
	else
		f = fibDP(n-1) + fibDP(n-2)
	fi
	memo[n]=f
	return f
End procedure fibDP
```


---
# Bottom up
The bottom up approach still involves solving the same set of sub problems, what changes is the order

Memory free fibonacci

```c++
Procedure fibSmall(n: integer): integer
	if n < 2 then
		return n
	end if
	prev: integer = 0 // Holds F(k-1); starts at F(0)
	f: integer = 1 // Holds F(k); starts at F(1)
	k: integer = 2 // compute up to F(n), beginning from k = 2
	
	while k <= n do // f = F(k-1) and prev= F(k-2)
		f = f + prev // f becomes F(k-1) + F(k-2) = F(k)
		prev= f - prev // prev becomes old f = F(k-1)
		k = k + 1
	end while
	return f
end Procedure
```


---
# Coin-row problem
F(n) is max amount that can be picked up from row of n coins
- Those without last coin - the max amount is 
	- F(n) -> F(n-1)
- Those with the last coin - the max is
	- F(n) -> Cn + F(n-2)

Thus we have
F(n) = max{Cn + F(n-2), F(n-1)}


---
# Change making problem
If we pick $d_{j}$ to the amount $n-d_{j}$ ($d_{j}$ is index from 0 to n) such that $n\geq d_{j}$, then $F(n-d_{j})+1$

$F(n)=min\{ F(n-d_{j}) \}+1 \ for \ n>0$



 