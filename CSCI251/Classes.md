# Object
---
- To create a class with methods
	- Inside class
	- Outside class
### Inside
```c++
#include <iostream>
using namespace std;
class Hacker { // The class Hacker
public: // Access specifier
	void scan(){ // Create function/
		method inside class
		cout << "I am scanning the target";
	}
};
int main(){
	Hacker hacker_1; // Create an Object of Hacker
	hacker_1.scan(); // Call the method by "." operator
	return 0;
}
```

### Outside
```c++
#include <iostream>
using namespace std;
class Hacker { // The class Hacker
public: // Access specifier
	void scan(); // Declare the function/method
};
// Create function/method outside class
void Hacker::scan(){
	cout << "I am scanning the target";
}
int main(){
	Hacker hacker_1; // Create an Object of Hacker
	hacker_1.scan(); // Call the method by "." operator
	return 0;
}
```

# Constructor / Destructor
---
- To create a constructor, use the same name as the class 
```c++
class Hacker
{
	Hacker(); // constructor
	~Hacker(); // destructor
}
```

- We can have multiple constructor


# 'this' pointer
---
- Represent the address of the current object instance on which the member function is being called
```c++
class Test
{
	int x;
	
public:
	void setX(int x)
	{
		this->x = x;
	}	
}
```


# Copy constructor
---
```c++
X(const X &cp);
```
- the copy constructor creates an object by initing it with an object of the same class, which has been created previously

- how to call
```c++
X first;
X second(first);
X second = first;
```


# Copy assignment
---
```c++
X& operator = (const x &cp);

class Test
{
	Cat& operator = (const Cat &cp) 
	{ 
		return *this;
	}
}
Cat cat2;
cat2=cat1;
```


# Polymorphisms
----
- Compile time polymorphism
	- Function overloading
	- Operator overloading

- Run time polymorphism
	- Function overriding
	- Virtual function

## Overloading
- Multiple functions with the same name but different parameter


# Friend
---
- A friend function is defined outside that class scope but it has the right to access all private and protected members
```c++
friend return_type function_name (Class & objClass);
```

