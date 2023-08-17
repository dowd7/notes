What is the function called when the program is run?

- main

What is the standard input stream in C++?

- cin

What would this program print out? 

```c++
int x;
    cout<<x;
```

- A random integer


```c++
#include <iostream>

using namespace std;

int main()
{
    cout << "Hello world!" << endl;
    
    return 0;
}
```

simple calculator
```c++
#include <iostream>

using namespace std;

int main()
{
    int a;
    int b;

    int sum;

    cout << "Enter a number:" << endl;
    cin >> a;

    cout << "Enter a number:" << endl;
    cin >> b;

    sum = a+b;

    cout << "The sum is " << sum << endl;

    return 0;
}
```
