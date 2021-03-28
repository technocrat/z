---
date: 2021-03-28T19:14
---

# replace NaN in a data frame

[[[munging]]]
[[functions]]
[[R]]


``` r
b <- data.frame(c1=c(1, NaN, 2), c2=c(NaN, 2, 7))
b
#>    c1  c2
#> 1   1 NaN
#> 2 NaN   2
#> 3   2   7
b[is.na(b)] <- NA
b
#>   c1 c2
#> 1  1 NA
#> 2 NA  2
#> 3  2  7
```

