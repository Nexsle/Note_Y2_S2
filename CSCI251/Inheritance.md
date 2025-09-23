- Inheritance allows us to define a child class that inherits all the methods and properties from a parent class

```c++
class White_Hacker : public Hacker {};
```



## Multilevel Inheritance
---
- Class can also be derived from one class, which is already derived from another class

```c++
class Hacker{};

class White_Hacker: public Hacker {};

class Child_Hacker: public White_Hacker {}';
```


## Multiple Inheritance
---
A class can also be derived from more than one base class, using a comma-separated list

```c++
class Child_Hacker: public White_Hacker, public Blue {};
```

## Protected
---
Can be directly accessed by objects of subclasses, but not by arbitrary external objects


## Inheritance modes
---
- Public inheritance: makes public member of the base class remain public
- Protected inheritance: makes public member of the base class protected
- Private inheritance: makes public + protected member private


## Polymorphisms
---
- Compile-time poly:
	- Function overloading
	- Operator overloading
- Runtime
	- Function overriding
	- Virtual function
