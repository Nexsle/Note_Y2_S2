A library is a precompiled binary that contains the implementation of that functionality pre-compiled into machine language

# Why pre-compiled
Save resources: library rarely change, they do not need to be recompiled often
Improve security: precompiled object are in machine language, prevents people from changing the machine code

# Lib types
Static:
- A collection of .o files concatenated together
- Compiled and linked directly into your program

Dynamic:
- Loaded into your app at run time
- Remains a separate unit


# Build a static Lib
---
```c++
g++ -c code.cpp
ar -crv libcode.a code.o
```
The result is a library: libcode.a

Check whats inside 
```c++
ar -t libcode.a
code.o
```



# Build a shared lib
---
To build the shared library with the GNU compiler you must use the use ```-fpic``` directive which produces position independent output
```g++
g++ -fpic -shared -o libcode.so code.cpp
```

# Using a lib
---
We need to set up the lib path to the current directory
```c++
LD_LIBRARY_PATH=.
export LD_LIBRARY_PATH


g++ -I. -L. main.cpp -lcode
```