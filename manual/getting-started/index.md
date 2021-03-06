---
layout: manual
title:  Getting Started
---

The latest version of Julia can be downloaded and installed by following the instructions on the [main GitHub page](https://github.com/JuliaLang/julia#readme).
The easiest way to learn and experiment with Julia is by starting an interactive session (also known as a read-eval-print loop or "repl"):

    $ julia
                   _
       _       _ _(_)_     |
      (_)     | (_) (_)    |  A fresh approach to technical computing.
       _ _   _| |_  __ _   |
      | | | | | | |/ _` |  |  Version 0 (pre-release)
      | | |_| | | | (_| |  |  Commit 61847c5aa7 (2011-08-20 06:11:31)*
     _/ |\__'_|_|_|\__'_|  |
    |__/                   |

    julia> 1 + 2
    3

    julia> ans
    3

    julia> load("file.j")

To exit the interactive session, type `^D` — the control key together with the `d` key.
When run in interactive mode, `julia` displays a banner and prompts the user for input.
Once the user has entered a complete expression, such as `1 + 2`, and hits enter, the interactive session evaluates the expression and shows its value.
If an expression is entered into an interactive session with a trailing semicolon, its value is not shown.
The variable `ans` is bound to the value of the last evaluated expression whether it is shown or not.
The `load` function reads and evaluates the contents of the given file.

To run code in a file non-interactively, you can give it as the first argument to the julia command:

    $ julia script.j arg1 arg2...

As the example implies, the following command-line arguments to julia are taken as command-line arguments to the program `script.j`.
There are various ways to run Julia code and provide options, reminiscent of those taken by the `perl` and `ruby` programs:

    julia [options] [program] [args...]
     -q --quiet               Quiet startup without banner
     -H --home=<dir>          Load files relative to <dir>
     -T --tab=<size>          Set REPL tab width to <size>

     -e --eval=<expr>         Evaluate <expr> and don't print
     -E --print=<expr>        Evaluate and print <expr>
     -P --post-boot=<expr>    Evaluate <expr> right after boot
     -L --load=file           Load <file> right after boot
     -b --bare                Bare: don't load default startup files
     -J --sysimage=file       Start up with the given system image file

     -p n                     Run n local processes

     -h --help                Print this message

## Example Code

At this point it is useful to take a look at some [Example Programs](../example-programs).

## Major Differences From MATLAB®

Julia's syntax is intended to be familiar to users of MATLAB®.
However, Julia is in no way a MATLAB® clone:
there are major syntactic and functional differences.
The following are the most significant differences that may trip up Julia users accustomed to MATLAB®:

- Arrays are indexed with square brackets, `A[i,j]`.
- Multiple values are returned and assigned with parentheses, `return (a, b)` and `(a, b) = f(x)`.
- Values are passed and assigned by reference. If a function modifies an array, the changes will be visible in the caller.
- Use n for nx1: The number of arguments to an array constructor equals the number of dimensions of the result.
In particular, `rand(n)` makes a 1-dimensional array.
- Concatenating scalars and arrays with the syntax `[x,y,z]` concatenates in the first dimension ("vertically").
For the second dimension ("horizontally"), use spaces as in `[x y z]`.
To construct block matrices (concatenating in the first two dimensions), the syntax `[a b; c d]` is used to avoid confusion.
- Colons `a:b` and `a:b:c` construct `Range` objects.
To construct a full vector, use `linspace`, or "concatenate" the range by enclosing it in brackets, `[a:b]`.
- Functions return values using the `return` keyword, instead of by listing their names in the function definition (see [The "return" Keyword](../functions#The+return+Keyword) for details).
- A file may contain any number of functions, and all definitions will be externally visible when the file is loaded.
- Reductions such as `sum`, `prod`, and `max` are performed over every element of an array when called with a single argument as in `sum(A)`.
- Functions such as `sort` that operate column-wise by default (`sort(A)` is equivalent to `sort(A,1)`) do not have special behavior for 1xN arrays; the argument is returned unmodified since it still performs `sort(A,1)`. To sort a 1xN matrix like a vector, use `sort(A,2)`.
- Parentheses must be used to call a function with zero arguments, as in `tic()` and `toc()`.
- Do not use commas to end statements. The results of statements are not automatically printed (except at the interactive prompt), and lines of code do not need to end with semicolons. The function `println` can be used to print a value followed by a newline.
