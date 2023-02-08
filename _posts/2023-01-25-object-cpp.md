---
layout: post
title: C++ Object-Oriented Programming
---

### Namespace

A namespace in C++ is a *container that holds a set of identifiers*, e.g. variables, functions, classes, etc... It is used to avoid naming conflicts and to organize code into logical groups. Namespaces are declared using the `namespace` keyword followed by the namespace name, and the contents of the namespace are enclosed in curly braces. To access an identifier in a namespace, one can either qualify the identifier with the namespace name or use a `using` directive to make the contents of the namespace accessible in the current scope.

```
#include <stdio.h>

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
}
```

### `stdio` streams

The term *stdio streams* refers to the standard input/output streams in the C standard library, commonly known as `stdio`. These streams provide a means of inputting and outputting data in a standardized way, and are typically implemented as buffered text streams. The three main stdio streams are:

    stdin - standard input stream, usually associated with keyboard input.
    stdout - standard output stream, usually associated with screen display.
    stderr - standard error stream, also usually associated with screen display, but used for error messages.

These streams can be read from and written to using various functions such as `printf` and `scanf` for formatted output and input, respectively. They are an important part of the C standard library and are widely used in C and C++ programming.


```
#include <iostream>

int     main( void ) {

    char    buff[512];

    std::cout << "Hello World !" << std::endl;

    std::cout << "Input a word: ";
    std::cin >> buff;
    std::cout << "You entered: [" << buff << "]" << std::endl;

    return (0);
}
```

### Class & instance

A *class* in object-oriented programming (OOP) is a blueprint or template for creating objects. It defines a set of attributes (member variables) and behaviors (member functions) that are common to all objects of that class. A class does not hold any values for its attributes, it simply defines what kind of data they can hold.

An *instance*, also known as an *object*, is a specific occurrence of a class. It holds the values for the attributes defined in the class and can perform the behaviors specified in the class. An object is created from a class by calling a special function called a constructor. Each object has its own set of values for the attributes defined in the class, and can perform the behaviors independently of other objects of the same class

In C++, a class is defined using the `class` keyword followed by the class name and the class definition, which is enclosed in curly braces. Member variables are declared within the class definition and can be either public (accessible from outside the class) or private (only accessible within the class). Member functions are also declared within the class definition and can access and manipulate the member variables.

```
// Sample.class.hpp

class   Sample {

    public:
        Sample( void );
        ~Sample( void );

};
```

```
// Sample.class.cpp
#include <iostream>
#include "Sample.class.hpp"

Sample::Sample( void ) {

    std::cout << "Constructor called" << std::endl;
    return ;
}

~Sample::Sample( void ) {

    std::cout << "Destructor called" << std::endl;
    return ;
}
```

### Member attributs & member functions

*Member variables* (also known as member attributes or instance variables) are data members of a class, used to hold information about an object of that class. They define the state of an object.

*Member functions* (also known as methods) are functions that are members of a class and perform operations on the objects of that class. They define the behavior of an object.

In C++, a class is defined using the keyword `class` followed by the name of the class. Member variables are declared inside the class definition and can be private or public. The default access level for member variables is private. Member functions are also declared inside the class definition and can access and modify the member variables.

```
... (as above)

void    Sample::bar( void ) {

    std::cout << "Member function bar called" << std::endl;
    return ;
}
```

```
int     main() {

    Sample  instance;

    instance.foo = 42;
    std::cout << "instance.foo: " << instance.foo << std::endl;

    instance.bar();

    return (0);

}
```

### `this`

The `this` keyword in C++ is a *pointer to the current object*. It is a constant pointer that holds the memory address of the object for which the member function is called.

The `this` pointer is automatically passed to the member function by the compiler and can be used to access the member variables of the object. It can be used within any non-static member function of a class.

```
#include <iostream>
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
```

```
#ifndef SAMPLE_CLASS_H
# define SAMPLE_CLASS_H

class   Sample {

    public:

        int     foo;

        Sample( void );
        ~Sample( void );

        void    bar( void );

};
```

```
int     main() {

    Sample  instance;

    return (0);

}
```

### Initialization lists

In C++, an *initialization list* is used to initialize the member variables of an object at the time of its creation. It is a comma-separated list of initial values that are assigned to the member variables in the order in which they are declared in the class definition. The initialization list is specified in the constructor of the class using the syntax : `variable1(value1)`, `variable2(value2)`, ... after the constructor's parameters.

Initialization lists are useful in situations where the default constructor for a type is not sufficient for initializing the member variables. By using an initialization list, the member variables can be initialized to specific values in the constructor, which can improve the readability and maintainability of the code.

```
#include <iostream>

class   Sample1 {

    public:

        char    a1;
        int     a2;
        float   a3;

        Sample1( char p1, int p2, float p3 );
        ~Sample1( void );

};
```

```
Sample1::Sample1( char p1, int p2, float p3 ) {

    std::cout << "Constructor called" << std::endl;

    this->a1 = p1;
    std::cout << "this->a1 = " << this->a1 << std::endl;

    this->a2 = p2;
    std::cout << "this->a2 = " << this->a2 << std::endl;

    this->a3 = p3;
    std::cout << "this->a3 = " << this->a3 << std::endl;

    return ;
}

Sample1::~Sample1( void ) {

    std::cout << "Destructor called" << std::endl;
    return ;
}
```

```
class   Sample2 {

    public:

        char    a1;
        int     a2;
        float   a3;

        Sample2( char p1, int p2, float p3 );
        ~Sample2( void );

};
```

