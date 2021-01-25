---
date: 2021-01-25T02:59
---

# Winzorizing

[[[robust]]]
[[Statistics]]

`mean` is sensitive to extreme values; removing the upper and lower extremes is said to give a *robust* mean. Tukey, [as quoted](https://blogs.sas.com/content/iml/2017/02/08/winsorization-good-bad-and-ugly.html)

> we are likely to think of them as 'strays' [or]'wild shots' ... and to focus our attention on how normally distributed the rest of the distribution appears to be. One who does this commits two oversights, forgetting Winsor's principle that 'all distributions are normal in the middle,' and forgetting that the distribution relevant to statistical practice is that of the values actually provided and not of the values which ought to have been provided. 

> Sets of observations which have been de-tailed by over-vigorous use of a rule for rejecting outliers are inappropriate, since they are not samples. 


Tukey, J. W. 1960. A survey of sampling from contaminated distributions. In Olkin, I., Ghurye, S.G., Hoeffding, W., Madow, W.G. and Mann, H.B. (Eds) Contributions to Probability and Statistics: Essays in Honor of Harold Hotelling. Stanford, CA: Stanford University Press, 448-485. 

``` r
mean(iris[,1])
#> [1] 5.843333

iris[which(iris[,1] > 7),][1] <- 7

mean(iris[,1])
#> [1] 5.805333
```


