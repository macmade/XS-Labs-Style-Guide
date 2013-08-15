XS-Labs Coding Style Guide for C, C++, Objective-C and x86 Assembly
===================================================================

Table Of Contents
-----------------

 1. [About]()
 1. [License]()
 1. [C Style Guide]()
 1. [C++ Style Guide]()
 1. [Objective-C Style Guide]()
 1. [x86 Assembly Style Guide]()

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

... [ in progress ] ...

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

#### 1.1 Direction of Operands

The direction of the operands in the Intel syntax is the opposite of AT&T syntax.  
In the Intel syntax, the destination operand comes first, followed by the source operand:

    instr dest, src  | Intel
    instr src,  dest | AT&T

#### 1.2 Prefixes

The Intel syntax doesn't use prefixes for register names or immediate operands, while the AT&T syntax uses the `%` prefix for registers and `$` for immediate operands:

    mov  rax, 1    ; Intel
    movq $1,  %rax ; AT&T
    
#### 1.3 Suffixes

The Intel syntax doesn't use suffixes for mnemonics, while the AT&T syntax uses `b`, `w`, `l` and `q`.  
The size of the operands is automatically assumed when using registers.  
For memory operands, similar directives can be used (`BYTE`, `WORD`, `DWORD`, `QWORD`):

	mov  rax, 1   | Intel
	mov  eax, 1   | Intel
	movq $1, %rax | AT&T
	movl $1, %eax | AT&T
	
#### 1.4 Memory operands

The Intel syntax uses `[]` for memory operands, while the AT&T syntax uses `()`:

    mov  rax,       [ rdi + 8 ] | Intel
    movq 8( %rdi ), %rax        | AT&T
    
The index, scale, displacement and segment also use a different notation:

    mov  rax,                                         segment:[ base + index * scale + displacement ]
    movq %segment:displacement( base, index, scale ), %rax
    
### 2. Local labels

Local labels inside a procedure should always start with a dot.  
For instance:

    procedure:
        
        .label1:
            
            ; ...
            
        .label2:
            
            ; ...
            
        ret

Label names should be meaningful.  
Don't use compiler style label names, like `L1:`.

### 3. Indentation

Code should always be indented using four spaces.  Never use tabulations for indentation.

### 4. Alignment

Mnemonics and operands should be aligned, in order to improve the code's readability, and a decent amount of spaces should be placed between the mnemonics and the operands:

    xor      rax,       rax
    mov      al,        1
    pxor     xmm0,      xmm0
    movdqa   xmm1,      [ rsi ]
    movdqa   [ rdi ],   xmm1

Not this:

    xor rax, rax
    mov al, 1
    pxor xmm0, xmm0
    movdqa xmm1, [rsi]
    movdqa [rdi], xmm1

### 5. Whitespace

When using memory operands, inserts a white space between the brackets:

    mov rax, [ rdi ]
    
Not:

    mov rax, [rdi]
    
Also inserts a a whitespace around arithmetic operators:

    mov rax, [ rdi + 8 ]
    
Not:

    mov rax, [rdi+8]

### 6. Comments

Comments should be placed on a new line and should not exceed 80 columns in width:

    ; This is a comment
    ; with another line...
    xor rax, rax
    
Not:

    xor rax, rax ; This is a comment
    
Comments should be as meaningful as possible.  
Don't simply describe what you are doing, but also why you are doing it.

### 7. Grouping

Instructions should be grouped in a logical manner, with a newline between groups:
    
    ; Comment for instruction group 1
    xor     rax,     rax
    xor     rcx,     rcx
    mov     al,      2
    mov     cl,      8
    mul     rcx
    
    ; Comment for instruction group 2
    pxor     xmm0,   xmm0
    movdqa   xmm1,   [ rdi ]

### 8. Procedures comments

All procedures should start with a standard comment, describing the procedure, the input and return registers, as well as killed registers, if any:

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

When no register is used as input or as return, or when no register is killed:

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

### 9. Optimisation

The following is not mandatory, but it's strongly advised to follow these recommendations, when writing performance-critical code.

#### 9.1 Zeroing

Always use `xor` to zero a register, instead of `mov`:

    xor rax, rax
    
Not:

    mov rax, 0
    
#### 9.2 Comparing with zero

Always use `test` when comparing with zero, instead of `cmp`:

    test rax, rax
    jz   .label
    
Not:

    cmp  rax, 0
    je   .label

#### 9.3 Incrementing and decrementing

Always use `add` and `sub` when incrementing or decrementing a register, instead of `inc` or `dec`:

    add rax, 1
    sub rbx, 1
    
Not:

    inc rax
    dec rbx
    
While `inc` and `dec` are shorter, some processors have performance issues with those mnemonics.

#### 9.4 Branching

When using conditional jumps, the following rules should be observed in order to increase the overall performances (due to the CPUs branch prediction algorithm).

##### Predict forward conditional branches to be not taken

    test rax, rax
    jz   .label
    
    ; Fallthrough - Most likely
    
    .label:
        
        ; Forward branch - Most unlikely


##### Predict backward conditional branches to be taken

    .label:
        
        ; Backward branch - Most likely
        
    test rax, rax
    jz   .label
    
    ; Fallthrough - Most unlikely

And of course, eliminate branches whenever possible.

#### 9.5 Loops unrolling

Whenever possible, unroll loops:

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

Instead of:

    .loop:
        
        mov [ rdi ],      [ rsi ]
        
        add  rdi,         8
        add  rsi,         8
        sub  rcx,         8
        
        test rcx,         rcx
        jnz .loop

Repository Infos
----------------

    Owner:			Jean-David Gadina - XS-Labs
    Web:			www.xs-labs.com
    Blog:			www.noxeos.com
    Twitter:		@macmade
    GitHub:			github.com/macmade
    LinkedIn:		ch.linkedin.com/in/macmade/
    StackOverflow:	stackoverflow.com/users/182676/macmade
