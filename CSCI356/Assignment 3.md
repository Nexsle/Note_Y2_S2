# Implementation 

  1. SLIDING DOOR MECHANICS
     - Smooth sliding doors using sine wave interpolation for natural easing
     - Doors slide between two defined points (pointA and pointB)

  2. KEY-BASED DOOR SYSTEM
     - Color-coded key system (keys must match door lock color)
     - Key pickup and removal system ("Q" to drop key)
     - Keys are consumed when used to unlock doors
     - Visual key attachment to player

  3. PROXIMITY-BASED INTERACTION
     - Doors only unlock when player is near
     - UI prompt ("C" key) appears only for locked doors
     - Automatic door opening/closing for unlocked doors

  4. DOOR COUNTER UI
     - Counter tracking number of doors unlocked
     - TextMeshPro  for UI display

  5. SMART DOOR BEHAVIOR
     - Unlocked doors open automatically when approaching
     - Delayed closing system prevents doors closing too quickly

# CONTROLS

  - Left Click: to move
  - Hold Right Click + Mouse: rotate camera
  - C: Unlock door (when near locked door with correct key)

# TECHNICAL IMPLEMENTATION

  Key Classes:
  - SlidingDoor.cs: Handles smooth door animation using sine interpolation
  - OpenDoor.cs: Manages door locking, key validation, and UI interaction
  - KeyHolder.cs: Player inventory system for keys
  - Key.cs: Key objects with color-coded types
  - UIEvent.cs: control all the ui elements

  Door Animation:
  - Uses sin(x - π/2) * 0.5 + 0.5 for smooth 0→1 easing curve
  - sinTime clamped to π for complete half-sine cycle
  - Automatic position swapping between pointA and pointB

# ISSUES ENCOUNTERED & SOLUTIONS

  1. FLOATING POINT PRECISION
     Issue: Door position comparison using == caused doors to never finish moving
     Solution: Implemented distance-based comparison and position snapping

  2. DOUBLE KEY PRESS REQUIREMENT
     Issue: Door required two key presses due to immediate position swapping
     Solution: Added proper current/target position logic based on door location

  3. PREMATURE DOOR CLOSING
     Issue: Fast player movement caused doors to close before fully opening
     Solution: Implemented coroutine-based delay system for proper door sequencing

  4. UI INTERACTION CONFLICTS
     Issue: Multiple doors updating UI simultaneously caused flickering prompts
     Solution: Moved UI updates to OnTriggerEnter/Exit instead of Update loop
