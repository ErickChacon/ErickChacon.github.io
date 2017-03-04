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
- Line 4 and 6: Indicates the beginning and end of the `main` method body.
- Line 5: `cout` is a method that prints "Hello World" and it is found, `::`, in the `std` namespace.
- Line 7: Returns 0 if everything executes fine inside the body of `main` method.

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
int | 4 | signed | $-2$ x $10 ^ 9$ to $2$ x $10 ^ 9$
unsigned int | 4 | unsigned | $0$ to $4$ x $10 ^ 9$
_int8 | 1 | char | $-128$ to $127$
_unsigned _int8 | 1 | unsigned char | $0$ to $255$
__int16 |2 | short, short int, signed short int | $–32,768$ to $32,767$
unsigned __int16  | 2  | unsigned short, unsigned short int  | $0$ to $65,535$
__int32 | 4 | signed, signed int, int | $-2$ x $10 ^ 9$ to $2$ x $10 ^ 9$
unsigned __int32 | 4 | unsigned, unsigned int | $0$ to $4$ x $10 ^ 9$ 
__int64 | 8 | long long, signed long long | $-9$ x $10 ^ {18}$ to $9$ x $10 ^ {18}$
unsigned __int64 | 8 | unsigned long long | $0$ to ${18}$ x $10 ^ {18}$
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
