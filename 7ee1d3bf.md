---
date: 2021-05-20T20:07
---

# apply family

[[[functions]]]
[[R]]

``` r

the_list <- list("a" = 1, "b" = 2, "c" = 3)
getElement(the_list, "a")

# `[[` is a function!
lapply(big_list, "[[", "a")
set.seed(137); m <- matrix(sample(1:27,9),nrow=3)
m
#>      [,1] [,2] [,3]
#> [1,]   27   15    7
#> [2,]    2    6   11
#> [3,]    8   24    3

# row sums

# apply returns a vector or array or list of values obtained 
# by applying a function to __margins__ of an array or matrix.
rowSums(m)
#> [1] 49 19 35
apply(m,1,sum) # is rowwise
#> [1] 49 19 35
colSums(m)
#> [1] 37 45 21
apply(m,2,sum) # is colwise
#> [1] 37 45 21

# lapply returns a list of the same length as X, each element 
# of which is the result of applying FUN to the corresponding element of X.

ml <- list(A=matrix(1:9,nrow=3),B=1:5,C=8)
ml
#> $A
#>      [,1] [,2] [,3]
#> [1,]    1    4    7
#> [2,]    2    5    8
#> [3,]    3    6    9
#> 
#> $B
#> [1] 1 2 3 4 5
#> 
#> $C
#> [1] 8

lapply(ml,sum)
#> $A
#> [1] 45
#> 
#> $B
#> [1] 15
#> 
#> $C
#> [1] 8

unlist(lapply(ml,sum))
#>  A  B  C 
#> 45 15  8

# λ lambda

lapply(ml,function(x) x*20)
#> $A
#>      [,1] [,2] [,3]
#> [1,]   20   80  140
#> [2,]   40  100  160
#> [3,]   60  120  180
#> 
#> $B
#> [1]  20  40  60  80 100
#> 
#> $C
#> [1] 160

# sapply user-friendly version and wrapper of lapply by default
# returning a vector, matrix or, if simplify = “array”, an array 
# if appropriate, by applying simplify2array(). 
# sapply(x, f, simplify = FALSE, USE.NAMES = FALSE) 
# is the same as lapply(x, f).

sapply(ml,sum)
#>  A  B  C 
#> 45 15  8



# mapply stands for multi-variant apply

mapply(rep,1:4,4:1)
#> [[1]]
#> [1] 1 1 1 1
#> 
#> [[2]]
#> [1] 2 2 2
#> 
#> [[3]]
#> [1] 3 3
#> 
#> [[4]]
#> [1] 4
x <- c(A = 20, B = 1, C = 40)
y <- c(J = 430, K = 50, L = 10)

simply <- function(u,v) (u+v)*2

mapply(simply,x,y)
#>   A   B   C 
#> 900 102 100

# tapply  a function to each cell of a ragged array, that is to 
# each (non-empty) group of values given by a unique combination 
# of the levels of certain factors

tapply(iris$Sepal.Length,iris$Species,max)
#>     setosa versicolor  virginica 
#>        5.8        7.0        7.9
```