```
Sample2::Sample2( char p1, int p2, float p3 ) : a1(p1), a2(p2), a3(p3) {

    std::cout << "Constructor called" << std::endl;

    std::cout << "this->a1 = " << this->a1 << std::endl;
    std::cout << "this->a2 = " << this->a2 << std::endl;
    std::cout << "this->a3 = " << this->a3 << std::endl;

    return ;
}

Sample2::~Sample2( void ) {

    std::cout << "Destructor called" << std::endl;
    return ;
}
```

```
int         main() {

    Sample1 instance1( 'a', 42, 4.2f );
    Sample2 instance2( 'z', 13, 3.14f );

    return (0);

}
```

### `const`

In C++, the `const` keyword is used to declare a variable as constant, meaning its value cannot be changed after initialization. When used before a variable or function declaration, it indicates that the variable or function is constant and its value cannot be modified.

```
#include <iostream>

class   Sample {

    public:

        float const pi;
        int         qd;

        Sample( float const f );
        ~Sample( void );

        void    bar( void ) const;

};
```

```
Sample::Sample( float const f ) : pi( f ), qd( 42 ) {

    std::cout << "Constructor called" << std::endl;
    return ;
}

Sample::~Sample( void ) {

    std::cout << "Destructor called" << std::endl;
    return ;
}

void Sample::bar( void ) const {

    std::cout << "this->pi: " << this->pi << std::endl;
    std::cout << "this->qd: " << this->qd << std::endl;

    return ;
}
```

```
int         main() {

    Sample instance( 3.14f );

    instance.bar();

    return (0);

}
```

### Encapsulation

In encapsulation, the data members of a class are declared as private, and the class provides public methods (member functions) to access and manipulate the data. This way, the implementation details of the class are hidden from the outside world and can be changed without affecting the users of the class. The public methods act as an interface between the class and its users, ensuring that the class's behavior is predictable and consistent.

Encapsulation provides several benefits, including improved data protection and security, reduced complexity, and better maintenance. It also makes it easier to change the implementation of a class without affecting its users, which can be especially useful for large projects.

### `class` vs `struct`

*Default Member Access*: In a struct, the members are public by default, while in a class they are private by default.
*Syntax*: Classes and structs are declared using different keywords, class and struct, respectively.
*Use*: In practice, the distinction between structs and classes is largely a matter of convention and programming style. Structs are often used to define simple data structures, while classes are used to define more complex data structures with member functions.

### Accessors

Accessors are member functions in a `class` or `struct` that allow you to access and manipulate the private data members of an object. They are also known as getters and setters.

1. *Getters* (Accessors): Getters, also known as accessors, are used to retrieve the value of a private data member. They are defined as member functions with the keyword `get` in their names.
2. *Setters*: Setters are used to modify the value of a private data member. They are defined as member functions with the keyword `set` in their names. 
    
Accessors are used to protect the internal representation of an object from direct modification, making it easier to maintain and change the implementation without affecting the code that uses the object.

```

#ifndef SAMPLE_CLASS_H
# define SAMPLE_CLASS_H

class   Sample {

    public:

        Sample( void );
        ~Sample( void );

        int     getFoo( void ) const;
        void    setFoo( int v );

    private:

        int     _foo;

};

#endif
```

```
#include <iostream>
#include "Sample.class.hpp"

Sample::Sample( void ) {

    std::cout << "Constructor called" << std::endl;

    this->setFoo( 0 );
    std::cout << "this->getFoo(): " << this->getFoo() << std::endl;
    return ;
}

Sample::~Sample( void ) {

    std::cout << "Destructor called" << std::endl;
    return ;
}

int    Sample::getFoo( void ) const {

    return this->_foo;
}


void    Sample::setFoo( int v ) {

    if (v >= 0)
        this->_foo = v;

    return ;
}
```

```
#include <iostream>
#include "Sample.class.hpp"

int     main() {

    Sample  instance;

    instance.setFoo( 42 );
    std::cout << "instance.getFoo(): " << instance.getFoo() << std::endl;
    instance.setFoo( -42 );
    std::cout << "instance.getFoo(): " << instance.getFoo() << std::endl;

    return (0);

}
```

### Comparisons

### Non-member attributs & non-member functions `static`

"Non-member" refers to functions or variables that are not associated with a class in object-oriented programming.

Non-member functions are standalone functions that are not part of a class and do not have access to the private data of the class. They are usually used to perform tasks that do not need access to the class's data and can operate on data passed as arguments.

Non-member variables are variables that are not part of a class, but are global to the program. They can be accessed by any function or class in the program.

In general, non-member functions and variables can provide a more modular and reusable design for a program. However, they should be used with caution to avoid global state problems, such as namespace collisions, unintended side effects, and loss of encapsulation.

### Pointers to members

Pointers to members are a type of pointer in C++ that can be used to refer to class member functions or data members. They provide a way to manipulate members of an object directly, without using the object's public interface.

Pointers to member functions are declared using the same syntax as normal function pointers, but with an additional class name before the function name.

#### `noexecpt`

The `noexecpt` keyword in C++ is used to indicate that a function does not throw any exceptions. When a function is declared with `noexecpt`, the compiler will generate faster code for this function and the program will perform better. Additionally, if an exception is thrown from within a `noexecpt` function, the program will terminate immediately. This keyword can be used in function declarations, function templates, and exception specifications.
