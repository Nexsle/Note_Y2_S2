- Lighting
	- Calculate intensity to shade 3D models![[Pasted image 20250908084353.png]]


## Real world
---
- Light 
	- Emitted from sun or other source
	- Interacts with object in the scene
		- Part is absorbed 
		- Part is scattered
	- Finally light enter eye
- Color seen by the viewer
	- Determined by multiple interactions among light sources and reflective surfaces

- Local vs global illumination
![[Pasted image 20250908085830.png]]


- Light material interaction
	- Scattering
		- Away from the surface
		- Into the surface
	- Surface reflection
		- The smoother the surface, the more reflected light is concentrated in the direction a perfect mirror would reflect the light
	- Specular surfaces
		- Shiny as most light reflected in a narrow range![[Pasted image 20250908090406.png]]
	- Diffuse surfaces
		- Reflected light scatter in all directions![[Pasted image 20250908090437.png]]
	- Translucent surface
		- Some light enter the surface and emerges from another location

- Attenuation of light![[Pasted image 20250908090831.png]]

## Light source
---
- Light can leave a surface 
- Point source
	- Ideal point source emits light equally
	- Ease of use, less resemblance to reality
	- Affected by attenuation

- Directional light source
	- Also known as distant light source
	- Can be approximate as a point source
	- Ignore attenuation

- Ambient light
	- Provides uniform illumination throughout the environment
	- Models contribution of many sources and reflecting surfaces

- Spotlights
	- Can construct simple spotlight from point source by restricting angle light
	- Characterized by distribution of light![[Pasted image 20250908092235.png]]


## Phong Reflection Model
---
- To calculate color for an arbitrary point
	- Choose 4 unit vectors
		- To light source, l
		- to viewer, v
		- Normal, n
		- Perfect reflector, r
![[Pasted image 20250908092704.png]]

![[Pasted image 20250908092714.png]]


- Lighting model vectors
	- Normal vector is determined by local surface orientation
![[Pasted image 20250908094041.png]]

- Intensity of reflection
$$I=I_{a'} + \sum_{i \ \in \ lights}(I_{d}+I_{s}+I_{a})$$
$I_{a}$ intensity of ambient reflection
$I_{d}$ intensity of diffuse reflection
$I_{s}$ intensity of specular reflection

- Ambient reflection
	- Result of multiple interactions between light sources and object in environment
	- $I_{a} = k_{a}L_{a}$
	- $I_{a}$ intensity of ambient reflection
	- $k_{a}$ ambient reflection coefficient
	- $L_{a}$ intensity of ambient light
- Intensity of ambient light
	- The same at every point o surface
- Some light absorbed, some is reflected

- Diffuse reflection
	- for perfectly diffuse reflector
![[Pasted image 20250908095034.png]]
$$I_{d}=k_{d}L_{d}\cos\theta=k_{d}L_{d}(l \times n)$$
n unit surface normal
l unit direction to light source
$l\times n$ clamped to zero


## Specular reflection
---
- Most surfaces neither perfectly diffuse nor perfectly specular
![[Pasted image 20250908095607.png]]
![[Pasted image 20250908095718.png]]



## Point light
---
```c++
layout(location = 0) in vec3 aPosition;
layout(location = 1) in vec3 aNormal;

uniform mat4 uModelViewProjectionMatrix;
uniform mat44 uModelMatrix;
uniform mat3 uNormalMatrix;

out vec3 vPosition;
out vec3 vNormal;

void main()
{
	gl_Position = uModelViewProjectionMatrix * vec4(aPosition, 1.0f);
		
	vPosition = (uModelMatrix * vec4(aPosition, 1.0f)).xyz;
	vNormal = uNormalMatrix * aNormal;
}
```
