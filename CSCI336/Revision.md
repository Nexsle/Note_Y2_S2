## Display devices
- Pixel grid is divided into single color regions that contribute to the displayed or sensed color 

## Vsync
- Synchronizes graphic frame rate and display device's refresh rate
- A way to deal with screen tearing


## Pipeline
- Modelling Transformation
- Viewing Transformation
- Lighting
- Projection
- Clipping
- Rasterization
- Fragment Processing

Coordinates system
- Vertex data : Model coords
- Modelling Transformation : World coords
- Viewing Transformation : View coords
- Lighting
- Projection : clip coords
- Clipping
- Rasterization : Screen coords
- Fragment Processing

## Shader
- code intended for execution on one of the programmable processors
- Compiled and linked to form executable code called a program

## Buffers
- VBO
	- Buffer used as the source for vertex data
- VAO 
	- Store all of the state needed to supply vertex data
	- Stores format of the vertex data and buffer objects


## Vector
Quantity with magnitude and direction
No fixed position in space

## Matrices
Rectangular grid of numbers arranged in rows and columns


## 2D Transformation
Translation: translate original coords(x, y) by translational distances
Scaling: Objects transformed using simple scaling both scaled and repositioned
Rotation

## Viewing Transformation

## Light and Shading
- Emitted from sun or other sources
- Interacts the object in the scene

Point source
- Ideal point source emits light equally in all direction

Directional light
- Also known as distant light sources
- Can be approximated as  a point source


## Polygonal Shading
Flat shading
- Unattractive, can see individual polygons
- Mach bands

Gouraud shading
- Known as smooth shading
- Interpolative vertex intensity values across polygon faces

Phong shading
- Instead of interpolating vertex intensities, interpolate vertex normal


## Mapping Technique
![[Pasted image 20251027093355.png]]

Filtering
- Nearest, default filtering method
- Linear, interpolate value from neighboring texels

Mipmaps
- For minification problems
- Create multiple resolution

## Create a window
Color Buffer
- Two separate color buffer
- Front and back buffers
- One for displaying, others for rendering

## Stencil Buffer
- General purpose buffer for doing things not possible with color and depth buffer alone
- Tag pixels in one rendering pass to control their update in subsequent rendering passes


## Visibility Determination
Depth buffer method
- Common approach
- Compares surface depth values for each pixel position on the projection plane
- Also referred to as the z buffer method


## Clipping
