# Compound types: References
- A compound type is a one that is defined in terms of another type. Two important compound type in C++ are references and pointers
```c++
int ival = 1024;
int& refVal = ival;
```


- A reference may be bound to an object, not a literal or result of a general expression
- #

# Functions: Default Arguments
---
```c++
void DrawString(char Text[], int style=0, int size=0);

DrawString("Enter Your Amount"); // 2 default value
```


# Compound Types: Pointers
----
- Pointer is a compound type that points to another type. Pointer can be used for indirect access to other objects. We define a pointer by writing declarator of the form *d
```c++
int* ip1, *ip2;
``` 

- Dereference operator
```c++
int iVal = 78;  
int *intPtr = &iVal; // pointer to iVal

std::cout << *intPtr // print 78
```