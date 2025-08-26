---

---
# Modelling Transformation
----
- Model space to world space
	- Models typically defined in their own coordinate system
![[Pasted image 20250804085703.png]]

# Viewing Transformation
---
- World space to view space
	- Viewing position transformed to origin and direction orientated along the z-axis
	- View seen from camera's viewpoint based on camera's orientation

# Lighting orientation
----
- Local lighting model
	- Calculate intensity to shade 3D
- Shading model
![[Pasted image 20250804090034.png]]

# Projection
----
- 3D scene projected to 2D surface
	- Defines a view volume 
	- Transformed into normalized device coordinates
![[Pasted image 20250804090225.png]]

# Clipping
---
- Clip scene against view volume 
	- Removes part of scene not within view
- Clip space
	- Coordinate system where clipping is performed


# Rasterization
----
- Scan converts vertices into screen space
- After rasterization, everything in fragments

# Coordinate Systems
---
- Graphic pipeline
	- Transforms vertices through several coordinate systems
	- Done using several transformation matrices

![[Pasted image 20250804091802.png]]

![[Pasted image 20250804092628.png]]
# Shader
---
- A shader is code intended for execution on one of the programmable processors
- Compiled and linked to form executable code called a program

- Programmable processors
	- Started off with 
		- Vertex processor
		- Fragment processor
	- Two more were introduced later
		- Geometry and tessellation shaders
- Shading language
	- GLSL(OpenGL Shading Language)


- Vertex shader
	- Used to process vertices
	- Per-vertex operations
- Fragment shader
	- To manipulate fragments
	- Per-fragment operations
	- Produces final RGBA color for each pixel location in the frame buffer


```c++
#version 330 core
// input
layout(location = 0) in vec3 aPosition;
void main()
{
	// set vertex position
	gl_Position = vec4(aPosition, 1.0f);
}
```


```c++
// output data
out vec3 fColor;
void main()
{
	// set output color
	fColor = vec3(1.0f, 0.0f, 0.0f);
}
```

# Primitives
---
- Vertices must be collected into geometric objects before clipping and rasterization can take place
![[Pasted image 20250804094837.png]]


- Attributes
	- Vertex attributes
		- Position
		- Color
	- Point size
		- gl_PointSize in vertex shader with GL_PROGRAM_POINT_SIZE enabled
	- Wireframe/polygon fill
		- glPolygonMode()
	- Textured

# Coordinate Systems
---
- Position
	- 2D coordinates: (x, y)
	- 3D coordinates: (x, y, z)
![[Pasted image 20250804095704.png]]

- Position 
```c++
std::vector<GLfloat> vertices = 
{
	0.0f, 0.5f, 0.0f,
	0.5f, -0.5f, 0.0f,
	-0.5f, -0.5f, 0.0f
};
```
![[Pasted image 20250804100449.png]]

# Graphic Programming
---
- Vertex data
	- Submitting vertex data for rendering requires creating a stream of vertices
		- Vertex buffer object (VBO)
	- Tell OpenGL how to interpret data in the stream
		- Format of the data
		- Vertex array object(VAO)
		- Primitive assembly

- Vertex Buffer object(VBO)
	- A buffer used as the source for vertex data
- Vertex array object(VAO)
	- Stores all of the stat needed to supply vertex data
	- Stores format of the vertex data and buffer objects
- OpenGL is known as "state machine"

- Passing vertex data
	- Define vertices
- Use VBO to store and send to graphics device
- Create VBO
```c++
GLuint gVBO = 0;
glGenBuffers(1, &gVBO);
```

- Bind buffer object to make it active
	- ```glBindBuffer(GL_ARRAY_BUFFER, gVBO);```
- Buffer the data in graphic device memory
```c++
glBufferData(GL_ARRAY_BUFFER, sizeof(float) * verices.size(), &vertices[0], GL_STATIC_DRAW);
```


- VAO
	- Store states, one or more VBOs and format of vertex data
	- Create VAO
```c++
GLuint gVAO = 0;
glGenVertexArrays(1, &gVAO);
```

- Bind array object to make it active
```c++
glBindVertexArray(VAO);
```

- Associate it with one or more buffer objects
```c++
glBindBuffer(GL_ARRAY_BUFFER, gVBO);
```
![[Pasted image 20250804102146.png]]

![[Pasted image 20250804102213.png]]


