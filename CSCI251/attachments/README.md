# CSCI251 Assignment 1
### Source Files

#### `driver.cpp`
- **Role**: Main entry point of the program
- **Content**: 
  - Handles command line arguments (Tasks.txt, Workers.txt, Output.txt)
  - Manages file operations and error handling
  - Coordinates the overall program flow
  - Calls LoadFile() and CalculatePerformance() functions

#### `header.h`
- **Role**: Header file containing all function prototypes and struct definitions
- **Content**:
  - Task struct definition with private members (taskId, description, uncertainty, difficulty, priorityLabel, workerList, workerCount) and public getter methods
  - Worker struct definition with private members (workerId, name, variability, ability, experienceLabel) and public getter methods
  - Function prototypes for all program operations

#### `header.cpp`
- **Role**: Implementation file containing all function definitions
- **Content**:
  - Task and Worker struct constructors and getter methods
  - LoadFile() - Parses Tasks.txt and Workers.txt files using delimiters
  - CalculatePerformance() - Main simulation logic that processes each task
  - AveragePerformance() - simulate set amount of draws and taking the average normal distribution
  - TaskDisplayBoard() - Formats and displays task information
  - File output management functions

## How to Compile and Run

### Compilation
```bash
g++ -o prog driver.cpp header.cpp
```

### Execution
```bash
./prog Tasks.txt Workers.txt Output.txt
```

### Command Line Arguments
1. **Tasks.txt** - Input file containing task information
2. **Workers.txt** - Input file containing worker information  
3. **Output.txt** - Output file where results will be written

