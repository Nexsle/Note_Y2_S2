# Qualifier - const, constexpr
---
- A const is used to qualify an object whose value we do not intend to change
```c++
const int shoeSize = get_size();
const int num = 43
const hvalue; // error: uninit const
```

- A reference to a const cannot be used to change the object to which the reference is bound

- Clockwise/Spiral Rule:
![[Pasted image 20250902114520.png]]


- A constant expression is one whose value cannot change and that can be evaluated at compile time
```c++
constexpr double licenseFee = 15.75;
constexpr double limitFee = licenseFee + 2.5;

//constexpr function
constexpr int newSize() {return 76};
constexpr int someVar = newSize();
```

# Auto, decltype
---
- If a var is intialised when it is declared, in such a way that its type is unambiguous, the keyword auto can be used to declare its type
```c++
auto item = val1 + val2;

```

- Auto will ordinarily ignore top level const

- Declare type automatically deduces the exact type
```c++
const int ci = 0;
decltype (ci) x = 0;
```