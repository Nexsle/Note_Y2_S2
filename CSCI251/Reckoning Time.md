- Three types
	- Clocks:
		- With an epoch and tick rate
	- Time points
		- Duration of time since epoch
	- Durations: 
		- Span of time associated with some number

```c++
#include <ctime>
#include <iostream>
int main()
{
std::time_t result = std::time(nullptr);
std::cout << std::asctime(std::localtime(&result))
<< result << " seconds since the Epoch\n";
std::cout << CLOCKS_PER_SEC << std::endl;
}
```