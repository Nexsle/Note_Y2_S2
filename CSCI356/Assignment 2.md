# OpenGL Solar System Simulation Report
![[Pasted image 20250923011603.png]]
![[Pasted image 20250923011614.png]]
![[Pasted image 20250923011622.png]]

## Implemented Features
### 1. Multi-Object Orbit System
**Implementation:**

- **Object 1 (Sphere)**: Central stationary object at the origin

- **Object 2 (Suzanne)**: Orbits around Object 1 at radius 5.0 units

- **Object 3 (Cube)**: Orbits around Object 2 at radius 2.0 units

```cpp
static float angle2 = 0.0f;
angle2 += gOrbitSpeed2;
gModelMatrix2 = glm::rotate(glm::mat4(1.0f), angle2, glm::vec3(0.0f, 1.0f, 0.0f));
gModelMatrix2 = glm::translate(gModelMatrix2, glm::vec3(5.0f, 0.0f, 0.0f));

  

static float angle3 = 0.0f;
angle3 += gOrbitSpeed3;
gModelMatrix3 = glm::rotate(glm::mat4(1.0f), angle3, glm::vec3(0.0f, 1.0f, 0.0f));
gModelMatrix3 = glm::translate(gModelMatrix3, glm::vec3(2.0f, 0.0f, 0.0f));
gModelMatrix3 = glm::scale(gModelMatrix3, glm::vec3(0.5f, 0.5f, 0.5f));

```
### 2. Material System
**Implementation:**
Three distinct materials are available: Brass, Jade, and Pearl, each with unique ambient, diffuse, specular, and shininess properties.
```cpp
gMaterials["Brass"].Ka = glm::vec3(0.33f, 0.22f, 0.03f);
gMaterials["Brass"].Kd = glm::vec3(0.78f, 0.57f, 0.11f);
gMaterials["Brass"].Ks = glm::vec3(0.99f, 0.94f, 0.8f);
gMaterials["Brass"].shininess = 27.9f;

gMaterials["Pearl"].Ka = glm::vec3(0.25f, 0.21f, 0.21f);
// ... similar for Jade and Pearl

```
### 3. Orbit Visualization
**Implementation:**

Two colored orbital rings show the paths of the orbiting objects.
```cpp
std::vector<glm::vec3> CreateCircle(float radius, int segment)
{
    std::vector<glm::vec3> circleVertices;
    for (int i = 0; i < segment; i++)
    {
        float angle = 2.0f * M_PI * i / segment;
        circleVertices.push_back(glm::vec3(radius * cos(angle), 0.0f, radius * sin(angle)));
    }
    return circleVertices;
}

std::vector<glm::vec3> firstCircle = CreateCircle(5.0f, 64);   // Object 2's orbit

std::vector<glm::vec3> secondCircle = CreateCircle(2.0f, 64);  // Object 3's orbit

```
### 4. Interactive Camera System
**Implementation:**
Three predefined camera viewpoints accessible via keyboard controls.
```cpp
if (key == GLFW_KEY_1 && action == GLFW_PRESS)
{
    gViewMatrix = glm::lookAt(glm::vec3(0.0f, 2.0f, 8.0f),
        glm::vec3(0.0f, 0.0f, 0.0f), glm::vec3(0.0f, 1.0f, 0.0f));
}
if (key == GLFW_KEY_2 && action == GLFW_PRESS)
{
    gViewMatrix = glm::lookAt(glm::vec3(0.0f, 0.0f, 10.0f),
        glm::vec3(0.0f, 0.0f, 0.0f), glm::vec3(0.0f, 1.0f, 0.0f));
}
if (key == GLFW_KEY_3 && action == GLFW_PRESS)
{
    gViewMatrix = glm::lookAt(glm::vec3(0.0f, 10.0f, 0.0f),
        glm::vec3(0.0f, 0.0f, 0.0f), glm::vec3(0.0f, 0.0f, -1.0f));
}
```

**Camera Views:**
- **Key 1**: Angled view (0, 2, 8) - Standard perspective view
- **Key 2**: Side view (0, 0, 10) - Horizontal perspective
- **Key 3**: Top-down view (0, 10, 0) - Orbital plane view
### 5. User Interface Integration
**Implementation:**
AntTweakBar-based UI for real-time parameter control, positioned to not overlap with the 3D viewport.

```cpp

TwAddVarRW(twBar, "Model 2", modelOptions, &gModelSelected2, " group='Object 2' ");
TwAddVarRW(twBar, "Material 2", materialOptions, &materialSelected2, " group='Object 2' ");
TwAddVarRW(twBar, "Orbit Speed 2", TW_TYPE_FLOAT, &gOrbitSpeed2, " group='Object 2' min=0 max=1 step=0.01");
```
**UI Controls:**
- Model selection (Sphere, Cube, Suzanne) for Objects 2 and 3
- Material selection (Brass, Jade, Pearl) for Objects 2 and 3
- Orbital speed controls (0.0 to 1.0 range)
- Rotation speed control for Object 2
### 6. Viewport Management
**Implementation:**
The rendering viewport is configured to not overlap with the UI panel.

```cpp
float viewPortWidth = gWindowWidth - 250;
gProjectionMatrix = glm::perspective(glm::radians(90.0f), viewPortWidth / gWindowHeight, 0.1f, 50.0f);

glViewport(uiWidth, 0, gWindowWidth - uiWidth, gWindowHeight);
```
**Features:**
- Window size: 1000x800 pixels
- UI width: 250 pixels (left side)
- 3D viewport: 750x800 pixels (right side)
- Adjusted projection matrix aspect ratio for correct proportions
## Usage Instructions
- **ESC**: Exit application
- **1, 2, 3**: Switch between camera viewpoints
- **UI Panel**: Adjust object models, materials, and animation speeds in real-time