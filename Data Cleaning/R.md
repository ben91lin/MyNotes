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

The atomic vector element has same type.\
Using `c()` or `vector()` to create the vector.

* `length()` - count the vector length.
* `seq()` - create the number sequence vector.
* `names()` - give vector element a name.
* `which()` - return vactor element bi logical expression.

Get value by boolean vector.
```R
    x <- c(0, -1, -2, NA, 4, 6)
    y <- x[(!is.na(x)) & x > 0]
    y # c(4, 6)
```
Get repeat value by index vector.
(Attention!! `1:4` in R contain the last value.)
```R
    x <- 1:4
    y <- x[ c(1, 2, 3, 1, 2, 4) ]
    y # c(1, 2, 3, 1, 2, 4)
```
Get value by negative index vector.
(Attention!! the negative index vactor will 
exclude elements.)
```R
    x <- 1:6
    y <- x[-(1:5)]
    y # c(1)
```
Get value by names.
```R
    cars <- c(5, 10)
    names(cars) <- c("benz", "toyota")
    cars <- fruit["toyota"]
    cars # c(10)
```
Assign value.
```R
    x <- c(NA, NA, 3)
    x[is.na(x)] <- 0
    x # c(0, 0, 3)
```

### Array & Matrix

Array - multiple dimension vectors.

Create Array.
```R
    x <- c(1, 2, 3)
    y <- c(4, 5, 6)
    rbind(x, y)
      [,1] [,2] [,3]
    x    1    2    3
    y    4    5    6
    cbind(x, y)
         x y
    [1,] 1 4
    [2,] 2 5
    [3,] 3 6
```
Get value.
```R
    x <- array(c(1, 2, 3), c(2,3))
    x
        [,1] [,2] [,3]
    [1,]  1    3    2
    [2,]  2    1    3
    x[1,]
        [,1] [,2] [,3]
    [1,]  1    3    2
    x[1, 1:2]
        [,1] [,2]
    [1,]  1    3
```

* `dim()`
* `ncol()`
* `nrow()`
* `aperm()` - transpose matrix.

Matrix - 2D dimension vectors.

Create matrix.
```R
    matrix(c(1:4), nrow = 2, ncol = 2, byrow = TRUE)
        [,1] [,2]
    [1,]  1    2
    [2,]  3    4
```

* `t()` - transpose matrix.
* `%*%` - matrix multiplication.
* `diag()`
* `det()`
* `solve()`
* `eigen()`
* `colnames()`
* `dimnames()`
* `rownames()`

### Lists

Linked list in C.

```R
    x <- list(a = 1, b = TRUE, c = "test", d = c(1, 2, 3))
    x[1]
    # $a
    # [1] 1
    x[[1]]
    # [1] 1
    x$b # Get data by $name.
    # [1] TRUE
    x[[4]][1] 
    # [1] 1
```

* c() - combine list.

### Factor


### Dataframe


### Check missing value

* `is.na()`
* `is.nan()`
* `is.infinite()`

Attention!! `is.na(NaN)` and `is.na(NA)` will return TRUE.

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
* `format()`
* `formatC()`
* `ls()` - find the variable name in enviroment.
* `ls.str()` - find the variable name and structure in enviroment.
* `nchar()`
* `print()`
* `rm()` - remove variable.
* `sprintf()`
* `substr()`
* `sum()`
* `summary()`
* `str()` - check variable data structure.
* `strsplit()`
* `toString()`
* `toupper()`
* `tolower()`

## Refference

https://joe11051105.gitbooks.io/r_basic/content/

https://blog.gtwang.org/programming/r/#google_vignette