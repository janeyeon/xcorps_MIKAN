# The Simple Tutoral of C++ 11 

## 1. The Basics

### 1.1 Programs

C++ is compiled language. For a program to run, its source text has to be prodessend by a compiler, porducing object files. which are combiend by a linker yielding an executable program. 

![image-20200903200221018](/Users/yeon/Library/Application Support/typora-user-images/image-20200903200221018.png)

An executable program is created for a specific hardward/system combination; it is not portable, say, from a MAc to a Windows PC. When we talk about portability of C++ programs, we usually mean portability of source code; that is, the source code can be successfully compiled and run on a variety of systems. 

The **ISO C++** standard defines two kinds of entities: 

- <span style="color:#00bcd4">Core language features</span>, such as built-in types (char, int ) and loops (for-statements and while-statements)
- <span style="color:#00bcd4">Standard-library components</span>, such as coutainers (vector and map), and I/O operations (<< and getline())

C++ is statically typed language. That is, the type of every entity (object, value, name and expression) must be known to the compiler at its point of use. The type of an object determines the set of operations applicable to it. 

Every C++ program must have exactly one global function named <span style="color:#ffe78f"> main() </span>. The program starts by executing that function. The <span style="color:#ffe78f">int</span> integer value returned by <span style="color:#ffe78f">main()</span> , if any, is the programs's return value to "the system". If no value is returned, the system will receive a value indicating successful completion. A nonzero value from <span style="color:#ffe78f">main()</span> indicates failure. 

```cpp
#include <iostream>
int main(){
  std::cout << "Hello world!";
  return 0;
}
```

- **\#include<iostream>** : insturcts the compiler to *include* the declarations of the standard stream I/O factilities as found in **iostream** 
- **std::**  :  specifies that the name **cout** is to be found in the standard-library namespace. 

### 1.2 Functions

```cpp
Elem* next_elem();
void exit(int);
double sqrt(double);
```

- **Function declaration**  : Type of the value returnes + function name + (number and types of the arguments that must be supplied in a call)

A function declaration may contain argument names like, ` double squrt(double d)` 