R nuts and bolts: Data Types
========================================================
author:
date:
autosize: true

Atomic Classes
========================================================

R has five basic or "atomic" classes (aka atomin modes):

-   __character__ (Strings)
    - Ex. "Survived"

-   __numeric__ (default to floating point numbers)
    - Ex. 3.14

-   __integer__
    - Ex. 3

-   __complex__
    - Ex. 1 + 1i

-   __logical__
    - Ex. TRUE/FALSE


Numbers
========================================================

-   Numbers in R a generally treated as numeric objects (i.e. double
    precision real numbers)

    -   If you explicitly want an integer, you need to specify the ```L```
    suffix

    -   Ex: Entering ```1``` gives you a numeric object; entering ```1L```
    explicitly gives you an integer.

-   There is also a special number ```Inf``` which represents infinity;
    e.g. ```1 / 0```; ```Inf``` can be used in ordinary calculations;
    e.g. ```1 / Inf``` is 0

-   The value ```NaN``` represents an undefined value ("not a number");
    e.g. 0 / 0; ```NaN``` can also be thought of as a missing value
    (more on that later)


R Objects
========================================================

- Vector,
- List,
- Factor,
- Matrix,
- Data frame, ..

Vector: the R workhorse
========================================================

__The most basic object is a vector.__

- __Scalar__s do not really exist, actually a scalar is a vector fo 1 eleement.
-   A vector can __only contain objects of the same class__, in other words, elements of a vector all have the same class.
- The __size of a vector__ is __determined at its creation__, so if you wish to add or delete elements, you’ll need to reassign the vector.


---

```r
# Scalar -> vector of 1 element
> x <- 8
> x
 [1] 8
```

```r
# Size of a vector
> x <- c(88,5,12,13)
# Insert 168 before the 13
> x <- c(x[1:3],168,x[4])
> x
[1]  88   5  12 168  13
```

Vector: Creating vectors
========================================================

Using the `vector()` function to create an empty vector

```r
> x <- vector("numeric", length = 10)
> x
 [1] 0 0 0 0 0 0 0 0 0 0
```

---

The `c()` function can be used to create vectors of objects.

```r
> x <- c(0.5, 0.6)       ## numeric
> x <- c(TRUE, FALSE)    ## logical
> x <- c(T, F)           ## logical
> x <- c("a", "b", "c")  ## character
> x <- c(1L, 2L)         ## integer
> x <- 9:29              ## integer
> x <- c(1+0i, 2+4i)     ## complex
```

Vector: Length of a vector
========================================================

The `length()` function can be used to obtain the length of a vector.


```r
> x <- c(1,2,4)
> length(x)
[1] 3
```

```r
# Be careful using length!
> x <- c()
> x
NULL
> length(x)
[1] 0
> 1:length(x)
[1] 1 0
```


Vector: Mixing Objects & Implicit Coercion
========================================================

A vector contains objects of the same class. What about the following?

```r
# Mixing different class within the same vecto.r
> y <- c(1.7, "a")   ## coerced to character
> y <- c(TRUE, 2)    ## coerced to numeric
> y <- c("a", TRUE)  ## coerced to character
```

When different objects are mixed in a vector, _automatic coercion_ occurs so that every element in the vector is of the same class.

Vector: Explicit Coercion
========================================================

Objects can be explicitly coerced from one class to another using the `as.*` functions, if available.

```r
> x <- 0:6
> class(x)
[1] "integer"

> as.numeric(x)
[1] 0 1 2 3 4 5 6

> as.logical(x)
[1] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE

> as.character(x)
[1] "0" "1" "2" "3" "4" "5" "6"
```
---

Nonsensical coercion results in `NA`s.

```r
> x <- c("a", "b", "c")
> as.numeric(x)
[1] NA NA NA
Warning message:
NAs introduced by coercion
```

Vector: Recycling
========================================================

When applying an operation to two vectors that requires them to be the same length, R automatically __recycles__, or repeats, the shorter one, until it is long enough to match the longer one. A warning could be generated.

```r
# longer object length multiple of shorter object length
> c(1,2,3) + c(1,2,3,4,5,6)
[1] 2 4 6 5 7 9
```


```r
# longer object length not multiple of shorter object length
> c(1,2,3) + c(1,2,3,4,5,6,7)
[1] 2 4 6 5 7 9 8
Warning message:
In c(1, 2, 3) + c(1, 2, 3, 4, 5, 6, 7) :
  longer object length is not a multiple of shorter object length
```

List
========================================================

Lists are a special type of vector that can contain elements of different classes.

```r
> x <- list(1, "a", TRUE, 1 + 4i)
> x
[[1]]
[1] 1

[[2]]
[1] "a"

[[3]]
[1] TRUE

[[4]]
[1] 1+4i
```

Lists are quite important in R, eg. objects (OO) are list with attributes.

Hands-On (15 minutes)
========================================================


```r
library(swirl)
swirl()
#.....
# Select the "R Programming" entry
# Select the "Vectors" entry [4]

# Enjoy :)
```

Factors
========================================================

**Factors are used to represent categorical data.**

Factors can be unordered or ordered. One can think of a factor as an integer vector where each integer has a _label_.

