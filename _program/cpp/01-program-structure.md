---
title: "Introduction to C++"
date: 2017-02-17 20:21:43.000000000 +01:00
---

As an statistician and software developer enthusiast, I believe that C++ is an excellent tool to boost your code in your preferred language for data analysis like R, python or Julia. Anyway, there are several reason why C++ is so useful, so I will share some notes for learning C++, based on the course called [Introduction to C++ on edX](https://www.edx.org/course/introduction-c-microsoft-dev210x-2).
<!-- Check the following link for more information about multi-software packages develop. -->

## What is c++?

C++ programming language was created by [Bjarne Stroustrup](http://www.stroustrup.com/C++.html), who defines C++ as a general purpose programming language with a bias towards systems programming that
- is a better C
- supports data abstraction
- supports object-oriented programming
- supports generic programming.

## Basic Program Structure of C++ Code

The structure of a C++ script is quite similar to other languages, including R, where first we declare the packages or libraries for being used in the current application and then the body. The famous first program "Hello World" is shown below.

```cpp
#include <iostream>

int main()
{
  std::cout << "Hello World!";
  return 0;
}
```

- Line 1: Pre-processor directive, locates the code for `iostream` library.
- Line 3: `main` method is required for any C++ program, it is the starting point of any application. `int` indicates that the output will be an integer.
- Line 4 and 7: Indicates the beginning and end of the `main` method body.
- Line 5: `cout` is a method that prints "Hello World" and it is found, `::`, in the `std` namespace.
- Line 7: Returns 0 if everything executes fine inside the body of `main` method.

<!-- namespace indicates where to look for an object or function. They are not neccesarily related. A header file called with `include` add files to your project, in particular libraries are integrated while namespaces do not need to. -->

## Compilation and Code Formatting

Once a C++ script is written, it is build which means that is has passes the compilation process consisting of on th work of the preprocessor, compiler and linker. In general terms, the preprocessor takes the code and made some small modifications; then the compiler takes this output checking the syntax, semantic rules, so on and accepts the promises that used things are defined in other files. Finally the linker, links the objects into an executable program ensuring that all the promises are kept.

On linux, a C++ script can be executed as follows:

```bash
g++ hello-world.cpp # build the program
./a.out # executes the output
```

The first line uses `g++` to compile the program, saving the output on the executable file `a.out` and the second line execute this file.

C++ is case sensitive.

- Preprocessor: prior tasks to code compiling.
- Directives: namespaces to include.
- Function header: Return type, function name and parameters.
- Function body: code perfomed by the function.
- Statements
- Comments
- Curly braces to enclose bodies of statements.
- Arbitrary use of whitespace.

### C++ Statements

- Declarations: variables and constants.
- Assignments: values to variables.
- Preprocessor directives: prior tasks to code compiling.
- Comments
- Function declaration
- Executable statements: e.g. `cout << "Hello Wordl!"`

## Data Types

### Numeric Data

Name | Bytes | Alias | Approximate Range
:-|:-|:-|:-
int | 4 | signed | $-2$ x $10^9$ to $2$ x $10^9$
unsigned int | 4 | unsigned | $0$ to $4$ x $10^9$
\_\_int8 | 1 | char | $-128$ to $127$
unsigned \_\_int8 | 1 | unsigned char | $0$ to $255$
\_\_int16 |2 | short, short int, signed short int | $–32,768$ to $32,767$
unsigned \_\_int16  | 2  | unsigned short, unsigned short int  | $0$ to $65,535$
\_\_int32 | 4 | signed, signed int, int | $-2$ x $10 ^ 9$ to $2$ x $10 ^ 9$
unsigned \_\_int32 | 4 | unsigned, unsigned int | $0$ to $4$ x $10 ^ 9$
\_\_int64 | 8 | long long, signed long long | $-9$ x $10^{18}$ to $9$ x $10^{18}$
unsigned \_\_int64 | 8 | unsigned long long | $0$ to $18$ x $10^{18}$
short | 2 | short int, signed short int | $–32,768$ to $32,767$
unsigned short | 2 | unsigned short int | $0$ to $65,535$
long | 4 | long int, signed long int | $-2$ x $10 ^ 9$ to $2$ x $10 ^ 9$
unsigned long | 4 | unsigned long int | $0$ to $4$ x $10 ^ 9$
long long | 8 | none | $-9$ x $10 ^ {18}$ to $9$ x $10 ^ {18}$
unsigned long long | 8 | none |  $0$ to ${18}$ x $10 ^ {18}$
float | 4 | none | 3.4E +/- 38 (7 digits)
double | 8 | none | 1.7E +/- 308 (15 digits)
long double | 8 | none | 1.7E +/- 308 (15 digits)

Note: 3.4E +/- 38 (7 digits) means that:
- the smallest positive value es $3.4$ x $10^{-38}$,
- the largest positive value es $3.4$ x $10^{38}$,
- only 7 significant decimal digits can be represented.
- Similarly for the smallest and largest negative value.
- The type names that start with a `__` character are considered non-standard types.

### Character Data

Name | Bytes | Alias | Approximate Range
:-|:-|:-|:-
char | 1 | none | -128 to 127 or 0 to 255
signed char | 1 | none | -128 to 127
unsigned char | 1 | none | 0 to 255
wchar*\_t | 2 or 4 | \_\_wchar\_t | 0 to $65\times 10^3$ or $4\times 10^9$

### Other Data

Name | Bytes | Alias | Approximate Range
:-|:-|:-|:-
bool |1 | none | true or false
enum | varies | none | dependant on the enclosed data types

## Variables and Constants

**Variables** are named memory locations. When creating them, you must provide the data type. Case sensitives, start always with a letter or underscore. Customized types can be also created. $x^2$

```cpp
int myVar = 0;
int youVar{1};
```

Be careful when assigning different data types than the defined for certain variable (assigning decimal to integer data type), because information can be lost.

**Constants** are named memory location, but their values can not be changed. They are created with `const`, and the value should be assigned when it is created.

**Explicit Type Conversion**
Using the type cast statement and cast operator `static_cast`.

```cpp
long myLong = (long)myInt;
long myLong = long(myInt);
char ch = static_cast<char>(i);   // int to char
double dbl = static_cast<double>(f);   // float to double
auto i = 3.0/2;
```

## Complex Data Types

Compound data types store more than on piece of data or more than one data type.

### Arrays

An array is collection of elements of the same type. An array of one, two and three dimension is a list, table and cube respectively. It has the following features:

- Every element contains a value.
- Indexation starts from 0.
- Its size is the number of elements.
- Single or multi-dimensional.
- Its rank is the dimension of the array.

The code below shows how to initialize, access and iterate through an array.

```cpp
//Initialize
int arrayName[10];
int arrayName[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}; // with values
int arrayName[10] = {1, 2, 3};// only some values, otherwise 0
//Accesing
int number = arrayName[2]; // value 3
//Iterating Over an Array
for (int i = 0; i < 5; i++)
{
     int number = arrayName[i];
     ...
}
```

### Strings

Last character is a null character string `\0`.

```cpp
// Basic way with character array.
char myString[5] = {'c', 'h', 'a', 'r', '\0'}
cout << myString << endl;
// Create and initialize.
char isAString[6] = "Hello";
char isAString = "Hello"; // not necessary to add the length
// With string class.
std::string myNewString = "More easy!";
```

### Structures

Arrays can only store data of the same type.

```cpp
// Declare a new structure called user.
struct user
{
     string name;
     string country;
     int age;
};
// Create an object user with initial values.
user newUser = {"David", "Peru", 13};
// Create an object without initial values.
user unkUser;
unkUser.name = "David";
unkUser.country = "Peru";
unkUser.age = 13;
std::cout << "User " + newUser.name + " is from " + newUser.country + " and " + newUser.age + " years old."
```

### Unions

Similar to structures, but can only store one piece of data at a time.

```cpp
union numericUnion
{
     int intValue;
     long longValue;
};
numericUnion myUnion;
myUnion.intValue = 3;
cout << myUnion.intValue << endl;
myUnion.longValue = 4.5;
cout << myUnion.longValue << endl;
cout << myUnion.intValue; cout << endl; // 0 because just one field is stored.
```

### Enumerations

Create symbolic constants. Common case for day of the week.

```cpp
enum Day {Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday};
// Notice that it starts from 0, but you can specify the starting value.
enum Day {Sunday = 2, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday};
Day payDay;
payDay = Thursday;
cout << payDay << endl; // shows 6, because internally they are numbers.
```

# Control Statements

## C++ Operators

Operator      | Description
:-            | :-
`+`           | addition
`-`           | subtraction
`*`           | multiplication
`/`           | division
`%`           | modulo
`+= (y += x)` | same as y = y + x
`-= (y -= x)` | same as y = y - x
`*= (y *= x)` | same as y = y * x
`++`          | increment by 1
`--`          | decrement by 1
`==`          | equal to
`!=`          | not equal to
`>`           | greater than
`<`           | less than
`>=`          | greater than or equal to
`<=`          | less than or equal to
`&&`          | logical AND
`||` | logical OR
`!`           | logical NOT

## Decision Statements

Uses conditional to set the behaviour of the program.

### `if` statement

```cpp
char response = 'y';
if (response == 'y' || response == 'Y')
{
    cout << "Positive response received" << endl;
} // if there is no curly braces, only execute the first next line.
```

### `if else` statement

```cpp
string response;
if (response == "connection_failed")
{
    // Block of code executes if the value of the response variable is "connection_failed".
}
else
{
    // Block of code executes if the value of the response variable is not "connection_failed".
}
```

### `else if` statement

```cpp
string response;
if (response == "connection_failed")
{
    // Block of code executes if the value of the response variable is "connection_failed".
}
else if (response == "connection_error")
{
    // Block of code executes if the value of the response variable is "connection_error".
}
else
{
    // Block of code executes if the value of the response variable is neither above responses.
}
```

### `switch` statement

Includes a `default` category when no other case is matched. `C++` supports `int`, `char` or `enumerations` for case option.

```cpp
char response = 'y';
switch (response)
{
   case 'y':
      // Block of code executes if the value of response is y.
      break;
   case 'Y':
      // Block of code executes if the value of response is Y.
      break;
   case 'n':
      // Block of code executes if the value of response is n.
      break;
   default:
      // Block executes if none of the above conditions are met.
      break;
}
```

### The conditional operator

Similar to `if else` operator but more compactly using three operands. The first operand evaluate the condition, the second operand is evaluated if the condition is hold; otherwise, the third operand is evaluated.

```cpp
#include <iostream>
using namespace std;
int main()
{
     int i = 1, j = 2;
     cout << ( i > j ? i : j ) << " is greater." << endl;
}
```

## Repetition statements

Repetition through the use of loops.

### `for` loop

Three main attributes that are separated by a semicolon. The first attribute indicates how to get started; the second, when to continue the loop and the last one, how to move on. This third attribute is executed at the end of each iteration.

```cpp
for ([initializer(s)]; [condition]; [iterator])
{
   // code to repeat goes here
}
```

```cpp
for (int i = 0 ; i < 10; i++)
{
  std::cout << i << endl;
}
```

### `while` loop

Executes the code while a certain condition is hold. Only includes the condition as an attribute; is up to you how to initialize and when the loop finishes.

```cpp
string response;
cout << "Enter menu choice " << endl << "More" << endl << "Quit" << endl;
cin >> response;

    while (response != "Quit")
    {
        // Code to execute if Quit is not entered

        // Prompt user again with menu choices until Quit is entered
        cout << "Enter menu choice " << endl << "More" << endl << "Quit" << endl;
        cin >> response;
    }
```

### `do` loop

Similar to a `while` loop, but the `do` loop will always execute the block of code at least once.

```cpp
string response; // response should be defined outside the loop

do
{
     cout << "Enter menu choice " << endl << "More" << endl << "Quit" << endl;
     cin >> response;

     // Process the data.

} while (response != "Quit"); // this semicolon is required
```

# Functions and Objects

## Introduction to Functions

A function is basically a bock of code with a given name. It can be called in order to execute the block of code inside this function. It could accept arguments and may return a certain value when it is executed.


```cpp
int Sum(int x, int y)
{
     return x + y;
}
```

A function can also be overloaded, which means that you can define another function with the same name and different number or arguments. Then, the compiler will call the function according to the number of arguments.

Usually, when defining a function (function prototype) you have to specify its

- storage class,
- return type,
- name,
- parameters.



