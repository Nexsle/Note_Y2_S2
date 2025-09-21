- Used to provide replacements throughout text
```c++
#define MACRO replacement-text
#define PI 3.14
#define MAX(a,b) (((a) > (b)) ? (a) : b)
```
- We would often replace macros associated with function like operations by inline functions


# Assertion
---
- use to check for condition that cannot happen
```c++
#include <iostream>
#include <cassert>
using namespace std;
int main()
{
#ifndef NDEBUG
cout << "We are in debug mode" << endl;
#endif
assert( 5 > 3);
// assert( 3 > 5);
cout << "All is well" << endl;
return 0;
}
```

- If the expr given to assert is false and we are in debug mode, assert writes a message then terminates the program