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
