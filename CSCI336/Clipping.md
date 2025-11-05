Clip scene against view volume
- Remove parts of scene not within view volume
![[Pasted image 20251020083817.png]]

2D vs 3D
![[Pasted image 20251020083835.png]]

The purpose of clipping
- For preventing activity in one window from affecting pixels in other windows
- Mathematical overflow and underflow because we calculate till infinity
- Rasterization is computationally expensive, so we only rasterize after clipping

## Point Clipping
![[Pasted image 20251020084433.png]]

For point P = (x, y)
check
$xw_{min} \leq x<xw_{max}$
$yw_{min} \leq y\leq yw_{max}$


## Line Clipping
![[Pasted image 20251020085117.png]]
For case C, we know that both point of C lie out side of $xw_{max}$ and $yw_{max}$

![[Pasted image 20251020085235.png]]
Line segment can be represented as 
$x=x_{0}+u(x_{end} - x_{0})$
$y=y_{0}+u(y_{end}-y_{0})$
$0\leq u\leq1$

if u in range of \[0,1] then line intersects border



# Cohen-Sutherland Clipping Algorithm
Steps

1. If both endpoints 0000, ACCEPT
2. Else If (code1 & code2) != 0, REJECT
3. Else, {Clip line against one viewport boundary}
4. Assign the new endpoint with a 4-bit region code
5. Go to 1
![[Pasted image 20251020090803.png]]
![[Pasted image 20251020090809.png]]
![[Pasted image 20251020090819.png]]
![[Pasted image 20251020090857.png]]

## Hodgman-Sutherland Polygon clipping
![[Pasted image 20251020091412.png]]
- Parse all polygon edges either in clockwise or counter clockwise
![[Pasted image 20251020091545.png]]

- Potential issue
![[Pasted image 20251020091649.png]]


# Weiler-Atherton polygon clipping
Use to clip either convex or concave area filled polygons
1. Process edges until \[in -> out] pair of vertices encountered
2. From exit intersection point, trace clipping boundary until another intersection point
	- if point was previously processed, goto next step
	- else continue processing edges until a previously processed vertex is encountered
3. Form the vertex list for this section of clipped fill area
4. Return to exit intersection point and continue processing the polygon edges


![[Pasted image 20251020092152.png]]

