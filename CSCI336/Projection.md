# Perspective and Parallel Projection
---
![[Pasted image 20250825100810.png]]

- Orthographic projection
	- Projectors orthogonal to projection surface
		- Projection lines form a 90 degree angle with the view plane![[Pasted image 20250825101550.png]]
	- Multi-view Orthographic projection
		- Projection plane parallel to principle face![[Pasted image 20250825101558.png]]

# Viewing
---
- 3D viewing
	- a right handed viewing coord system, with axes x, y, z relative to a right handed world coord system![[Pasted image 20250901084056.png]]
	- Orientation of the view plane and view plane normal vector N in the z direction
	- N can be obtained in the direction from reference point, $P_{ref}$ to the viewing origin, $P_{0}$

- Viewing transformation
	- Translate viewing coord origin to world coord origin
	- Apply rotation to align view axes with world axes, use unit vector u, v, n to form composite rotation matrix
	- Combine R and T for viewing transformation matrix![[Pasted image 20250901084725.png]]![[Pasted image 20250901084738.png]]


# Orthogonal Projection 
---
- Projection direction parallel to the z axis, projection is trivial
- View volume
	- How much of the scene to transfer to the view plane
	- An infinite orthogonal projection view volume only clips object description to four boundary plane
	- Limit the extent in the z direction by selecting two additional, near and far boundary planes


# Normalization Transformation
---
- Normalized device coordinates (NDC)
	- Representation where a graphic package is independent of the coordinate range of any specific output device
	- From an orthogonal projection view volume to the symmetric normalization cube![[Pasted image 20250901090316.png]]
```c++
glm::ortho(left, right, bottom, top, zNear, zFar)
```


# Perspective Projection
---
- View frustum
	- Finite view volume by specifying near and far clipping planes


# Viewport Transformation
---
```c++
glViewPort(x, y, z, h);
```