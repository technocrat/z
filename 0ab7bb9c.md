---
date: 2021-01-05T02:37
---

# key violation

[[[9c1fd9f0]]]
[[b9c53131]]
[[R]]
[[snips]]
``` r
library(validate)
library(magrittr)
data("samplonomy")
rule <- validator(is_unique(region, period, measure))
out <- confront(samplonomy, rule)
# showing 7 columns of output for readability
summary(out)[1:7]
#>   name items passes fails nNA error warning
#> 1   V1  1199   1197     2   0 FALSE   FALSE
violating(samplonomy, out)
#>       region freq period measure  value
#> 870 Induston    Q 2018Q2  export 165900
#> 871 Induston    Q 2018Q2  export 170000
```

