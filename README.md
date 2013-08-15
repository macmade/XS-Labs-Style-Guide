XS-Labs Coding Style Guide for C, C++, Objective-C and x86 Assembly
===================================================================

Table Of Contents
-----------------

 1. About
 1. License
 1. C Style Guide
 1. C++ Style Guide
 1. Objective-C Style Guide
 1. x86 Assembly Style Guide

About
-----

These are the coding conventions used for all recent [XS-Labs](http://www.xs-labs.com/) projects.  
Feel free to comment, raise issues, fork and/or adapt this document.

### Note about whitespaces

XS-Labs' coding conventions make a heavy use of whitespaces.  
It's not a common habit among coders, who usually prefers compact code.

This is just a personal taste.  
After 15 years of professional development, I like to see a lot of spaces in my own code. It's like letting the code breath.   
Code is about rhythm, and readability. And I think taking time to carefully align operators, declarations, etc. improves the overall readability and the feeling you can get while reading code.

License
-------

This style guide is published under the terms of the [FreeBSD documentation license](http://www.freebsd.org/copyright/freebsd-doc-license.html).

C Style Guide
-------------

  1.  Indentation
  2.  Ending line
  3.  Comments
  4.  Maximum number of columns
  5.  Includes
  6.  Whitespace
      1. Operators
      2. Parenthesis and brackets
      3. Pointers
      4. Casts
      5. `for` loops
  7.  Braces
  8.  Alignment
      1. Assignments
      2. Variable declarations
      3. Single line conditionals
      4. Array subscripting operator
  9.  Case and symbols naming
  10. Variable declaration
  11. Macros
  12. Structs and unions
  13. Enums
  14. Typedefs
  15. New lines
  16. Header guards
  17. Functions prototypes
  18. Functions with no parameters
  19. Inline functions
  20. Dereferencing
  21. Conditionals
  22. Switch statements
  23. Long `if/else if` statements
  24. Inline documentation
  25. Compilation

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

### 2. Ending line

Source and header files should always end with a single empty line.

### 3. Comments

Comments should always use the `/* */` notations.  
Single line C++ style comments (`//`) are disallowed.

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

### 4. Maximum number of columns

The number of columns for a single line is not limited.  
However, try whenever possible to wrap long lines in order to improve the overall readability.

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

### 6. Whitespace

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

#### 6.4 Casts

No whitespace should be added after a cast. A single whitespace should be used after the opening parenthesis and before the closing one:

```C
x = ( char * )y;
```

Not:

```C
x = ( char * ) y;
```

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

### 8. Alignment

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

#### 8.3. Single line conditionals

If using single line conditional statements (see above), align the `if`/`else` statements, as well as the opening/closing braces and comparison operators:

```C
     if( x      == 1 ) { foobar = 1;          }
else if( foobar == 1 ) { x      = 0xFFFFFFFF; }
else				   { x      = 0;          }
```

Not:

```C
if( x == 1 ) { foobar = 1; }
else if( foobar == 1 ) { x = 0xFFFFFFFF; }
else { x = 0; }
```

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

### 9. Case and symbols naming

Local variables should never start with an underscore, and should always start with a lowercase letter.  
Lower camel-case is recommended.

For global symbols (variables and functions), upper camel-case is usually recommended.  
A single underscore may be used to denote private symbols, if they are not static.  
Underscores may be used to simulate namespaces.

```C
void SomePackage_SomePublicFunction( void );
void _SomePackage_SomePrivateFunction( void );

extern int SomeInteger;
```

Static symbols should always start with two underscores, and have a value:

```C
static int __x = 0;
```

Not:

```C
static int x;
```

This also applies to static functions.

### 10. Variable declaration

Local variables should be declared without a value, and before any other statement:

```C
void foo( void )
{
    int x;
    int y;
    
    x = 0;
    x = 1;
    
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

The same applies for `for` loops:

```C
int i;

for( i = 0; i < 10; i++ )
{
    /* ... */
}
```

Not:

```C
for( int i = 0; i < 10; i++ )
{
    /* ... */
}
```

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

### 12. Structs and unions

Members of structs and unions should be properly aligned, as mentioned before:

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

When manually padding a struct, use two leading underscore for the member name, and a trailing number, prefaced with an underscore.  
Always use a `char` array to manually pad a structure:

```C
struct foo
{
	char s;
	char __pad_0[ 3 ];
	int  x;
};
```

### 13. Enums

Enum values should be properly aligned, as mentioned before.  
A value should always be provided. Hexadecimal is usually preferred:

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

### 14. Typedefs

Simple typedefs are declared on a single line:

```C
typedef int foo;
```

With structs, unions and enums place the type name on a new line:

```C
typedef struct
{
    int x;
    int y;
}
foo;
```

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

### 16. Header guards

All headers should be properly guarded:

```C
#ifndef __FOO_H__
#define __FOO_H__

/* ... */

#endif
```

The name of the macro used as header guard should always be in uppercase, start and end with two underscores.  
It should consist of the name of the header file (optionally with directories prefixes, separated by a single underscore), and a trailing `_H`.

For instance, for `include/foo/bar/foobar.h`, this should be `__FOO_BAR_FOOBAR_H__`.

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

### 18. Functions with no parameters

Functions without parameters should always be declared as taking `void`:

```C
void foo( void );
```

Not:

```C
void foo();
```

### 19. Inline functions

Inline functions should generally avoided, unless there's a very good and specific reason to make them inline.

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

Always prefer testing with `==`, even with boolean values:

```C
if( b == true )
{
    /* ... */
}
```

Not:

```C
if( b )
{
    /* ... */
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

### 24. Inline documentation

Documented code should prefer [Apple's HeaderDoc](https://developer.apple.com/library/mac/documentation/DeveloperTools/Conceptual/HeaderDoc/intro/intro.html) syntax rather than JavaDoc.

### 25. Compilation

Always compiles your code with `-Werror` or similar, and always use the highest possible error reporting level.

When function parameters are not used, cast them to `void` to prevent a warning:

```C
void foo( int unused )
{
    ( void )unused;
}
```

C++ Style Guide
---------------

**All rules from the C Style Guide applies here, with a few exceptions and additions described hereafter.**

  1. Comments
  2. Namespaces
  3. Classes
     1. Naming
     2. Inheritance
     3. Members
     4. Method definitions
  4. Templates

### 1. Comments

Single line C++ comments are allowed, even if the `/*  */` notation is usually preferred.

### 2. Namespaces

Namespaces should always use the upper camel-case rule.

### 3. Classes

#### 3.1. Naming

C++ classes should always use the upper camel-case rule.  
Methods should always use the lower camel-case rule, as well as properties.

Private members should always have a leading underscore.

#### 3.2. Inheritance

The `:` sign should immediately follow the class name and should be followed by a single whitespace character.  
When inheriting from multiple classes, a single whitespace character should be used after the comma:

```C++
class FooBar: Foo, Bar
{
	
};
```

#### 2.3. Members

Public members should be declared first, followed by protected and private members.  
Always group members with the same visibility (properties and methods).  

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

#### 3.4. Method definitions

Except for templates, method should never be defined in the header files.

### 4. Templates

Template parameters should be surrounded by a single whitespace character.  
A single whitespace character should be used after the comma.  
The `<` sign should immediately follow the class name:

```C++
template class Foo< int x, int y >
{
    
};
```

### 5. Using

The `using` keyword is usually discouraged, except for very long namespaces.  
It's strictly prohibited for the `std` namespace - the full notation should always be used.

```C++
std::vector< int > v;
```

Not:

```C++
using std;

vector< int > v;
```

### 6. [ xxx ]

... [ in progress ] ...

Objective-C Style Guide
-----------------------

**All rules from the C Style Guide applies here, with a few exceptions and additions described hereafter.**

... [ in progress ] ...

x86 Assembly Style Guide
------------------------

  1. Syntax
     1. Direction of Operands
     2. Prefixes
     2. Suffixes
     2. Memory operands
  2. Local labels
  3. Indentation
  4. Alignment
  5. Whitespace
  6. Comments
  7. Grouping
  8. Procedures comments
  9. Optimisation
     1. Zeroing
     2. Comparing with zero
     3. Incrementing and decrementing
     4. Branching
     5. Loops unrolling

### 1. Syntax

The Intel syntax should always be preferred, when possible, to the AT&T syntax, for clarity.  
An exception is made for inline assembly, when compiling C code with Clang or GCC.

The basic differences are the following:

#### 1.1. Direction of Operands

The direction of the operands in the Intel syntax is the opposite of AT&T syntax.  
In the Intel syntax, the destination operand comes first, followed by the source operand:

```NASM
    instr dest, src  ; Intel
```
```GAS
    instr src,  dest # AT&T
```

#### 1.2. Prefixes

The Intel syntax doesn't use prefixes for register names or immediate operands, while the AT&T syntax uses the `%` prefix for registers and `$` for immediate operands:

```NASM
    mov  rax, 1    ; Intel
```
```GAS
    movq $1,  %rax # AT&T
```

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

### 3. Indentation

Code should always be indented using four spaces.  Never use tabulations for indentation.

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

### 9. Optimisation

The following is not mandatory, but it's strongly advised to follow these recommendations, when writing performance-critical code.

#### 9.1. Zeroing

Always use `xor` to zero a register, instead of `mov`:

```NASM
xor rax, rax
```
    
Not:

```NASM
mov rax, 0
```

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

#### 9.4. Branching

When using conditional jumps, the following rules should be observed in order to increase the overall performances (due to the CPUs branch prediction algorithm).

##### Predict forward conditional branches to be not taken

```NASM
test rax, rax
jz   .label

; Fallthrough - Most likely

.label:
    
    ; Forward branch - Most unlikely
```

##### Predict backward conditional branches to be taken

```NASM
.label:
    
    ; Backward branch - Most likely
    
    test rax, rax
    jz   .label
    
; Fallthrough - Most unlikely
```

And of course, eliminate branches whenever possible.

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

    Owner:			Jean-David Gadina - XS-Labs
    Web:			www.xs-labs.com
    Blog:			www.noxeos.com
    Twitter:		@macmade
    GitHub:			github.com/macmade
    LinkedIn:		ch.linkedin.com/in/macmade/
    StackOverflow:	stackoverflow.com/users/182676/macmade
