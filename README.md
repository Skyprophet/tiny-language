# Design Point

- a tiny, mostly-static, very easy-to-compile imperative language
intended for high-performance integer computations

- safe: any unsafe action such as out-of-bounds array access leads to
program termination with a diagnostic

- newlines are significant, but indentation is not; a logical line of
code can be broken across physical lines using a backslash, which must
immediately precede a newline, and which is treated as whitespace by
the lexer

- there are no libraries, separate compilation, linking, etc.

# Syntax

```
program :=
     function+

function :=
     type ident(arg1 [, arg2 ...]) {
       stmt*
     }

type :=
  bool
  int
  array
  void

stmt :=
     { \n stmt }\n
     type name [, name ...]
     array name\[expr\] [, name\[expr\] ...]
     print((string|expr)*)
     if (expr) {\n stmt* }\n [else {\n stmt }]
     while (expr) {\n stmt* }
     for (ident : expr) {\n stmt* }
     ident := expr
     ident\[expr\] := expr
     expr
     ;.*
     return expr

expr :=
     true
     false
     -?[0-9]+
     ident
     (expr ? expr : expr)
     sizeof(ident)
     input()
     ident\[expr\]
     ident([expr, ...])
     (expr binop expr)
     (unaryop expr)

binop :=
     + - * ^ / % & | == > >= < <=
    (caret is exponentiation, we have no xor operator)

unaryop :=
    - !
    (bang is Boolean not)

ident :=
     [a-zA-Z_][a-zA-Z0-9_]*

```

# More

- there are no implicit conversions among types
- the int type is a 64-bit, two's complement integer
- an array is always a 1-D array of int
- arrays are sized (and bounds checked) but the size is not part of the type
- the void type is not allowed in variable definitions or function parameter lists
- identifiers cannot be keywords
- every program must contain exactly one function called "main"
- recursion is allowed
- arrays cannot be assigned
- arrays are passed to functions by reference
- when the program first passes an array definition, an array of the
  specified size is allocated and initialized to all zero
- arrays are deallocated at the end of their block
- arrays must not escape their block
- names are visible using block scope
- there are no global variables
- variable shadowing is a compile-time error

# THE FUTURE

version 2 of this language will have bignum as the default (and only!)
integer type
