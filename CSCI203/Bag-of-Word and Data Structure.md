# Definition
---
A text representation model that treats a docs as a collection of words
Ignore word order and grammar, only counts word frequency

Step by step how to Build a BoW
- Build a vocabulary = all unique words in the corpus
- For each docs count word frequency
- represent the docs as a vector over the vocab


# Count-min Sketch
---
![[Pasted image 20250909161008.png]]
Look up counters at hashed positions:
 - Row 1: C\[1, h1("dog")] = 3
 - Row 2: C\[2, h2("dog")] = 3
 - Row 3: C\[3, h3("dog")] = 2
Estimate frequency
- f^("dog")=min(3,3,2)=2
- 