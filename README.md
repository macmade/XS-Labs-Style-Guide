XS-Labs Coding Style Guide for C, C++, Objective-C and x86 Assembly
===================================================================

[![Issues](http://img.shields.io/github/issues/macmade/XS-Labs-Style-Guide.svg?logo=github)](https://github.com/macmade/XS-Labs-Style-Guide/issues)
![Status](https://img.shields.io/badge/status-active-brightgreen.svg?logo=git)
![License](https://img.shields.io/badge/license-bsd-brightgreen.svg?logo=open-source-initiative)  
[![Contact](https://img.shields.io/badge/follow-@macmade-blue.svg?logo=twitter&style=social)](https://twitter.com/macmade)
[![Sponsor](https://img.shields.io/badge/sponsor-macmade-pink.svg?logo=github-sponsors&style=social)](https://github.com/sponsors/macmade)

Table Of Contents
-----------------

 1. [About](#about)
 1. [License](#license)
 1. [C Style Guide](#c)
 1. [C++ Style Guide](#cpp)
 1. [Objective-C Style Guide](#objc)
 1. [x86 Assembly Style Guide](#asm)

<a name="about"></a>
About
-----

These are the coding conventions used for all recent [XS-Labs](http://www.xs-labs.com/) projects.  
Feel free to comment, raise issues, fork and/or adapt this document.

### Note about whitespaces

XS-Labs' coding conventions make a heavy use of whitespaces.  
It's not a common habit among coders, who usually prefers compact code.

This is just a personal taste.  
After years of professional development, I like to see a lot of spaces in my own code. It's like letting the code breath.   
Code is about rhythm, and readability. And I think taking time to carefully align operators, declarations, etc. improves the overall readability and the feeling you can get while reading code.

<a name="license"></a>
License
-------

This style guide is published under the terms of the [FreeBSD documentation license](http://www.freebsd.org/copyright/freebsd-doc-license.html).

<a name="c"></a>
C Style Guide
-------------

  1.  [Indentation](#c-1)
  2.  [Ending line](#c-2)
  3.  [Comments](#c-3)
  4.  [Maximum number of columns](#c-4)
  5.  [Includes](#c-5)
  6.  [Whitespace](#c-6)
      1. [Operators](#c-6-1)
      2. [Parenthesis and brackets](#c-6-2)
      3. [Pointers](#c-6-2)
      4. [Casts](#c-6-4)
      5. [`for` loops](#c-6-5)
  7.  [Braces](#c-7)
  8.  [Alignment](#c-8)
      1. [Assignments](#c-8-1)
      2. [Variable declarations](#c-8-2)
      3. [Single line conditionals](#c-8-3)
      4. [Array subscripting operator](#c-8-4)
  9.  [Case and symbols naming](#c-9)
  10. [Variable declaration](#c-10)
  11. [Macros](#c-111)
  12. [Structures and unions](#c-12)
  13. [Enumerated types](#c-13)
  14. [Typedefs](#c-14)
  15. [New lines](#c-14)
  16. [Header guards](#c-16)
  17. [Functions prototypes](#c-17)
  18. [Functions with no parameters](#c-18)
  19. [Inline functions](#c-19)
  20. [Dereferencing](#c-20)
  21. [Conditionals](#c-21)
  22. [Switch statements](#c-22)
  23. [Long `if/else if` statements](#c-23)
  24. [C++ compatibility](#c-24)
  25. [Inline documentation](#c-25)
  26. [Compilation](#c-26)

<a name="c-1"></a>
### 1. Indentation

Code should always be indented using four spaces.  Never use tabulations for indentation.

Preprocessor directives should also be indented:

```C
void foo( void )
{
    #ifdef FOO
    /* ... */
    #endif
}
```

Not:

```C
void foo( void )
{
#ifdef FOO
    /* ... */
#endif
}
```

<a name="c-2"></a>
### 2. Ending line

Source and header files should always end with a single empty line.

<a name="c-3"></a>
### 3. Comments

Comments should always use the `/* */` notation.  
Single line C++ style comments (`//`) are strictly prohibited.

A line of comment should whenever possible be no more that 80 columns.

When a comment consists of a single line, place the `/* */` on the same line.  
If the comments consists of multiple lines, place the `/* */` on a new line:

```C
/* Single line comment */

/*
 * Multiple
 * line
 * comment
 */
```

When using multiple line comments, always align the `*` signs, as in the above example.

<a name="c-4"></a>
### 4. Maximum number of columns

The number of columns for a single line is not limited.  
However, try whenever possible to wrap long lines in order to improve the overall readability.

<a name="c-5"></a>
### 5. Includes

Include directives should always come first, before any other declaration:

```C
#include <stdio.h>

int x;
```

Not:

```C
int x;

#include <stdio.h>
```

An exception is made when a header needs a specific macro to be set before inclusion:

```C
#define FOOBAR 1 /* Permitted */

#include <foobar.h>
```

<a name="c-6"></a>
### 6. Whitespace

<a name="c-6-1"></a>
#### 6.1 Operators

A single whitespace character should always be used around all operators except unary operators:

```C
x = 1 + 2 + 3;

x++;
~x;

if( !x )
{
    /* .... */
}
```

Not:

```C
x=1+2+3;

x ++;
~ x;

if( ! x )
{
    /* .... */
}
```

<a name="c-6-2"></a>
#### 6.2 Parenthesis and brackets

A single whitespace character should always be used inside parenthesis and brackets, but never before:

```C
x[ 0 ] = 0;

foo( x );

if( y == 0 )
{
    /*  */
}
```

Not:

```C
x[0] = 0;

foo (x);

if (y == 0)
{
    /*  */
}
```

<a name="c-6-3"></a>
#### 6.3 Pointers

The pointer sign should alway have a leading and trailing space:

```C
int * x;
```

Not:

```C
int* x;
int *x;
```

<a name="c-6-4"></a>
#### 6.4 Casts

No whitespace should be added after a cast. A single whitespace should be used after the opening parenthesis and before the closing one:

```C
x = ( char * )y;
```

Not:

```C
x = ( char * ) y;
```

<a name="c-6-5"></a>
#### 6.5 `for` loops

When using `for` loops, a single whitespace character should be used after the semicolons:

```C
for( i = 0; i < 10; i++ )
{
    /* ... */
}
```

Not:

```C
for( i = 0;i < 10;i++ )
{
    /* ... */
}
```

<a name="c-7"></a>
### 7. Braces

Braces should always be placed on an empty line.  
This apply for all constructs (functions, conditions, loops, etc.).  
Code inside braces should be indented by four spaces:

```C
void foo( void )
{
    if( ... )
    {
    	/* ... */
    }
    else if( ... )
    {
    	/* ... */
    }
    else
    {
    	/* ... */
    }
    
    for( ... )
    {
    	/* ... */
    }
    
    while( ... )
    {
    	/* ... */
    }
    
    do
    {
    	/* ... */
    }
    while( ... );
}
```

An exceptions can be made for very simple constructs:

```C
     if( ... ) { x = 1; }
else if( ... ) { x = 2; }
```

<a name="c-8"></a>
### 8. Alignment

<a name="c-8-1"></a>
#### 8.1 Assignments

Always align consecutive assignments:

```C
x       = 1;
foo     = 2;
foobar += 2;
```

Not:

```C
x = 1;
foo = 2;
foobar += 2;
```

If using multiple lines in an assignment, aligns the extra lines to the equal sign:

```C
x      = 1;
foobar = x
       + 1
       + 2;
```

When using conditional assignment, aligns the `?` and `:` signs whenever possible.  
The `?` sign should be aligned by adding whitespaces before the closing parenthesis:

```C
x      = 1;
foobar = ( x      ) ? 2      : x + 3;
foo    = ( foobar ) ? foobar : x;
```

Not:

```C
x      = 1;
foobar = ( x ) ? 2 : x + 3;
foo    = ( foobar ) ? foobar : x;
```

<a name="c-8-2"></a>
#### 8.2. Variable declarations

Always aligns the names of variables:

```C
int           x;
unsigned long y;
float         z;
```

Not:

```C
int x;
unsigned long y;
float z;
```

When using pointers, place the pointer sign next to the variable name:

```C
int           * x;
unsigned long * y;
```

<a name="c-8-3"></a>
#### 8.3. Single line conditionals

If using single line conditional statements (see above), align the `if`/`else` statements, as well as the opening/closing braces and comparison operators:

```C
     if( x      == 1 ) { foobar = 1;          }
else if( foobar == 1 ) { x      = 0xFFFFFFFF; }
else                   { x      = 0;          }
```

Not:

```C
if( x == 1 ) { foobar = 1; }
else if( foobar == 1 ) { x = 0xFFFFFFFF; }
else { x = 0; }
```

<a name="c-8-4"></a>
#### 8.4. Array subscripting operator

Always align the closing brackets when using the array subscripting operator. Indexes should be indented in a logical manner:

```C
x[   1 ] = 0;
x[ 100 ] = 0;
```

Not:

```C
x[ 1 ]   = 0;
x[ 100 ] = 0;
```

<a name="c-9"></a>
### 9. Case and symbols naming

Local variables should never start with an underscore, and should always start with a lowercase letter.  
Lower camel-case is recommended.

For global symbols (variables and functions), upper camel-case is usually recommended.  
Underscores may be used to simulate namespaces.

```C
void SomePackage_SomePublicFunction( void );

extern int SomeInteger;
```

Symbols shall never start with two underscores, or with an underscore followed by an uppercase letter.

<a name="c-10"></a>
### 10. Variable declaration

Local variables should be declared before any other statement:

```C
void foo( void )
{
    int x = 0;
    int y = 1;
    
    foo();
    foobar();
}
```

Not:

```C
void foo( void )
{
    bar();
    
    int x = 0;
    
    foobar();
    
    int y = 0;
}
```

If you need to delcare variables after a statement, always use a dedicated scope:

```C
void foo( void )
{
    int x = 0;
    
    foo();

    {
        int y = 1;
        
        foobar();
    }
}
```

The rules above do not apply to `for` loops, where a variable delcaration is permitted and recommended:

```C
for( int i = 0; i < 10; i++ )
{
    /* ... */
}
```

Not:

```C
int i;

for( i = 0; i < 10; i++ )
{
    /* ... */
}
```

<a name="c-11"></a>
### 11. Macros

Macros should always be in uppercase.

```C
#define FOO         1
```

If a macro takes parameters, the parameters names should begin and end with a single underscore:

```C
#define BAR( _x_ )  ( ( _x_ ) + 1 )
```

As in the above example, parenthesis should always be used around a macro parameter.

<a name="c-12"></a>
### 12. Structures and unions

Members of structures and unions should be properly aligned, as mentioned before:

```C
struct foo
{
	int           x;
	unsigned long y;
};

union bar
{
	int           x;
	unsigned long y;
};
```

When manually padding a struct, use a leading underscore for the member name, and a trailing number, prefixed with a single underscore.  
Always use a `char` array to manually pad a structure:

```C
struct foo
{
	char s;
	char _pad_0[ 3 ];
	int  x;
};
```

<a name="c-13"></a>
### 13. Enumerated types

Enum values should be properly aligned, as mentioned before.  
If using explicit values, hexadecimal notation is preferred:

```C
enum
{
	Foo    = 0x01,
	Bar    = 0x02,
	Foobar = 0x10
};
```

Not:

```C
enum
{
	Foo,
	Bar,
	Foobar = 0x10
};
```

When using flags, the left shift operator is recommended:


```C
enum
{
	Foo    = 1 << 0,
	Bar    = 1 << 1,
	Foobar = 1 << 2
};
```


<a name="c-14"></a>
### 14. Typedefs

Simple typedefs are declared on a single line:

```C
typedef int foo;
```

With structures, unions and enumrated types place the type name on a new line:

```C
typedef struct
{
    int x;
    int y;
}
foo;
```

For enumrated types, each value should be prefixed by the type name:

```C
typedef enum
{
    FooX = 0,
    FooY = 1,
    FooZ = 2
}
Foo;
```

Not:

```C
typedef enum
{
    X = 0,
    Y = 1,
    Z = 2
}
Foo;
```

<a name="c-15"></a>
### 15. New lines

An empty line should be used to separate logical parts of the code, as well as to separate function calls and assignments:

```C
x = 0;
y = 0;

foo();

z = 2;
```

Not:

```C
x = 0;
y = 0;
foo();
y = 2;
```

<a name="c-16"></a>
### 16. Header guards

All headers should be properly guarded:

```C
#ifndef FOO_H
#define FOO_H

/* ... */

#endif /* FOO_H */
```

The name of the macro used as header guard should always be in uppercase.  
It should consist of the name of the header file (optionally with directories prefixes, separated by a single underscore), and a trailing `_H`.

For instance, for `include/foo/bar/foobar.h`, this should be `FOO_BAR_FOOBAR_H`.

<a name="c-17"></a>
### 17. Functions prototypes

Function prototypes should always declare the parameters names.  
A single whitespace character should be used after the coma separating parameters.  
The return type should be place on the same line as the function's name:

```C
void foo( int x, int y );
```

Not:

```C
void
foo( int,int );
```

<a name="c-18"></a>
### 18. Functions with no parameters

Functions without parameters should always be declared as taking `void`:

```C
void foo( void );
```

Not:

```C
void foo();
```

<a name="c-19"></a>
### 19. Inline functions

Inline functions should generally be avoided, unless there's a very good and specific reason to make them inline.

<a name="c-20"></a>
### 20. Dereferencing

When using the dereference operator `*`, always use an extra set of parenthesis:

```C
*( x ) = 1;
y      = *( x );
```

Not:

```C
*x = 1;
y  = *x;
```

<a name="c-21"></a>
### 21. Conditionals

Always use braces with conditionals:

```C
if( x == 1 )
{
    x = 2;
}
```

Not:

```C
if( x == 1 )
    x = 2;
```

Don't use `else` clauses when not necessary:

```C
if( x == 0 )
{
    return true;
}

return false;
```

Not:

```C
if( x == 0 )
{
    return true;
}
else
{
	return false;
}
```

Also avoid using `!` in a conditional:

```C
if( b == false || p == null )
{
    /* ... */
}
```

Not:

```C
if( !b || !p )
{
    /* ... */
}
```

<a name="c-22"></a>
### 22. Switch statements

When using switch statements, separate each `case` with an empty line and adds an empty line after the `case`.  
The `break` statement should be indented, in regard to the `case` statement.

```C
switch( x )
{
    case 1:
        
        /* ... */
        break;
        
    default:
        
        /* ... */
        break;
}
```

An exception can be made for very simple switch statements:

```C
switch( x )
{
    case 1:  y      = 0;          break;
    default: foobar = 0xFFFFFFFF; break;
}
```

In such a case, `break` statements should be aligned, as well as assignment operators, if any.

<a name="c-23"></a>
### 23. Long `if`/`else if` statements

Very long `if`/`else if` statements should be wrapped the following way:

```C
if
(
       x      == 1
    && y      == 2
    && foobar == 3
)
{
   /* ... */
}
```

Parenthesis are placed on a new line. Variable names and comparison operators should be aligned.

When using extra parenthesis, apply the same rules:

```C
if
(
       x == 1
    && y == 2
    &&
    (
          z      == 3
       || foobar == 4
    )
)
{
   /* ... */
}
```

<a name="c-24"></a>
### 24. C++ compatibility

All headers should be compatible with C++, using `extern "C"`:

```C
#ifdef __cplusplus
extern "C" {
#endif

/* ... */

#ifdef __cplusplus
}
#endif
```

<a name="c-254"></a>
### 25. Inline documentation

Documented code should prefer [Apple's HeaderDoc](https://developer.apple.com/library/mac/documentation/DeveloperTools/Conceptual/HeaderDoc/intro/intro.html) syntax rather than JavaDoc.

<a name="c-26"></a>
### 26. Compilation

Always compiles your code with `-Werror` or similar, and always use the highest possible error reporting level.

When function parameters are not used, cast them to `void` to prevent a warning:

```C
void foo( int unused )
{
    ( void )unused;
}
```

<a name="cpp"></a>
C++ Style Guide
---------------

**All rules from the C Style Guide applies here, with a few exceptions and additions described hereafter.**

  1.  [Files and files extensions](#cpp-1)
  2.  [Comments](#cpp-2)
  3.  [Namespaces](#cpp-3)
  4.  [Classes](#cpp-4)
     1. [Naming](#cpp-4-1)
     2. [Inheritance](#cpp-4-2)
     3. [Members](#cpp-4-3)
     4. [Method definitions](#cpp-4-4)
     5. [Destructors](#cpp-4-5)
  5.  [Templates](#cpp-5)
  6.  [Using](#cpp-6)
  7.  [Variable declaration](#cpp-7)
  8.  [Function/method arguments](#cpp-8)
  9.  [Lambdas](#cpp-9)
  10. [Enumerated types](#cpp-10)
  11. [Includes and forward declarations](#cpp-11)
  12. [Using C functions](#cpp-12)

<a name="cpp-2"></a>
### 1. Files and files extensions

C++ source files should end with the `.cpp` extension.  
C++ headers should end with the `.hpp` extension.

Source and header files for classes should be named as the classes they declare/define.  
Namespaces should be represented as directories.

<a name="cpp-2"></a>
### 2. Comments

Single line C++ comments are allowed, even if the `/*  */` notation is usually preferred, especially when the comment consists of multiple lines.

<a name="cpp-3"></a>
### 3. Namespaces

Namespaces should always follow the upper camel-case rule.

<a name="cpp-4"></a>
### 4. Classes

<a name="cpp-4-1"></a>
#### 4.1. Naming

C++ classes should always follow the upper camel-case rule.  
Properties should always follow the lower camel-case rule.  
Methods should follow either the upper camel-case rule or the lower camel-case rule, but mixing both in the same project is not allowed.

Private members should always have a leading underscore.

<a name="cpp-4-2"></a>
#### 4.2. Inheritance

The `:` sign should immediately follow the class name and should be followed by a single whitespace character.  
When inheriting from multiple classes, a single whitespace character should be used after the comma:

```C++
class FooBar: Foo, Bar
{
	
};
```

<a name="cpp-4-3"></a>
#### 4.3. Members

Public members should be declared first, followed by protected and private members.  
Always group members with the same visibility (properties and methods), unless it is not possible.  

Static members should also be declared first, inside the visibility group, followed by methods and properties.  
Separate static methods, methods and properties by an empty line.

The `public`, `protected` and `private` keywords should be indented by four spaces and an empty line should be placed directly after.  
Members should be indented by four more spaces:

```C++
class Foo
{
    public:
        
        static void staticMethod( void );
        
        Foo( void );
        
        int           x;
        unsigned long y;
        
    private:
        
        void _bar( void );
        
        int _z;
};
```

<a name="cpp-4-4"></a>
#### 4.4. Method definitions

Except for templates, method should never be defined in the header files.

<a name="cpp-4-5"></a>
#### 4.5. Destructors

Destructors should always be declared as `virtual`, unless there's a very good and specific reason not to do so.

<a name="cpp-5"></a>
### 5. Templates

Template parameters should be surrounded by a single whitespace character.  
A single whitespace character should be used after the comma.  
The `<` sign should immediately follow the class name:

```C++
template class Foo< int x, int y >
{
    
};
```

<a name="cpp-6"></a>
### 6. Using

The `using` keyword is usually discouraged for namespaces, except for very long namespaces.  
It's strictly prohibited for the `std` namespace - the full notation should always be used.

```C++
std::vector< int > v;
```

Not:

```C++
using std;

vector< int > v;
```

<a name="cpp-7"></a>
### 7. Variable declaration

Variables may be declared with a value.  
In such a case, parenthesis should be preferred over the equal sign.  

```C++
int x( 0 );
```

Over:

```C++
int x = 0;
```

Using braces is also allowed.  
In such a case, always add a leading space before the opening brace:

```C++
int x {};
int y { 42 };
```

Not:

```C++
int x{};
int y{ 42 };
```

<a name="cpp-8"></a>
### 8. Function/method arguments

Except for out parameters, primitive or integral types should always be passed by value.  
For other types, passing `const` references is preferred:

```C++
void foo( int value );
void bar( const std::string & value );
```

Over:

```C++
void foo( const int & value );
void bar( std::string value );
```

<a name="cpp-9"></a>
### 9. Lambdas

When using lambdas, a single space should be placed before and after any capture.  
A single space should be placed after the comma in the capture list.  
When there is no capture, no space should be placed inside the brackets:

```C++
auto a = []( void )            {};
auto b = [ & ]( void )         {};
auto c = [ this ]( void )      {};
auto c = [ this, foo ]( void ) {};
```

Not:

```C++
auto a = [ ]( void )        {};
auto b = [&]( void )        {};
auto c = [this]( void )     {};
auto c = [this,foo]( void ) {};
```

No space should be placed between the capture brackets and the opening parenthesis for arguments.  
When the lambda doesn't take arguments, always use `( void )`, as for functions:

```C++
auto a = []( int x ) {};
auto b = []( void )  {};
```

Not:

```C++
auto a = [](int x) {};
auto b = []        {};
```

The return type may be omitted.  
If specified, a leading and trailing space should be placed around `->`:


```C++
auto a = []( void ) -> int {};
```

Not:

```C++
auto a = []( void )->int {};
```

<a name="cpp-10"></a>
### 10. Enumerated types

Scoped enumerations should always be preferred over unscoped enumerations:

```C++
enum class Foo
{
	X
	Y
};
```

Over:

```C++
enum Foo
{
	FooX
	FooY
};
```

<a name="cpp-11"></a>
### 11. Includes and forward declarations

The number of included files contained in the headers should be limited.  
Always use forward declarations when possible:

```C++
class Foo;

class Bar
{
    public:
        
        Bar( Foo * f );
};
```

Not:

```C++
#include "Foo.h"

class Bar
{
    public:
        
        Bar( Foo * f );
};
```

<a name="cpp-12"></a>
### 12. Using C functions

The use of C functions is generally discouraged unless there's no C++ equivalent, or if there's a specific reason not to use a C++ equivalent.

C library headers should not be used directly. Always use the C++ variants instead, when available:

```C++
#include <cstdio>
```

Not:

```C++
#include <stdio.h>
```

<a name="objc"></a>
Objective-C Style Guide
-----------------------

**All rules from the C Style Guide applies here, with a few exceptions and additions described hereafter.**

  1.  [Files](#objc-1)
  2.  [Primitive datatypes](#objc-2)
  3.  [Bracket notation](#objc-3)
  4.  [Literals](#objc-4)
  5.  [Constants](#objc-5)
  6.  [Enumerated types](#objc-6)
  7.  [`NULL`, `nil` and `Nil`](#objc-7)
  8.  [Blocks](#objc-8)
  9.  [Classes](#objc-9)
      1.  [Naming](#objc-9-1)
      2.  [Interface declaration](#objc-9-2)
      3.  [Instance variables](#objc-9-3)
      4.  [Properties](#objc-9-4)
      5.  [Properties atomicity](#objc-9-5)
      6.  [Methods](#objc-9-6)
      7.  [Imports and forward declarations](#objc-9-7)
      8.  [Private methods](#objc-9-8)
      9.  [Categories](#objc-9-9)
      10. [Protocols](#objc-9-10)
  10. [Singletons/Shared instances](#objc-10)
  11. [NSLog](#objc-11)
  12. [Multithreading](#objc-12)
  13. [Compilation](#objc-13)

<a name="objc-1"></a>
### 1. Files

Source and header files for classes should be named as the classes they declare/define.  
Directories should be used to separate logical groups of source files.

For categories, the source and header files should be name as the class, followed by a `+` and the category name (`SomeClass+SomeCategory.m`).

<a name="objc-2"></a>
### 2. Primitive datatypes

Unless there's a specific need to do so, never use the C primitive datatypes.  
The Objective-C equivalent should always be preferred:

  * `NSInteger` instead of `int` or `long`
  * `NSUInteger` instead of `unsigned int` or `unsigned long`
  * `CGFloat` instead of `float` or `double`

Or use the types from `stdint.h` when needed.

<a name="objc-3"></a>
### 3. Bracket notation

When sending messages, a single whitespace should be used before and after the brackets:

```Objective-C
a = [ [ NSArray alloc ] init ];
```

Not:

```Objective-C
a = [[NSArray alloc]init];
```

Long lines should be wrapped the following way:

```Objective-C
a = [ [ NSDictionary alloc ] initWithObjects: obj1,
                                              obj2,
                                              obj3,
                                              nil
                             forKeys:         @"key1",
                                              @"key2",
                                              @"key3",
                                              nil
    ];
```

The closing bracket is aligned with the opening one.  
Parts of the method name are aligned to the left, as well as arguments.

<a name="objc-5"></a>
### 5. Literals

The use of literals is generally encouraged, as well as subscripting:

```Objective-C
array      = @[ obj1, obj2 ];
dictionary = @{ @"key1" : obj1, @"key2" : obj2 };
number     = @42;
```

Instead of:

```Objective-C
array      = [ NSArray arrayWithObjects: obj1, obj2, nil ];
dictionary = [ NSDictionary dictionaryWithObjectsAndKeys: obj1, @"key1", obj2, @"key2", nil ];
number     = [ NSNumber numberWithInteger: 42 ];
```

Long declarations for array or dictionaries literals should be wrapped the following way:

```Objective-C
array      = @[
                  obj1,
                  obj2
              ];
dictionary = @{
                  @"key1"   : obj1,
                  @"key2"   : obj2,
                  @"foobar" : obj2
              };
```

The opening and closing brackets/braces are aligned.  
Contained objects are placed on their own line, indented by four spaces.

Fo dictionaries, the `:` signs are aligned.

<a name="objc-6"></a>
### 6. Constants

The use of the `k` prefix for constants is prohibited.  
When related to a class, constants should be prefixed by the class name.

The name of constants should follow the upper camel-case rule.

The use of the `extern` keyword is strictly prohibited for constants. Use the `FOUNDATION_EXPORT` macro instead:

```Objective-C
FOUNDATION_EXPORT NSString * const SomeClassConstantName;
```

Not

```Objective-C
extern NSString * const kConstantName;
```

<a name="objc-7"></a>
### 7. Enumerated types

The use of the `NSEnum` and `NSOptions` macros is encouraged, while not mandatory.

<a name="objc-8"></a>
### 8. `NULL`, `nil` and `Nil`

`NULL`, `nil` and `Nil` should not be used interchangeably.

`nil` should always be used for instances, while `Nil`should be used for classes.  
For any other pointer type, `NULL` should be used.

<a name="objc-9"></a>
### 9. Blocks

The declaration of a block should follow the same rules as the declaration of a function pointer:

```Objective-C
NSUInteger ( ^ blockName )( NSUInteger x );
```

The `^` sign is surrounded by a single whitespace character.  
For complex blocks, a typedef is recommended:

```Objective-C
typedef NSUInteger ( ^ blockTypeName )( NSUInteger x );
```

The definition of blocks should follow the function's definition style.  
No whitespace should be placed after the `^` sign.  
Block's code should be indented by four spaces.

```Objective-C
block = ^( void )
{
    /* ... */
};
```

Blocks without arguments should always be defined as taking `void`.

<a name="objc-9"></a>
### 9. Classes

  1.  [Naming](#objc-9-1)
  2.  [Interface declaration](#objc-9-2)
  3.  [Instance variables](#objc-9-3)
  4.  [Properties](#objc-9-4)
  5.  [Properties atomicity](#objc-9-5)
  6.  [Methods](#objc-9-6)
  7.  [Imports and forward declarations](#objc-9-7)
  8.  [Private methods](#objc-9-8)
  9.  [Categories](#objc-9-9)
  10. [Protocols](#objc-9-10)

<a name="objc-9-1"></a>
#### 9.1. Naming

The name of classes should follow the upper camel-case rule.

<a name="objc-9-2"></a>
#### 9.2. Interface declaration

The interface declaration should follow the following rules:

Instance variabes are prohibited in the interface (see [9.3. Instance variables](#objc-9-3)).

Properties and methods should not be indented.  
Properties should come first, followed by methods.

The `:` sign after the class name should have a trailing whitespace character, but never a leading one.

If protocols are implemented, the opening `<` sign should have a leading and trailing whitespace character.  
The closing `>` sign should have a leading whitespace character.  
A single whitespace character should be placed after the comma, when implementing multiple protocols.

Example:

```Objective-C
@interface Foobar: NSObject < Foo, Bar >

@property( atomic, readonly ) NSInteger x;

- ( void )foo;

@end
```

<a name="objc-9-3"></a>
#### 9.3. Instance variables

Instance variables should follow the lower camel-case rule and start with a single leading underscore.

Using instance variables should be avoided avoided whenever possible.  
Use properties instead.

Instance variables are not allowed in the public interface.  
Use a private class extension in the implementation instead.

Except when using headerdoc comments, the name of the instance variables should be aligned, as mentioned in the alignment topic of the C style guide:

```Objective-C
@interface Foo()
{
    NSUInteger     _x;
    NSArray      * _array;
    NSDictionary * _dict;
}
```

Not:

```Objective-C
@interface Foo()
{    
    NSUInteger _x;
    NSArray * _array;
    NSDictionary * _dict;
}
```

<a name="objc-9-4"></a>
#### 9.4. Properties

Properties variables should follow the lower camel-case rule.

Properties should always declare their full attributes:

```Objective-C
@property( nonatomic, readwrite, assign ) NSUInteger x;
```

Not:

```Objective-C
@property( assign ) NSUInteger x;
```

<a name="objc-9-5"></a>
#### 9.5. Properties atomicity

Properties should generally be declared as `atomic`, unless there's a specific reason not to do so.

An exception is made for `IBOutlet` properties, which should always be `nonatomic`.

<a name="objc-9-6"></a>
#### 9.6. Methods

Methods should follow the lower camel-case rule.  
The use of a leading underscore is strictly prohibited.

Empty parameter names are discouraged.

A trailing whitespace should be used after the `+` or `-` sign.  
The method's return type and argument's types should follow the same rule as casts, as mentioned in the C style guide.  
A trailing whitespace character should be used after the `:` sign, but not before:

```Objective-C
- ( void )methodWithObject1: ( id )object object2: ( id )object;
```

Not:

```Objective-C
-( void ) methodWithObject1 :( id ) object object2 :( id ) object;
```

Parameter names should be as explicit as possible.

The use of a `the` or `a` prefix for a parameter name is strictly prohibited.

```Objective-C
( id )object
```

Not:

```Objective-C
( id )anObject
```

<a name="objc-9-7"></a>
#### 9.7. Imports and forward declarations

The number of included files contained in the headers should be limited.  
Always use forward declarations when possible:

```Objective-C
@class Foo;

@interface Bar

- ( id )initWithFoo: ( Foo * )foo;

@end
```

Not:

```Objective-C
#import "Foo.h"

@interface Bar

- ( id )initWithFoo: ( Foo * )foo;

@end
```

<a name="objc-9-8"></a>
#### 9.8. Private methods

Private methods should be declared and defined in a class extension, in the main implementation.  
Declaration may be avoided, but is usually preferred:

```Objective-C
#import "Foo.h"

@interface Foo()

- ( void )bar;

@end

@implementation Foo()

- ( void )bar
{}

@end
```

<a name="objc-9-9"></a>
#### 9.9. Categories

Each category should have its own header and source file.  

Declaration should be as follow, with a single whitespace character around the category name, and no leading whitespace before the `(` sign:

```Objective-C
@interface Foo( CategoryName )
```

Not:

```Objective-C
@interface Foo (CategoryName)
```

<a name="objc-9-10"></a>
#### 9.10. Protocols
 
If the protocol conformance is not intended to be public, the main interface file should not declare it.

For instance, a `Foo` class implementing `NSTableViewDelegate` (for internal use).

`Foo.h`:

```Objective-C
@interface Foo: NSObject

@end
```

`Foo.m`:

```Objective-C
#import "Foo.h"

@interface Foo() < NSTableViewDelegate >

@end
```

<a name="objc-10"></a>
### 10. Singletons/Shared instances

Singletons or shared instances should always be created with the `dispatch_once` pattern.  
For pure singletons, `allocWithZone:` should be overriden to return the shared instance:

```Objective-C
+ ( instancetype )sharedInstance
{
    static dispatch_once_t once;
    static id              instance = nil;
    
    dispatch_once
    (
        &once,
        ^( void )
        {
            instance = [ [ super allocWithZone: nil ] init ];
        }
    );
    
    return instance;
}

+ ( id )allocWithZone: ( NSZone * )zone
{
    ( void )zone;
    
    return [ self sharedInstance ];
}
```

<a name="objc-11"></a>
### 11. NSLog

`NSLog` should be used carefully.  
It's recommended to use a macro to disable logging for release builds.

<a name="objc-12"></a>
### 12. Multithreading

The use of `libdispatch` should always be preferred to standard `NSThread` approach, unless there's a specific reason to use `NSThread`, like ensuring the thread is detached immediately.

<a name="objc-13"></a>
### 13. Compilation

GCC should never be used to compile Objective-C. Use Clang/LLVM instead.

<a name="asm"></a>
x86 Assembly Style Guide
------------------------

  1. [Syntax](#asm-1)
     1. [Direction of Operands](#asm-1-1)
     2. [Prefixes](#asm-1-2)
     3. [Suffixes](#asm-1-3)
     4. [Memory operands](#asm-1-4)
  2. [Local labels](#asm-2)
  3. [Indentation](#asm-3)
  4. [Alignment](#asm-4)
  5. [Whitespace](#asm-5)
  6. [Comments](#asm-6)
  7. [Grouping](#asm-7)
  8. [Procedures comments](#asm-8)
  9. [Optimisation](#asm-9)
     1. [Zeroing](#asm-9-1)
     2. [Comparing with zero](#asm-9-2)
     3. [Incrementing and decrementing](#asm-9-3)
     4. [Branching](#asm-9-4)
     5. [Loops unrolling](#asm-9-5)

<a name="asm-1"></a>
### 1. Syntax

The Intel syntax should always be preferred, when possible, to the AT&T syntax, for clarity.  
An exception is made for inline assembly, when compiling C code with Clang or GCC.

The basic differences are the following:

<a name="asm-1-1"></a>
#### 1.1. Direction of Operands

The direction of the operands in the Intel syntax is the opposite of AT&T syntax.  
In the Intel syntax, the destination operand comes first, followed by the source operand:

```NASM
    instr dest, src  ; Intel
```
```GAS
    instr src,  dest # AT&T
```

<a name="asm-1-2"></a>
#### 1.2. Prefixes

The Intel syntax doesn't use prefixes for register names or immediate operands, while the AT&T syntax uses the `%` prefix for registers and `$` for immediate operands:

```NASM
    mov  rax, 1    ; Intel
```
```GAS
    movq $1,  %rax # AT&T
```

<a name="asm-1-3"></a>
#### 1.3. Suffixes

The Intel syntax doesn't use suffixes for mnemonics, while the AT&T syntax uses `b`, `w`, `l` and `q`.  
The size of the operands is automatically assumed when using registers.  
For memory operands, similar directives can be used (`BYTE`, `WORD`, `DWORD`, `QWORD`):

```NASM
    ; Intel
	mov  rax, 1
	mov  eax, 1
```
```GAS
    # AT&T
	movq $1, %rax
	movl $1, %eax
```

<a name="asm-1-4"></a>
#### 1.4. Memory operands

The Intel syntax uses `[]` for memory operands, while the AT&T syntax uses `()`:
```NASM
    mov  rax, [ rdi + 8 ] ; Intel
```
```GAS
    movq 8( %rdi ), %rax  # AT&T
```

The index, scale, displacement and segment also use a different notation:

```NASM
mov  rax, segment:[ base + index * scale + displacement ] ; Intel
```
```GAS
movq %segment:displacement( base, index, scale ), %rax    # AT&T
```
    
<a name="asm-2"></a>
### 2. Local labels

Local labels inside a procedure should always start with a dot.  
For instance:

```NASM
procedure:
    
    .label1:
        
        ; ...
        
    .label2:
        
        ; ...
        
    ret
```

Label names should be meaningful.  
Don't use compiler style label names, like `L1:`.

<a name="asm-3"></a>
### 3. Indentation

Code should always be indented using four spaces.  Never use tabulations for indentation.

<a name="asm-4"></a>
### 4. Alignment

Mnemonics and operands should be aligned, in order to improve the code's readability, and a decent amount of spaces should be placed between the mnemonics and the operands:

```NASM
xor      rax,       rax
mov      al,        1
pxor     xmm0,      xmm0
movdqa   xmm1,      [ rsi ]
movdqa   [ rdi ],   xmm1
```

Not this:

```NASM
xor rax, rax
mov al, 1
pxor xmm0, xmm0
movdqa xmm1, [rsi]
movdqa [rdi], xmm1
```

<a name="asm-5"></a>
### 5. Whitespace

When using memory operands, inserts a white space between the brackets:

```NASM
mov rax, [ rdi ]
```

Not:

```NASM
mov rax, [rdi]
```

Also inserts a a whitespace around arithmetic operators:

```NASM
mov rax, [ rdi + 8 ]
```

Not:

```NASM
mov rax, [rdi+8]
```

<a name="asm-6"></a>
### 6. Comments

Comments should be placed on a new line and should not exceed 80 columns in width:

```NASM
; This is a comment
; with another line...
xor rax, rax
```

Not:

```NASM
xor rax, rax ; This is a comment
```

Comments should be as meaningful as possible.  
Don't simply describe what you are doing, but also why you are doing it.

<a name="asm-7"></a>
### 7. Grouping

Instructions should be grouped in a logical manner, with a newline between groups:

```NASM
; Comment for instruction group 1
xor     rax,     rax
xor     rcx,     rcx
mov     al,      2
mov     cl,      8
mul     rcx

; Comment for instruction group 2
pxor     xmm0,   xmm0
movdqa   xmm1,   [ rdi ]
```

<a name="asm-8"></a>
### 8. Procedures comments

All procedures should start with a standard comment, describing the procedure, the input and return registers, as well as killed registers, if any:

```NASM
;-------------------------------------------------------------------------------
; Short description of the procedure (single line)
; 
; Long description of the procedure
; (can be multi-line)
; 
; Input registers:
;       
;       - RDI:      Parameter description
;       - RSI:      Parameter description
; 
; Return registers:
;       
;       - RAX:      Return value description
; 
; Killed registers:
;       
;       - RCX
;       - RDX
;------------------------------------------------------------------------------- 
```

When no register is used as input or as return, or when no register is killed:

```NASM
;-------------------------------------------------------------------------------
; Short description of the procedure (single line)
; 
; Long description of the procedure
; (can be multi-line)
;
; Input registers:
;       
;       None
; 
; Return registers:
;       
;       None
; 
; Killed registers:
;       
;       None
;------------------------------------------------------------------------------- 
```

<a name="asm-9"></a>
### 9. Optimisation

The following is not mandatory, but it's strongly advised to follow these recommendations, when writing performance-critical code.

<a name="asm-9-1"></a>
#### 9.1. Zeroing

Always use `xor` to zero a register, instead of `mov`:

```NASM
xor rax, rax
```
    
Not:

```NASM
mov rax, 0
```

<a name="asm-9-2"></a>
#### 9.2. Comparing with zero

Always use `test` when comparing with zero, instead of `cmp`:

```NASM
test rax, rax
jz   .label
```
 
Not:

```NASM
cmp  rax, 0
je   .label
```

<a name="asm-9-3"></a>
#### 9.3. Incrementing and decrementing

Always use `add` and `sub` when incrementing or decrementing a register, instead of `inc` or `dec`:

```NASM
add rax, 1
sub rbx, 1
```  

Not:

```NASM
inc rax
dec rbx
```
While `inc` and `dec` are shorter, some processors have performance issues with those mnemonics.

<a name="asm-9-4"></a>
#### 9.4. Branching

When using conditional jumps, the following rules should be observed in order to increase the overall performances (due to the CPUs branch prediction algorithm).

##### Predict forward conditional branches to be not taken:

```NASM
test rax, rax
jz   .label

; Fallthrough - Most likely

.label:
    
    ; Forward branch - Most unlikely
```

##### Predict backward conditional branches to be taken:

```NASM
.label:
    
    ; Backward branch - Most likely
    
    test rax, rax
    jz   .label
    
; Fallthrough - Most unlikely
```

And of course, eliminate branches whenever possible.

<a name="asm-9-5"></a>
#### 9.5. Loops unrolling

Whenever possible, unroll loops:

```NASM
.loop:
    
    mov [ rdi      ], [ rsi      ]
    mov [ rdi +  8 ], [ rsi +  8 ]
    mov [ rdi + 16 ], [ rsi + 16 ]
    mov [ rdi + 24 ], [ rsi + 24 ]
    
    add  rdi,         32
    add  rsi,         32
    sub  rcx,         32
    
    test rcx,         rcx
    jnz .loop
```

Instead of:

```NASM
.loop:
    
    mov [ rdi ],      [ rsi ]
    
    add  rdi,         8
    add  rsi,         8
    sub  rcx,         8
        
    test rcx,         rcx
    jnz .loop
```

Repository Infos
----------------

    Owner:          Jean-David Gadina - XS-Labs
    Web:            www.xs-labs.com
    Blog:           www.noxeos.com
    Twitter:        @macmade
    GitHub:         github.com/macmade
    LinkedIn:       ch.linkedin.com/in/macmade/
    StackOverflow:  stackoverflow.com/users/182676/macmade
