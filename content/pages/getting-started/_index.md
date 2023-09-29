---
content_type: page
description: This section provides a diagnostic test taken by students prior to taking
  the course and information on the recommended computing environment.
learning_resource_types: []
ocw_type: CourseSection
title: Getting Started
uid: eb6ffd3a-5e1f-1bee-46d8-bbe89130fd37
---

Course Diagnostic Test
----------------------

Prior to taking the course, students were asked to complete a {{% resource_link 41753f29-d456-9368-11a6-6993bb892916 "diagnostic test (PDF)" %}}. {{% resource_link f5d748dc-6dd9-6a9a-ab7e-751a2cef2c0b "Sample solutions to the last three problems" %}} were later provided to illustrate some of the best practices to be covered and followed during the course.

Recommended Computing Environment
---------------------------------

For learning purposes, students should use a consistent environment. Because students submitted their assignments through an online system that used gcc, the GNU compiler collection, students were recommended to use the same in their local environment.

*   **Compiler tools:** gcc, g++, make
*   **Debugging:** gdb, valgrind

Note that gcc/g++ should be at least version 4.7 or higher in order to use their more complete C++11 functionality. Everyone using these tools should also be using the following Makefile:

 `CC := gcc
CFLAGS := -O0 -g -std=c99 -Wall -Wextra -Wshadow -pedantic –Werror
CXXFLAGS := -O0 -g -std=c++11 -Wall -Wextra -Wshadow -pedantic -Weffc++ -Werror ` 

Save the above code as "Makefile" in the directory where you are compiling your program.

_Setting up a Local Environment_

*   **Windows:** The best way to get your local gcc toolchain is with [Cygwin](http://cygwin.org/). Make sure to select the 'gcc-core', 'gcc-g++', 'gdb', and 'make' packages during installation. If you would like to learn with an IDE, we recommend obtaining [Visual Studio Professional 2013](https://www.visualstudio.com/vs/professional/), which is available for free if you are a student. However, you'll still need to make sure your code compiles on gcc/g++ since that what the assignment submission system uses.
*   **OS X:** Open Xcode, go to Preferences > Downloads > Components and download "Command Line Tools".
*   **Linux:** Just install the listed tools via your usual package manager, if you don't already have them.

{{< anchor "C___Coding_Standards_and_Best_Practices" >}}{{< /anchor >}}C++ Coding Standards and Best Practices
--------------------------------------------------------------------------------------------------------------

_General Important Points_

*   **Write in a clear and consistent coding style.** You can see some examples of my code in the samples from Assignment 1 and the sample from the Diagnostic test. This is not the exact style you need to follow, but pick a style and stick with it; all of your submitted code should be formatted the same way.
*   **Code should be self-documenting.** Variables should be sensibly named, function names descriptive of their purpose. Reserve comments for places where clarification is valuable; if you have a long piece of code and it is hard to tell what it does, consider splitting it up into several functions whose names will describe what is going on.
*   **Keep your headers clean.** Put the absolute minimum required in your headers for your interface to be used. Anything that can go in a source (.cpp) file should. Don't `#include` any system headers in your .h files that are not absolutely required in that specific file.
*   **Don't expose your classes' private parts.** Keep as much of your classes private as possible. All data members should be private; mark them as such by using a leading underscore: `int _someVariable;` You can then write the getter/setter functions for this variable as `int someVariable() const;` and `int& someVariable( int value );`. Avoid `friend` functions.
*   **Use** `const` **wherever possible.** All member functions that do not modify their object should be const. If your function takes a reference to an object and does not modify that object, you should be passing a `const` reference.
*   **Write portable code.** Don't use any very compiler-specific features or depend on `long` or `unsigned` types being a particular size. Prefer to use `size_t` for array indexing, especially when dealing with the STL.
*   **Don't leak memory.** Every heap allocation using new should have a corresponding `delete`.

_Classes in C++_

*   **Follow the [rule of three](http://en.wikipedia.org/wiki/Rule_of_three_%28C%2B%2B_programming%29).** If your class needs a non-trivial destructor, you should also either implement or disable the copy constructor and copy assignment operators. (Furthermore, if you want your data to have the ability to be moved cheaply, also define the move constructor and move assignment.)
*   **Don't use global data.** Instead, encapsulate it in a class and design your interfaces effectively.
*   **Use the constructor initializer list.**

_Other_

*   **Prefer using** `nullptr` **to** `NULL`**.**
*   **Prefer using** `auto` **as long as it helps clarity.** For example, `auto dirPtr = Directory::create( "home" );` is probably better than declaring the type of `dirPtr`. Refer to [Herb Sutter's post on using auto](http://herbsutter.com/2013/08/12/gotw-94-solution-aaa-style-almost-always-auto/).
*   **Prefer uniform initialization syntax.** You should be constructing objects with curly braces whenever possible, like so: `auto someObj = SomeObject{};`.
*   **Associate asterisks and ampersands with the variable name, not data type.** Declare your pointers like `int *a, *b;`and references like `int &foo = other;`.
*   **Do take advantage of the standard library.** Generally don't try to rewrite data structures and algorithms that have already been implemented well in the standard library unless you have a good reason.