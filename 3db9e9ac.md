---
date: 2021-05-20T02:00
---

# Two-sample Wilcoxon test

[[[stattests]]
[[functions]]
[[R]]

``` r
library(ISwR)
attach(energy)
energy
#>    expend stature
#> 1    9.21   obese
#> 2    7.53    lean
#> 3    7.48    lean
#> 4    8.08    lean
#> 5    8.09    lean
#> 6   10.15    lean
#> 7    8.40    lean
#> 8   10.88    lean
#> 9    6.13    lean
#> 10   7.90    lean
#> 11  11.51   obese
#> 12  12.79   obese
#> 13   7.05    lean
#> 14  11.85   obese
#> 15   9.97   obese
#> 16   7.48    lean
#> 17   8.79   obese
#> 18   9.69   obese
#> 19   9.68   obese
#> 20   7.58    lean
#> 21   9.19   obese
#> 22   8.11    lean
summary(energy)
#>      expend        stature  
#>  Min.   : 6.130   lean :13  
#>  1st Qu.: 7.660   obese: 9  
#>  Median : 8.595             
#>  Mean   : 8.979             
#>  3rd Qu.: 9.900             
#>  Max.   :12.790
stem(expend)
#> 
#>   The decimal point is at the |
#> 
#>    6 | 1155569
#>    8 | 111482277
#>   10 | 02959
#>   12 | 8
# silly for so few observations; here null is ratio is equal to one
# and must be rejected at p-value much greater than any reasonable
# alpha; note also that 1 is within the confidence intervals
var.test(expend~stature)
#> 
#>  F test to compare two variances
#> 
#> data:  expend by stature
#> F = 0.78445, num df = 12, denom df = 8, p-value = 0.6797
#> alternative hypothesis: true ratio of variances is not equal to 1
#> 95 percent confidence interval:
#>  0.1867876 2.7547991
#> sample estimates:
#> ratio of variances 
#>           0.784446
# don't understand this one
# p 116
wilcox.test(expend~stature)
#> Warning in wilcox.test.default(x = c(7.53, 7.48, 8.08, 8.09, 10.15, 8.4, :
#> cannot compute exact p-value with ties
#> 
#>  Wilcoxon rank sum test with continuity correction
#> 
#> data:  expend by stature
#> W = 12, p-value = 0.002122
#> alternative hypothesis: true location shift is not equal to 0
```
