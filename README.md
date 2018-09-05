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
     type name(arg1 [, arg2 ...]) {
       stmt*
     }

stmt :=
     { \n stmt }\n
     type name [, name ...]
     array name\[expr\] [, name\[expr\] ...]
     ...
     print((string|expr)*)

expr :=
     ...
     sizeof(id)
     input()
```

# Types

- bool
- int (64-bit 2's complement)
- array (of int, arrays are sized but the size is not part of the type)
- void

# More Requirements

- every program must contain exactly one function called "main"
