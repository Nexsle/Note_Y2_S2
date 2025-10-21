# Reflection Stencil 
Basic algo
- Clear buffers
- Disable depth buffer and draw mirror surface to stencil buffer
- Enable depth buffer, draw reflected geometry where stencil buffer passes
- Disable stencil buffer, draw normal scene

Another way
- Clear buffers
- Draw all non mirror geometry to frame & depth buffers
- Draw mirror to stencil buffer, where depth buffer passes
- Set depth to infinity, where stencil buffer passes
- Draw reflected geometry to frame & depth buffer where stencil buffer passes

# Shadows
Shadow volume
- Volume of space in shadow
- Pyramid with point light as the apex
- Polygons inside a shadow volume will not be illuminated by that particular light
- Shadow test similar to clipping

# Compositing and Blending
Alpha blending
- When blending is enabled, value of $\alpha$ determines how the RGB values are written into the color buffer

Blending equation
- Can define source and destination blending factors for each RGBA component
![[Pasted image 20251013091036.png]]


Hidden surface removal
- Opaque polygons block all polygons behind them and affect the depth buffer
- Easiest solution
	- Render all opaque polygons first
	- disable the depth test
	- Render translucent polygons in a back to front order

Fog and depth cueing
- Composite and blending depend on depth
	- Add fog or haze effect to the scene
	- Gives the illusion of objects disappearing in the distance
	- $C_{s}' = fC_{s} +(1-f)C_{f}$
	- f is the fog factor
![[Pasted image 20251013092331.png]]


Billboarding
- 2D texture used as 3D entity in the scene
- Rotated so polygon's normal always faces the viewer
![[Pasted image 20251013092432.png]]


# Mapping Techniques
Normal mapping
- Textures used to perturb the surface normal 
	- Actual geo does not change

Environment mapping
![[Pasted image 20251013094047.png]]
