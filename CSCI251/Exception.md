# Traditional Error Handling
---
```c++
if(a < 1)
	exit(1);
```
- The exit() function forces the program to end 
- is inflexible
- function should be able to determine an error situation


- A better alt
```c++
bool inputStudentRec(Student &sRec)
{
	bool errorCode = true;
	
	if(day<1 || day > 31)
		errorCode = false;
	return(errorCode);
}
```


# Throw Exception
---
```C++
try {
	//exception may be thrown using throw
	
}
catch () {
	//handle your exception
}
```
- Need multiple catch block for multiple exception

# Unwinding the Stack
---
- Your function A can try a function call B and, if the function B throws and exception, you can catch the exception
- If A doesnt catch, then C that call A can still catch the exception![[Pasted image 20250826110854.png]]

