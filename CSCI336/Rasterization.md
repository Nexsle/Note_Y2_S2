Converts vertices into screen space
![[Pasted image 20251020093205.png]]
Determining which pixels that are inside primitive specified by a set of vertices

# Line drawing algo
![[Pasted image 20251020093426.png]]
Given two endpoints and want to find set of pixel that will represent the line![[Pasted image 20251020093648.png]]

## Digital Differential Analyzer
Line sampled at unit interval steps along one axis

## Bresenham's line algo


# Polygon Fill Algo
## Scan-line polygon fill
We count the edge, odd edge we start drawing, even we turn off
![[Pasted image 20251020095918.png]]

We count vertexes as 2 edges

Problem
![[Pasted image 20251020100110.png]]
Scan line b will be wrong
