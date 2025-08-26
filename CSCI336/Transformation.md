# Coordinate system
---
- Transformation matrices
![[Pasted image 20250818084038.png]]

- Modelling transformation
	- Operations applied to geometric description of an object
	- Affine transformations
		- Lines are preserved


# Point and Vectors
----
- Points: a location in space
- Vectors:
	- quantity with magnitude and direction
	- no fixed position in space

- Vector datatype
	- Dimensions 2, 3 ,4
	- Typically used for coordinates, vectors, colors
```c++
#include <glm/glm.hpp>
using namespace glm;
ivec2 VectorA;   // integer vector
uvec3 VectorB;   // unsigned int vector
vec4 VectorC // floating point vector
```


- Vector operations
	- Multiply by scalar
		- Alter magnitude
	- Inverse/negate
		- Same magnitude, opposite direction
	- Addition/subtraction
		- Combine directed line segments using head-to-tail rule

```c++
vec3 A = vec3(1.0f, 2.0f, 3.0f);
vec3 B = -A
vec3 C = A + B
vec4 E = vec4(A, 1.0f)
vec4 G = E.zxxw // swizzling, spawn order
```

- Vector operations
	- Magnitude of a vector
		- length(vectorA);
	- Normalization
		- Obtain a vector in the same direction, but of unit vector
			- normalize(vectorA);
	- Dot product
		- dot(vectorA, vectorB);
		- ![[Pasted image 20250818090450.png]]
- Cross operations
	- Cross product
		- cross product results in a vector perpendicular to the plane containing the input vector
			- cross(VectorA, VectorB);

# Matrices
---
- rectangular grid of numbers arranged in rows and columns
	- Dimensions = rows x columns
$\begin{bmatrix}m_{11} & m_{12}&m_{13} \\m_{21}&m_{22}&m_{23} \\m_{31}&m_{32}&m_{33}\end{bmatrix}$
- Square matrices
	- same number of rows and columns
	- diagonal elements
	- Identity matrix
		- ![[Pasted image 20250818091503.png]]


- Matrix addition
	- Component wise addition
	- ![[Pasted image 20250818091623.png]]
- Matrix multiplication
	- Can only multiply matrix A with matrix B if 
		- The number of columns in A is equal to the number of rows in B
		- The result is a matrix with the number of rows in A x the number of columns in B
		- ![[Pasted image 20250818092005.png]]
	- For example
```c++
mat3 identityMatrix = mat(1.0f);
mat3 theMatrix = mat3(0.0f, 1.0f, ...)

theMatrix[1] = vec3();
theMatix[2][0] = 13.0f;
```
![[Pasted image 20250818092201.png]]

# Homogenous Coordinates
---
- Key to all computer graphics system
	- Potential confusion between representation of a vector and a point
	- Homogenous coordinates avoids this difficulty by using another dimension to represent points and vectors
- Points and vector
	- Both represented by (x, y ,z)
	- Add a 4th coordinate (x, y, z, w)
		- w = 1(non-zero)


- Points
	- to recover original position
	- ![[Pasted image 20250818092908.png]]

- Matrices
	- All standard transformations can be implemented with matrix multiplication using 3 x 3 or 4 x 4 matrices


# 2D Transformation
---
- Translation
	- Move a point to a new location
		- Move original point along a straight line to its new location
	- An object is defined by multiple coordinate position
		- Relocate all coordinate position by same displacement along parallel paths
	- Translate original coordinates by translational distances $t_{x} \ and \ t_{y}$ to obtain new coordinate position
		- $x'=x+t_{x} \ y'=y+t_{y}$
		- ![[Pasted image 20250818094912.png]]

- Scaling
	- Alter the size of an object
	- Simple scaling operation
		- Multiply original object position(x, y) by scaling factor $s_{x}$ and $s_{y}$ to produce scaled coordinates
		- $x'=x\times s_{x} \ y'=y\times s_{y}$
	- Scaling factors
		- s=1, no change
		- 0<s<1, reduce size
		- s>1, increase size
		- s<0, negative values not only resize the object but reflect it about the respective coords
	- Can control the location of scaled object
		- By choosing a position, called the fixed point that is to remain
		- ![[Pasted image 20250818100007.png]]

- 2D rotation
	- In 2D, roation about an axis perpendicular to xy plane
		- rotation about a pivot point 
		- positive angle $\theta$ defines counter clockwise
	- For objects
		- every point rotated through same angle
		- rigid-body, every point moved without deformation
		- ![[Pasted image 20250818100335.png]]
	- Rotation about origin
		- equation in matrix form
		- ![[Pasted image 20250818100459.png]]
	- Rotation about an arbitrary pivot point
		- ![[Pasted image 20250818100536.png]]


- Reflection![[Pasted image 20250825092506.png]]

