# Procedural programming
---
- Focus on a specific aim or end result
	- The aim is often fairly fixed
	- We don't have the abstraction that is common within object oriented programming
- Code is written in a step by step way

- With the code being written for a specific purpose it's high performance
- Procedures are declared or defined independent of main


# Introducing main()
---
- Can have standalone function
- main() serves as an entry point
- must have a stand alone main() function, that should return an integer, an int


# Primitive
---
![[Pasted image 20250805110120.png]]


# Signed or Unsigned
----
- Types can have a qualifier signed or unsigned
- unsigned variables that only represent values greater than or equal to zero


# Literal or variable
---
- since << is left associative
- The left referenced ostream is returned and the next values in the chain added to it


- Not using namespace
	- Good practice to use, because doing so risks collisions between names in the standard library

# Scope
---
- the context of an entity, like a var
- It's where the name of the entity is visible, so we can refer to the entity
- Using a namespace brings the entities in a namespace into the current scope


# stoi
---
- The function ```stoi``` is often used to convert arguments to integer


# cin
---
```c++
# include <iostream>
using namespace std;
int main(){
	string name;
	int age;
	cout << "Enter a first name and age: ";
	cin >> name >> age;
	cout << name << " is " << age << " years old." << endl;
	return 0;
}
```

# Function
---
- Procedural suggests procedures, or functions
- Declaring sets up a relationship between a name and it's purpose
- Defining allocates memory and puts the data/code in it

- inline 
```c++
inline int square(int i){
	return i*i; 
}
```