Using factors with labels is _better_ than using integers because factors are self-describing; having a variable that has values “Male” and “Female” is better than a variable that has values 1 and 2.

---

```r
> x <- factor(c("yes", "yes", "no", "yes", "no"))
> x
[1] yes yes no yes no
Levels: no yes

> table(x)
x
no yes
 2   3

> unclass(x)
[1] 2 2 1 2 1
attr(,"levels")
[1] "no"  "yes"
```

Factors (Cont'd)
========================================================

The order of the levels can be set using the `levels` argument to `factor()`.

```r
> x <- factor(c("yes", "yes", "no", "yes", "no"),
              levels = c("yes", "no"))
> x
[1] yes yes no yes no
Levels: yes no
```

Matrices
========================================================

Matrices are vectors with a _dimension_ attribute. The dimension attribute is itself an integer vector of length 2 (nrow, ncol)

```r
> m <- matrix(nrow = 2, ncol = 3)
> m
     [,1] [,2] [,3]
[1,]   NA   NA   NA
[2,]   NA   NA   NA

> dim(m)
[1] 2 3

> attributes(m)
$dim
[1] 2 3
```

---

Matrices are constructed _column-wise_.

```r
> m <- matrix(1:6, nrow = 2, ncol = 3)
> m
     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6
```

Matrices (Cont'd)
========================================================

Matrices can be created by _column-binding_ or _row-binding_ with `cbind()` and `rbind()`.

```r
> x <- 1:3
> y <- 10:12
> cbind(x, y)
     x  y
[1,] 1 10
[2,] 2 11
[3,] 3 12
> rbind(x, y)
  [,1] [,2] [,3]
x    1    2    3
y   10   11   12
```

Data Frames
========================================================

__Data frames__ are used to store tabular data. Seen as __a special type of list where every element of the list has to have the same length__ and __each element of the list can be thought of as a column__.

Unlike matrices, __data frames__ can store different classes of objects in each column (just like lists); matrices must have every element be the same class

__Data frames__ also have a special attribute called `row.names`

__Data frames__ are usually created by calling `read.table()` or `read.csv()`

---

```r
> x <- data.frame(foo = 1:4, bar = c(T, T, F, F))
> x
  foo   bar
1   1  TRUE
2   2  TRUE
3   3 FALSE
4   4 FALSE

> nrow(x)
[1] 4

> ncol(x)
[1] 2
```

Hands-On (15 minutes)
========================================================


```r
library(swirl)
swirl()
#.....
# Select the "R Programming" entry
# Select the "Matrices and Data Frames" entry [7]

# Enjoy :)
```

Vectorized Operations
========================================================

__Vectorized operation__, the operation applied to a vector is actually applied individually to each element of the vector.

Many operations in R are __vectorized__ making code more efficient, concise and easier to read (but _challenging to write_).

Examples of __vectorized__ functions are the +, * and > operators. This applies to many other built-in R functions.

---

```r
> x <- 1:4; y <- 6:9
> x + y
[1] 7 9 11 13

> "+"(x,y)
[1]  7  9 11 13

> x * y
[1] 6 14 24 36
> x / y
[1] 0.1666667 0.2857143 0.3750000 0.4444444
```

```r
> x <- 1:4
> x > 2
[1] FALSE FALSE  TRUE  TRUE
```

```r
> sqrt(1:9)
[1] 1.000000 1.414214 1.732051 2.000000 2.236068 2.449490 2.645751 2.828427[9] 3.000000
```


Missing Values
========================================================

__Missing values__ are denoted by `NA` or `NaN` for undefined mathematical operations.

- `is.na()` is used to test objects if they are `NA`

- `is.nan()` is used to test for `NaN`

- `NA` values have a class also, so there are integer `NA`, character `NA`, etc.

- A `NaN` value is also `NA` but the converse is not true

---

```r
> x <- c(1, 2, NA, 10, 3)
> is.na(x)
[1] FALSE FALSE  TRUE FALSE FALSE

> is.nan(x)
[1] FALSE FALSE FALSE FALSE FALSE

> x <- c(1, 2, NaN, NA, 4)
> is.na(x)
[1] FALSE FALSE  TRUE  TRUE FALSE
> is.nan(x)
[1] FALSE FALSE  TRUE FALSE FALSE
```

Attributes
========================================================

R objects can have attributes

-   names, dimnames

-   dimensions (e.g. matrices, arrays)

-   class

-   length

-   other user-defined attributes/metadata

Attributes of an object can be accessed using the ```attributes()``` function.

---

```r
# Vectors
> x <- 1:3
> names(x)
NULL
> names(x) <- c("foo", "bar", "norf")
> x
foo bar norf
  1   2    3
```

```r
#List
> x <- list(a = 1, b = 2)
> x
$a
[1] 1

$b
[1] 2
```

```r
#Matrix
> m <- matrix(1:4, nrow = 2, ncol = 2)
> dimnames(m) <- list(c("a", "b"), c("c", "d"))
> m
  c d
a 1 3
b 2 4
```

Summary
========================================================

Data Types

- Atomic classes: numeric, logical, character, integer, complex \

- R objects: vectors, lists, factors, matrices and data frames

- Vectorized Operations

- Missing values

- Attributes