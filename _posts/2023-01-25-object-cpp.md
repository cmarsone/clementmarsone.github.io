---
layout: post
title: Programmation Objet C++
---

### Namespace

A namespace in C++ is a *container that holds a set of identifiers*, e.g. variables, functions, classes, etc... It is used to avoid naming conflicts and to organize code into logical groups. Namespaces are declared using the `namespace` keyword followed by the namespace name, and the contents of the namespace are enclosed in curly braces. To access an identifier in a namespace, one can either qualify the identifier with the namespace name or use a `using` directive to make the contents of the namespace accessible in the current scope.

```#include <stdio.h>

int     gl_var = 1;
int     f( void ) {
    return (2);
}

namespace   Foo {

    int     gl_var = 3;
    int     f( void ) {
    return (4);
    }
}

namespace   Bar {

    int     gl_var = 5;
    int     f( void ) {
    return (6);
    }
}

namespace   Muf = Bar;

int     main( void ) {

    printf( "gl_var:        [%d]\n", gl_var );
    printf( "f():           [%d]\n\n", f() );

    printf( "Foo::gl_var:   [%d]\n", Foo::gl_var );
    printf( "Foo::f():      [%d]\n\n", Foo::f() );

    printf( "Bar::gl_var:   [%d]\n", Bar::gl_var );
    printf( "Bar::f():      [%d]\n\n", Bar::f() );

    printf( "Muf::gl_var:   [%d]\n", Muf::gl_var );
    printf( "Muf::f():      [%d]\n\n", Muf::f() );

    printf( "::gl_var:      [%d]\n", ::gl_var );
    printf( "::f():         [%d]\n\n", ::f() );

    return (0);
}```

### `stdio` streams

The term *stdio streams* refers to the standard input/output streams in the C standard library, commonly known as `stdio`. These streams provide a means of inputting and outputting data in a standardized way, and are typically implemented as buffered text streams. The three main stdio streams are:

    stdin - standard input stream, usually associated with keyboard input.
    stdout - standard output stream, usually associated with screen display.
    stderr - standard error stream, also usually associated with screen display, but used for error messages.

These streams can be read from and written to using various functions such as `printf` and `scanf` for formatted output and input, respectively. They are an important part of the C standard library and are widely used in C and C++ programming.


`#include <iostream>

int     main( void ) {

    char    buff[512];

    std::cout << "Hello World !" << std::endl;

    std::cout << "Input a word: ";
    std::cin >> buff;
    std::cout << "You entered: [" << buff << "]" << std::endl;

    return (0);
}`

### Class & instance

A class in object-oriented programming (OOP) is a blueprint or template for creating objects. It defines a set of attributes (member variables) and behaviors (member functions) that are common to all objects of that class. A class does not hold any values for its attributes, it simply defines what kind of data they can hold.

An instance, also known as an object, is a specific occurrence of a class. It holds the values for the attributes defined in the class and can perform the behaviors specified in the class. An object is created from a class by calling a special function called a constructor. Each object has its own set of values for the attributes defined in the class, and can perform the behaviors independently of other objects of the same class

In C++, a class is defined using the "class" keyword followed by the class name and the class definition, which is enclosed in curly braces. Member variables are declared within the class definition and can be either public (accessible from outside the class) or private (only accessible within the class). Member functions are also declared within the class definition and can access and manipulate the member variables.

`// Sample.class.hpp

class   Sample {

    public:
        Sample( void );
        ~Sample( void );

};`

`// Sample.class.cpp
#include <iostream>
#include "Sample.class.hpp"

Sample::Sample( void ) {

    std::cout << "Constructor called" << std::endl;
    return ;
}

~Sample::Sample( void ) {

    std::cout << "Destructor called" << std::endl;
    return ;
}`

### Member attributs & member functions

` 

...

void    Sample::bar( void ) {

    std::cout << "Member function bar called" << std::endl;
    return ;
}

int     main() {

    Sample  instance;

    instance.foo = 42;
    std::cout << "instance.foo: " << instance.foo << std::endl;

    instance.bar();

    return (0);

}`

### `this`

`#include <iostream>
#include "Sample.class.hpp"

Sample::Sample( void ) {

    std::cout << "Constructor called" << std::endl;

    this->foo = 42;
    std::cout << "this->foo: " << this->foo << std::endl;

    this->bar();

    return ;
}

Sample::~Sample( void ) {

    std::cout << "Destructor called" << std::endl;
    return ;
}

void    Sample::bar( void ) {

    std::cout << "Member function bar called" << std::endl;
    return ;
}

#ifndef SAMPLE_CLASS_H
# define SAMPLE_CLASS_H

class   Sample {

    public:

        int     foo;

        Sample( void );
        ~Sample( void );

        void    bar( void );

};

int     main() {

    Sample  instance;

    return (0);

}`

### Initialization lists

### `const`

### Encapsulation

### `class` vs `struct`

### Accessors

### Comparisons

### Non-member attributs & non-member functions

### Pointers to membersc
