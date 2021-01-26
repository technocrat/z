---
date: 2021-01-26T13:46
---

# Use of which

[[[Indexing]]]
[[R]]
[[snips]]

$y$: Divide $x = \mathbb{N}$ into the largest set of subgroups such that each group has one more \member that the preceding ordinal group and no remaining group has fewer than three members.

``` r
find_grps <- function(N) {
  which(cumsum(seq(1:N)) <= N)
}
find_grps(30)
#> [1] 1 2 3 4 5 6 7
```


