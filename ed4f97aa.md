---
date: 2021-03-04T17:48
---

# summarise_all function

[[[snips]]]
[[R]]

``` r
suppressPackageStartupMessages({
  library(dplyr)
})
mtcars %>% summarise_all(~ if(is.numeric(.)) mean(., na.rm = TRUE) else last(.))
#>        mpg    cyl     disp       hp     drat      wt     qsec     vs      am
#> 1 20.09062 6.1875 230.7219 146.6875 3.596563 3.21725 17.84875 0.4375 0.40625
#>     gear   carb
#> 1 3.6875 2.8125
```
