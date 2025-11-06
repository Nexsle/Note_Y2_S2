## Implemented Features

### 1. Textured Objects (Floor and Cube)

**Implementation:**
- Added texture coordinates to vertex data structures (`VertexNormTex`)
- Modified `lighting.vert` shader to pass texture coordinates to fragment shader
- Updated `reflection.frag` shader to sample textures using `texture()` function
- Loaded textures using `Texture::generate()` for checkered floor and smile face

**Key Code:**
```cpp
// Load textures
gTextures["Check"].generate("./images/check.bmp");
gTextures["Smile"].generate("./images/smile.bmp");

// In shader: reflection.frag
vec3 textureColor = lighting * texture(uTextureSampler, vTexCoord).rgb;
```
![[Pasted image 20251031042939.png]]
---

### 2. Reflective Torus with Environment Mapping

**Implementation:**
- Loaded torus model and created separate shader program (`gCubeMapShader`)
- Generated cube map texture from 6 images (front, back, left, right, top, bottom)
- Used `lighting_cubemap.frag` shader to calculate reflection vectors
- Added `uReflectiveness` uniform to control metallic appearance (0.0 = matte, 1.0 = mirror)

**Key Code:**
```cpp
// Cube map generation
gTextures["Cube Map"].generate("./images/cm_front.bmp", "./images/cm_back.bmp",
    "./images/cm_left.bmp", "./images/cm_right.bmp",
    "./images/cm_top.bmp", "./images/cm_bottom.bmp");

// In shader: lighting_cubemap.frag
vec3 reflectEnvMap = reflect(-v, n);
vec3 envColor = texture(uEnvironmentMap, reflectEnvMap).rgb;
fColor = mix(fColor, fColor * envColor, uReflectiveness);
```

![[Pasted image 20251031042950.png]]

---
### 3. Four Textured Walls with Normal Mapping

**Implementation:**
- Created wall geometry with position, normal, tangent, and texture coordinate data
- Used separate VBO and VAO for walls (`gVBOs["Walls"]`, `gVAOs["Walls"]`)
- Created 4 model matrices with different translations and rotations:
  - Front wall: translate (0, 0, -4.5), no rotation
  - Back wall: translate (0, 0, 4.5), rotate 180° around Y
  - Left wall: translate (-4.5, 0, 0), rotate 90° around Y
  - Right wall: translate (4.5, 0, 0), rotate -90° around Y
- Loaded stone texture and normal map texture
- Tangent vectors set to (1, 0, 0) for flat vertical walls

**Key Code:**
```cpp
// Model matrix for front wall
gModelMatrix["FrontWall"] = glm::translate(glm::vec3(0.0f, 0.0f, -4.5f))
                          * glm::scale(glm::vec3(4.5f, 3.5f, 1.0f));

// In shader: normalMap.frag
vec3 tangent = normalize(vTangent);
vec3 biTangent = normalize(cross(tangent, n));
vec3 normalMap = 2.0f * texture(uNormalSampler, vTexCoord).xyz - 1.0f;
n = normalize(mat3(tangent, biTangent, n) * normalMap);
```
![[Pasted image 20251031043003.png]]
---

### 4. Multiple Viewport Views

**Implementation:**
- Added `gMultipleViews` boolean toggle controlled by TweakBar UI
- Created helper functions for fixed camera views:
  - `getTopDownView()`: Camera at (0, 10, 0) looking down
  - `getFrontView()`: Camera at (0, 2, 10) looking at origin
- Implemented temporary matrix system using global flags:
  - `gUseTemporaryMatrices`: Toggle between camera and temporary matrices
  - `gTempViewMatrix`, `gTempProjMatrix`, `gTempCameraPos`: Override matrices
- Modified all draw functions to check flag and use appropriate matrices
- Used `glViewport()` to divide window into quadrants:
  - Top-right: Top-down view
  - Bottom-left: Front view
  - Bottom-right: Moving camera view (user-controlled)
  - Top-left: Empty (for TweakBar)
- Single `glClear()` at start to prevent viewports from erasing each other

**Key Code:**
```cpp
if (gMultipleViews) {
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT | GL_STENCIL_BUFFER_BIT);

    // Top-right: Top-down view
    glViewport(halfWidth, halfHeight, halfWidth, halfHeight);
    render_scene_with_view(getTopDownView(), projMatrix, glm::vec3(0.0f, 10.0f, 0.0f));

    // Bottom-left: Front view
    glViewport(0, 0, halfWidth, halfHeight);
    render_scene_with_view(getFrontView(), projMatrix, glm::vec3(0.0f, 2.0f, 10.0f));

    // Bottom-right: Moving camera
    glViewport(halfWidth, 0, halfWidth, halfHeight);
    render_scene_with_view(gCamera.getViewMatrix(), projMatrix, gCamera.getPosition());
}
```
![[Pasted image 20251031043027.png]]

---
### 5. Floor Reflection(Stencil Buffer Technique)

**Implementation:**
- Used stencil buffer to mask reflection rendering to floor area only
- Three-pass rendering technique:
  1. **Stencil setup**: Draw floor shape into stencil buffer (set to 1)
  2. **Reflected geometry**: Draw objects with `scale(1, -1, 1)` transform, only where stencil = 1
  3. **Blended floor**: Draw semi-transparent floor with alpha blending over reflections
- Reflection matrix flips Y-axis to position objects below floor plane
- Alpha blending controlled by `gAlpha` parameter (0.2 to 1.0)
- All objects (cube, torus, walls) rendered twice: normal and reflected

**Key Code:**
```cpp
// Pass 1: Draw floor into stencil buffer
glStencilFunc(GL_ALWAYS, 1, 1);
glStencilOp(GL_REPLACE, GL_REPLACE, GL_REPLACE);
draw_floor(1.0f);

// Pass 2: Draw reflected objects where stencil = 1
glStencilFunc(GL_EQUAL, 1, 1);
reflectMatrix = glm::scale(glm::vec3(1.0f, -1.0f, 1.0f));
draw_objects(true);  // Applies reflection matrix

// Pass 3: Blend floor with reflections
glEnable(GL_BLEND);
glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);
draw_floor(gAlpha);  // Semi-transparent
```
![[Pasted image 20251031043057.png]]

---

## Technical Architecture

### Shader Programs
1. **gShader** (lighting.vert + reflection.frag): Floor and cube with textures
2. **gCubeMapShader** (lighting.vert + lighting_cubemap.frag): Torus with environment mapping
3. **gNormalMapShader** (normalMap.vert + normalMap.frag): Walls with normal mapping

### Data Structures
- Multiple VBOs/VAOs: Separate geometry for floor, walls
- Vertex formats:
  - `VertexNormTex`: Position, Normal, TexCoord (floor, cube)
  - `VertexNormTanTex`: Position, Normal, Tangent, TexCoord (walls)
- Model matrices stored in `std::map<std::string, glm::mat4>`
- Material properties stored in `std::map<std::string, Material>`

---
