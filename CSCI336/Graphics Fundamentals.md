# What is Computer Graphics
---
- Deals with all aspects of creating images with a computer
- ![[Pasted image 20250728090229.png]]


# Display Devices
----
- Cathode-Ray Tubes (CRT)
![[Pasted image 20250728090722.png]]

- Three electron guns
	- Aligned with the triangular color dot patterns on the screen, are directed to each dot triangle by a shadow mask
![[Pasted image 20250728090748.png]]

- Sub-pixels
	- Pixel grid is divided into single-color regions that contribute to the displayed or sensed color when viewed at a distance


# Raster-Scan Displays
----
- A raster-scan system displays an object as a set of discrete points
	- Each row is referred to as a scan-line
	- Pixel info stored in buffer locations, collectively referred to as the frame buffer
- Refresh rate
	- Frequency at which a picture is redisplayed
	- Vertical synchronization

- Architecture of a raster-graphics system with a display processor
![[Pasted image 20250728092810.png]]

# Real-time Rendering
----
- The process of converting data into visually perceivable form
- In general
	- Rendering at interactive rates
	- Done with the help of GPUs
- 

# Graphics Hardware
---
- Graphics processing unit
	- Dedicated to providing high-performance, visually rich, interactive 3D graphics
	- All of today's commodity GPUs structure their graphics computations in a similar org called the computer graphics pipeline

# Graphic pipeline
---
- task is to synthesize an image from a description of a ascene
- Scene contains geometric primitives, descriptions of lights, the way each object reflects light, viewer's position and orientation
- Overview of stages in the graphics pipeline
![[Pasted image 20250728094839.png]]

# Programmer's Interface
---
- Library of graphics functions that can be used i a a programming language
![[Pasted image 20250728095317.png]]

# Create a window
---
- Create a window and context 
	- OpenGL context represents many things
		- Stores all OpenGL states, represents buffers
		- Think of a context as an object that holds all of OpenGL
	- GLFW
- Load OpenGL extensions
	- Otherwise some platforms default to OpenGL 1.2
		- This subject is about modern OpenGL
	- GLEW

- Frame buffer
	- Collection of buffers used for rendering
		- Color buffer, depth buffer, stencil buffer
	- The term frame refers to the total display area
	- Often when people refer the the frame buffer, they are talking about the color buffer

- Color buffer
	- Where RGBA color values are stored
	- Settiing the clear color
		- ```glClearColor(0.2f, 0.2f, 0.2f, 1.0f);```
		- if not set, OpenGL will use the default clear color
	- Clearing the color buffer
		- ```glClear(GL_COLOR_BUFFER_BIT);```
	- Double buffering
		- Two separate color buffers
			- One for displaying, the other for rendering
			- Referred to as front and back buffers

- Rendering loop
	- Loops until the window is closed
	- Each loop pass renders a single frame
	- Swap buffers once complete
		- ```glfwSwapBuffers();```
	- Swap buffers with display device's vsync
		- ```glfwSwapInterval(1);```
		- Some gpu do not honor this request
	- Check and process events

# Vertical Synchronization
---
- Vsync
	- Synchronize graphic frame rate and display device's refresh rate 
	- A way of dealing with screen tearing


# Callback Function
---
```c++
static void error_call(int error, const char* description)
{
	blah
}

glfwSetErrorCallback(error_call);
```


# Key Callback
----
```c++
static void key_call(GLFWwindow* window, int key, int scancode, int action, int mods)
{
	blah
}

glfwSetKeyCallback(window, key_call);
```

# Rendering loop
---
```c++
	// the rendering loop
	while (!glfwWindowShouldClose(window))
	{
		render_scene();		// render the scene

		glfwSwapBuffers(window);	// swap buffers
		glfwPollEvents();			// poll for events
	}
```