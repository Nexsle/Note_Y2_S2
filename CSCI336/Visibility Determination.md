# Back face detection
- A polygon is facing forward if 
	- $-90^o\leq \theta \leq 90^o$
![[Pasted image 20251013095645.png]]
- Easier to test using dot product
	- $n \times v\geq 0$

Polygon winding
- Right hand system
	- Polygon is backface if $C\leq 0$
![[Pasted image 20251013095854.png]]

Depth sort method
- can be considered to be an object space approach
- General idea
	- Sort polygons in order of decreasing depth 
	- Scan convert polygons in order starting from the furthest


Depth buffer method
![[Pasted image 20251013101400.png]]
- Has the same resolution as the frame buffer and stores floating point numbers
- Typically carried out in normalized coords

1. Initialise depth buffer and color buffer for all position
	- `dpethBuff(x,y) = 1.0`
	- `colorBuff(x,y)= backgroundColor`
2. For each polygon in the scene
	- For each projected (x, y) pixel position of polygon, calculate the depth z
	- If z < depthBuff(x, y) then compute and set the surface color at that position
		- `depthBuff(x,y) = z`
		- `colorBuff(x,y) = surfColor(x,y)`
