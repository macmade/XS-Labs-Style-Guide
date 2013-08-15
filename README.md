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
Code is about rythm, and readability. And I think taking time to carefully align operators, declarations, etc. improves the overall readability and the feeling you can get while reading code.

License
-------

This style guide is published under the terms of the [FreeBSD documentation license](http://www.freebsd.org/copyright/freebsd-doc-license.html).

C Style Guide
-------------

### x. Indentation

Code should always be indented using four spaces.  Never use tabulations for indentation.

### x. Braces

Braces should always be placed on an empty line.  
This apply for all constructs (functions, conditions, loops, etc.):

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

### x. Alignment

#### x.1 Assignments

Always align assignments:

```C
x      = 1;
foo    = 2;
foobar = 2;
```

Not:

```C
x = 1;
foo = 2;
foobar = 2;
```

If using multiple lines in an assigment, aligns the extra lines to the equal sign:

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

#### x.1. Variable declarations

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

#### x.2. Single line conditionals

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

#### x.3. Array subscripting operator

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

### Pointers

The pointer sign should alway have a leading and trailing space:

```C
int * x;
```

Not:

```C
int* x;
int *x;
```

When aligning, place the pointer sign next to the variable name:

```C
int           * x;
unsigned long * y;
```

### x. Macros

Macros should always be in uppercase.

```C
#define FOO         1
```

If a macro takes parameters, the parameters names should begin and end with a single underscore:

```C
#define BAR( _x_ )  ( ( _x_ ) + 1 )
```

As in the above example, parenthesis should always be used around a macro parameter.

### x. Static symbols

Static symbols should always start with two underscores, and have a value:

```C
static int __x = 0;
```

Not:

```C
static int x;
```

This also applies to static functions.

### x. Header guards

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

### x. Functions with no parameters

Functions without parameters should always be declared as taking `void`:

```C
void foo( void );
```

Not:

```C
void foo();
```

C++ Style Guide
---------------

... [ in progress ] ...

Objective-C Style Guide
-----------------------

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
