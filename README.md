# Design Point

- a tiny, very easy-to-compile imperative language intended for
high-performance integer computations

- safe: any unsafe action such as out-of-bounds array access leads to
program termination with a diagnostic

- newlines are significant, but indentation is not; a logical line of
code can be broken across physical lines using a backslash, which must
immediately precede a newline, and which is treated as whitespace by
the lexer

- there are no libraries, separate compilation, linking, etc.

# Syntax

program :=
     function+

function :=
     type name(arg1 [, arg2 ...]) {
       stmt
     }

stmt :=
     type name
     array name[expr]
     ...
     print((string|expr)*)

expr :=
     ...
     sizeof(id)

type name(type name, ...) {
     stmt
}

type name

int main() {
}

# Types

bool
int (64-bit 2's complement)
array (array of int)
void

array semantics:
  arrays are sized, but this isn't part of the type
  OOB access kills the program

global namespace:

