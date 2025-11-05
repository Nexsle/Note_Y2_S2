Capture list
```c++
int target = 3;

auto testing = [target] (int num) { cout << target << endl};
```

\[x, &y] : pass x by value, y by reference
\[&] : pass all needed externals by reference
\[=] : pass all needed external by value
\[&, x]: pass x by value and others by reference
\[=,&z] pass z by reference and others by value

