---
date: 2021-01-30T01:44
---

# unitroot

[[[TS]]]


    google_2015 %>%
      features(Close, unitroot_kpss)
    #> # A tibble: 1 x 3
    #>   Symbol kpss_stat kpss_pvalue
    #>   <chr>      <dbl>       <dbl>
    #> 1 GOOG        3.56        0.01

The reported p-value is set to 0.01 if it is less than that, or to 0.1 if it is greater than that. In this case, the test statistic (3.56) is much bigger than the 1% critical value, so the p-value is less than 0.01, indicating that the null hypothesis is rejected. That is, the data are not stationary. We can difference the data, and apply the test again.