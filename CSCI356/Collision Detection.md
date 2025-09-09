- Simulating collisions consist of 
	- Collision detection
	- Collision response 
- Determining whether objects come into contact
- Responsible for finding
- Needs to take geometry into account

- Collider
	- Base class for all colliders
	- If an object with a collider needs to be moved during gameplay
	- should attach a rigidbody components 

- Collision detection often not carried out directly on meshes
- Primitive colliders
- Can be very time consuming
	- Each object in the game maybe colliding with any other object

# Bounding Volumes
---
- An area of space known to contain the object
- Large enough for the object to be inside
- Simple shape used
 ![[Pasted image 20250827090635.png]]
- Simple collision check
	- Overlap if distance between center less than sum of radius
	- 


# Bounding Volumes Hierarchies
---
- Building the hierarchy
	- Static environment
		- can be constructed offline
	- Dynamic environment
		- must be recalculated 
	- Bottom up
		- Starts with bounding volumes of each object
		- parent added
		- Continue till only one node left![[Pasted image 20250827095347.png]]
	- Top down
		- also starts with bounding volume of individual objects
		- Each iteration, objects in each group separated into two group
		- continue till only one object in each group![[Pasted image 20250827095500.png]]
	- Insertion
		- only approach suitable for use during the game
		- can adjust hierarchy without having to rebuild it completely
		- starts with existing tree
		- object added/ inserted into the tree![[Pasted image 20250827095608.png]]
	- Removing object
		- cant
		- need to replace or recalculate

# Spatial data structure
----
![[Pasted image 20250827101236.png]]
