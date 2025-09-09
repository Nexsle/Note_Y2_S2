![[Pasted image 20250904121850.png]]

![[Pasted image 20250904121900.png]]

![[Pasted image 20250904121921.png]]
## Implementation
---
```c++
	std::vector<VertexColor> allVertices;
	std::map<std::string, int> vertexCounts;
	std::map<std::string, int> startIndices;
```
- Use a single buffer where all vertex data is stored with indexed access.


```c++
std::map<std::string, glm::mat4> gModelMatrix;
```
- Each component has an associated transformation

```c++
glm::mat4 movement = glm::translate(glm::mat4(1.0f), gMoveVec); gModelMatrix["chassis"] = movement * gModelMatrix["chassis"]; gModelMatrix["driver"] = movement * gModelMatrix["driver"]; gModelMatrix["dump"] = movement * gModelMatrix["dump"]; gModelMatrix["leftWheel"] = movement * gModelMatrix["leftWheel"]; gModelMatrix["rightWheel"] = movement * gModelMatrix["rightWheel"];
```
- Move the whole truck as a unified object

```c++
float tireRotation = 0.0f;
if (glfwGetKey(window, GLFW_KEY_LEFT) == GLFW_PRESS) {
    tireRotation += rotateSpeed * deltaTime;
}
gModelMatrix["leftWheel"] *= glm::rotate(glm::radians(tireRotation), glm::vec3(0.0f, 0.0f, 1.0f));
```
- Wheels rotate proportionally to movement speed 

```c++
float gDumpClamp = 0.0f;
if (glfwGetKey(window, GLFW_KEY_UP) == GLFW_PRESS && gDumpClamp > -45.0f) {
    dumpAngle -= gRotateSensitivity * deltaTime; 
    gDumpClamp -= gRotateSensitivity * deltaTime;
}
```
- Clamp the dump rotation to between 0 and 45 degrees

## Keyboard Controls
---
- **Arrow Keys**: Primary interaction method
    - Left/Right: Horizontal movement with wheel animation
    - Up/Down: Dump bed articulation
- **B Key**: Cycles through 6 background colors
- **Escape**: Program termination
- **Right Click**: Alternative exit method