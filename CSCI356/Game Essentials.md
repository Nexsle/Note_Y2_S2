- Vectors
	- Can be used to represent a position in a vector space
		- Sometimes called a position vector
		- Specifies a unique position in 3D vector space

- Unity
	- Vector classes
		- Vector2, Vector3, Vector4
	- Create vector using a constructor
		- Vector3 vec = new Vector3(2, 8, 0);
	- Setting a GameObject's position
		- transform.position = new Vector3(0, 1, 0)


# Vector Operation
----
- Displacement
- ![[Pasted image 20250813094615.png]]

- Addition and subtraction
![[Pasted image 20250813094644.png]]

- Split into two element
	- Magnitude(length of vector)
		- $|\vec{u}|=\sqrt{ u_{x}^2+u^2_{y}+u^2_{z} }$
		- float length = vec.magnitude
	- Direction
		- Normalizing a vector
		- $\vec{u}=\frac{\vec{u}}{|\vec{u}|}$
		- Vector3 unitVector = vec.normalized

- Multiplication
![[Pasted image 20250813095117.png]]


- Distance
![[Pasted image 20250813095137.png]]

- Dot product
![[Pasted image 20250813095504.png]]


- Cross product
![[Pasted image 20250813095644.png]]
