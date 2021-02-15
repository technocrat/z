---
date: 2021-02-15T16:48
---

# Overlay normal density curve on histogram

[[[snips]]]
[[VIZ]]
[[R]]

``` r
suppressPackageStartupMessages({
  library(ggplot2)
})

p <- ggplot(iris,aes(Sepal.Length))
p + geom_histogram(aes(y = ..density..), bins = 40,
                   fill = "light grey",
                   color = "black") +
    geom_density(color = "green", size = 1) +
    stat_function(fun = dnorm, 
                  args = list(mean = mean(iris$Sepal.Length), 
                              sd = sd(iris$Sepal.Length)),
                  color = "orange", size = 1) +
    ggtitle("Histogram with density (green) and normal density (orange)") +
      theme_minimal()
```

![](https://i.imgur.com/A90s3ZV.png)

