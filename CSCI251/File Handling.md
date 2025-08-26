# Text File Streams
---
```c++
#include <fstream>

using namespace std;
#include <iostream>
#include <sstream>

ifstream inData; // input file
ofstream outData; //output file

inData.open("names.txt");
outData.open("marks.txt");

inData >> firstName >> lastName;
outData << 85.6;

inData.close();
outData.close();

```

- Different modes
- ![[Pasted image 20250821115835.png]]


# Error in reading files
----
```c++
if(inData.eof()) // flag indicates that the end of file is reached

if(inData.fail()) // indicates a failure due to invalid data

if(inData.bad()) // indicates hardware problems
```