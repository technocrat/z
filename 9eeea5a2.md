---
date: 2021-08-14T23:42
---

# logical subset

[[[snips]]]
[[R]]

``` r
outcome <- as.numeric(c(6,7,"NA",8,3,"NA",8,4,"NA"))
#> Warning: NAs introduced by coercion
outcome[which(is.na(outcome))] <-
  pmin(outcome[!is.na(outcome)][c(T,F)],outcome[!is.na(outcome)][c(F,T)])
outcome
#> [1] 6 7 6 8 3 3 8 4 4
```
