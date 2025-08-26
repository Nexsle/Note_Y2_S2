# Dynamics of Particles
----
- Physic is based on measurement
- Some SI(International System of Units) base quantity and unit![[Pasted image 20250820085331.png]]


- Linear motion
	- Described in terms of 
		- Displacement, time, velocity, and acceleration
	- Displacement
		- Change from one position to another
	- Average velocity(m/s)
		- Change in position over the time period taken for that change![[Pasted image 20250820085730.png]]
	- Velocity (instantaneous velocity)
		- Shrink the time interval closer and closer to 0
		- The limit as $\Delta t$ approaches 0![[Pasted image 20250820085900.png]]
	- Acceleration
		- rate at which velocity is changing
		- positive represents speeding up
		- zero means no change
		- a negative value represent slowing down![[Pasted image 20250820090014.png]]

- Linear motion
	- In mathematics, integration is the opposite of differentiation
	- Integration is used to update position and velocity
	- Equation for linear motion
		- ![[Pasted image 20250820090903.png]]
	- Kinematics can be implemented manually using a GameObject's Transform class![[Pasted image 20250820091058.png]]
	- Accuracy versus computational complexity
		- if acceleration is not too high, ignoring acceleration results in a reasonably accurate approximation


- Newton's first law(Law of inertia)
	- On object will remain at rest, or continue to move at a constant velocity, unless acted upon by a net force

- Newton's second law (Law of acceleration)
	- Any change in motion involves an acceleration
	- A net force acting on an object produces acceleration that is proportional to the object's mass
		- $\vec{F}=m\vec{a}$

# Rigidbody
---
- Used to control an object's movement and position
- In a script, the FixedUpdate() method is recommended as the place to apply forces and change rigidbody settings
- 