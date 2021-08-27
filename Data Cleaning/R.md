# R

## Basic

* annotation: `#`
* multiple code on one line: `;`
* find help: `?sum`, `??"sum"`, `help(sum)`
* documentation: `browseVignettes()`, `vignette("Sweave", package = "utils")`

## Type

Everything in R is an object.

### Basic

* numeric(real or float(double))
* integer: 2L(the L tells R to store this as an integer)
* complex
* logical(boolean)
* raw(binary data)
* character

### Vectors

* atomic vectors

    The vector elements have the same type.\
    Using `c()` or `vector()` to create the vector.\
    R support missing value "NA", use `is.na()` to check it.\
    There are other value was supported, like infinity "inf" and not a number "NaN", use `is.infinite()` and `is.nan()` to check it.\
    Attention!! `is.na(NaN)` and `is.na(NA)` will return TRUE.

* lists

### Check type

* `typeof()`
* `class()`
* `is.type_name()` - use `ls(pattern = "^is", baseenv())` to find all method.

### Casting

* `as.type_name()` - use `ls(pattern = "^as", baseenv())` to find all method

## Operator

Operator | Name |
--|--|
<-, <<-, = | Leftwards assignment |
->, ->> | Rightwards assignment |
\+ | Addition |
– | Subtraction |
\* | Multiplication |
/ | Division |
^ | Exponent |
%% | Modulus (Remainder from division) |
%/% | Division |
< | Less than |
\> | Greater than |
<= | Less than or equal to |
\>= | Greater than or equal to |
== | Equal to |
!= | Not equal to |
! | Logical NOT |
& | Element-wise logical AND |
&& | Logical AND |
\| | Element-wise logical OR |
\|\| | Logical OR |

https://www.datamentor.io/r-programming/operator/

## GUI

* `View()`
* `edit()`
* `fix()`

## Other built-in function

* `abs()`
* `attributes()`
* `length()`
* `ls()` - find the variable name in enviroment.
* `ls.str()` - find the variable name and structure in enviroment.
* `print()`
* `rm()` - remove variable.
* `sum()`
* `summary()`
* `str()` - check variable data structure.