- Convexity 
	- If all interior angles are <180
- Convex if and only if
	- For any two points in the object all points on the line segment between these points are also in the object
![[Pasted image 20250811084608.png]]


- Polygon issues
	- OpenGL will only display polygons correctly if they are 
		- Simple
			- Edge cannot cross
	- If these condition are violated 
		- OpenGL will produce undesirable outcome



# Trigonometry
---
- Right-angled triangle
- ![[Pasted image 20250811091342.png]]
- ![[Pasted image 20250811091402.png]]


# Draw Circle
---
```c++
//init center
gVertices.clear();
gVertices.push_back(0.0f);
gVertices.push_back(0.0f);
gVertices.push_back(0.0f);

float slice_angle = M_PI * 2.0f / slices;
float angle = 0;
float x, y, z = 0.0f;

for(int i = 0; i <= slices; i++)
{
	x = radius * cos(angle) * scale_factor;
	y = radius * sin(angle);

	vertices.push_back(x);
	vertices.push_back(y);
	vertices.push_back(z);

	angle += slice_angle
}
```


# Interpolation
---
![[Pasted image 20250811094814.png]]
- Before the vertex shader is transfer in to the fragment shader, interpolation happens
![[Pasted image 20250811094905.png]]


# Interleaved Vertex Attributes
----
![[Pasted image 20250811100438.png]]
