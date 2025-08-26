# Multi-Platform support
---
- Unity uses the open-source .NET platform
	- Ensures applications made with Unity can run on a wide variety of different hardware config

# Unity Essentials
---
- Scenes
	- Scenes are where you work with content in unity
	- Assets that contain all or part of a game or application
	- Can create any number of scenes in a project

- Global space
	- Coordinate system of the scene itself
	- Origin is the centre of the scene
	- Cannot change the direction of this coordinate system
- Local space
	- Coordinate system relative to rotation of a specific object
	- Origin is at the object's pivot point

- Game Object
	- Represent anything that can exist in a scene
	- Act as a container for Components
	-  Can have parent child relationship
	- Empty GameObject
		- Organize object


# Script
----
- Create your own components using scripts
	- Trigger game events, modify component properties over time
- Initialization is not done using a constructor


- Time class
	- Provides numeric values to measure time elapsing while game is running 
	- Some important properties 
		- Time.time - read only, time elapsed since project started
		- Time.daltaTime - read only, time elapsed since the last frame
		- Time.timeScale - control the rate at which time elapses
		- Time.fixedDeltaTime - control the interval of Unity's fixed timestep loop

- Input
	- Every project has several input axes created by default

- Serialising
	- Public variables are displayed in the inspector
		- Can change their value at run time
	- Instead of using public variable
		- Using \[SerializeField] makes the variable appear in the inspector, but is a private variable

- Component dependencies
	- Can enforce dependency
		- \[RequireComponent(typeof(Rigidbody))]


- Coroutines
```c++
IEnumerator Fade()
{
	yeild return new WaitForSeconds(.1f)
}
```

- Interaction between objects
	- Messaging system
		- Call a method that is implemented in another script attached to the same object, or another and pass a parameter to it