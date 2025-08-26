# Evolution of video games
---
- Games developed in 70s-80s
	- Relatively cheap
	- Often made from scratch by one programmer
- Modern games
- Enormous implementation complexity and costs if developed from scratch

# What is a game engine
----
- The core software of the game
	- Describes a set of code used to build the game app
	- Software suites that provide the technological underwiring for games
	- A framework comprised of a collection of different tools, utilities, and interfaces 
- The term was introduced in the mid 1990s in reference to FPS games like Doom
- The value of separation became evident
- Ideally, a game engine should be extensible
- Data-driven architecture is what differentiates a game engine from a program that is a game but not an engine

# Evolution of Game Engine
----
- Early game companies used to make their own game engines 
- Later on 
	- id Tech - 1996
	- Unreal Engine
- Key components of a game engine
	- Graphics
	- Input system
	- Physics and collision
	- Artificial intelligence
	- Audio system
	- Networking 
	- Other utilities

- Choosing a game engine
	- Each engine has its advantages and disadvantages
	- Depends on the developer's needs in terms of budget, schedule
	- Cros-platform capabilities
	- Look and feel


# Rendering Loop
----
- For the GUI of normal app
	- Contents on screen are mostly static
	- Only redraw  sections of screen that change via rectangle
- In real-time 3D graphic
	- Moving camera in 3D scene
![[Pasted image 20250730094900.png]]
- Interacting subsystems
	- Rendering, input/output systems, animation
- The game loop
	- Master loop that updates everything

# Time
---
- In a simple game loop that doesn't handle time
- The game runs
	- On slower hardware game run slow, fast hardware run fast
- Abstract timeline
	- Continuous, one-dimensional axis whose origin (t = 0) can lie at any arbitrary location
- Real time
	- Can be obtained from CPU's high resolution timer register


- Useful to have different timers
	- To pause the game, stop updating game timeline
	- Various effects of scaling/warping one timeline relative to another
	- Debugging

- Frame rate
	- How rapidly the sequence of still 3D frames is presented to the viewer
- Frame time
	- Also known as time delta
	- The amount of time that elapses between frames
	- Can be measure by simply subtracting time from previous frame with time at current frame
- Running average
	- Allows game to adapt to varying frame rates
- Governing the frame rate
	- Rather than guessing, try to guarantee every frame duration
	- put main thread to sleep until target frame time
	- 