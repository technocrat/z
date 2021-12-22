---
date: 2021-12-22T01:47
---

# marginal effects

[[[packages]]]

``` r
library(ggplot2)
library(marginaleffects)

mod <- lm(mpg ~ hp * wt * am, data = mtcars)

mfx <- marginaleffects(mod)
summary(mfx)
#> Average marginal effects 
#>       type Term   Effect Std. Error  z value   Pr(>|z|)    2.5 %   97.5 %
#> 1 response   am -0.04811    1.85260 -0.02597 0.97928233 -3.67913  3.58291
#> 2 response   hp -0.03807    0.01279 -2.97717 0.00290923 -0.06314 -0.01301
#> 3 response   wt -3.93909    1.08596 -3.62728 0.00028642 -6.06754 -1.81065
#> 
#> Model type:  lm 
#> Prediction type:  response
plot_cme(mod, effect = "hp", condition = c("wt", "am"))
```

![](https://i.imgur.com/JmfcvBH.png)

``` r
predictions(mod, variables = c("am", "wt"))
#>        type predicted std.error  conf.low conf.high       hp am     wt
#> 1  response 23.259500 2.7059342 17.674726  28.84427 146.6875  0 1.5130
#> 2  response 27.148334 2.8518051 21.262498  33.03417 146.6875  1 1.5130
#> 3  response 20.504387 1.3244556 17.770845  23.23793 146.6875  0 2.5425
#> 4  response 21.555612 1.0723852 19.342318  23.76891 146.6875  1 2.5425
#> 5  response 18.410286 0.6151016 17.140779  19.67979 146.6875  0 3.3250
#> 6  response 17.304709 1.5528055 14.099876  20.50954 146.6875  1 3.3250
#> 7  response 17.540532 0.7293676 16.035192  19.04587 146.6875  0 3.6500
#> 8  response 15.539158 2.1453449 11.111383  19.96693 146.6875  1 3.6500
#> 9  response 12.793013 2.9784942  6.645703  18.94032 146.6875  0 5.4240
#> 10 response  5.901966 5.8149853 -6.099574  17.90351 146.6875  1 5.4240
predictions(mod, newdata = typical(am = 0, wt = c(2, 4)))
#>       type predicted std.error conf.low conf.high       hp am wt
#> 1 response  21.95621  2.038630 17.74868  26.16373 146.6875  0  2
#> 2 response  16.60387  1.083201 14.36826  18.83949 146.6875  0  4
plot_cap(mod, condition = c("hp", "wt"))
```

![](https://i.imgur.com/QrXI4DM.png)

``` r
predictions(mod, 
            newdata = typical(am = 0:1, 
                              wt = fivenum(mtcars$wt), 
                              hp = seq(100, 300, 10))) |>
  ggplot(aes(x = hp, y = predicted, ymin = conf.low, ymax = conf.high)) +
  geom_ribbon(aes(fill = factor(wt)), alpha = .2) +
  geom_line(aes(color = factor(wt))) +
  facet_wrap(~am) +
  theme_minimal()
```

![](https://i.imgur.com/1y13q6Y.png)

``` r
mod <- lm(mpg ~ factor(cyl), data = mtcars)
plot_cap(mod, condition = "cyl")
```

![](https://i.imgur.com/N13JZUA.png)

``` r
dat <- mtcars
dat$am <- as.logical(dat$am)
dat$cyl <- as.factor(dat$cyl)

mod <- lm(mpg ~ am + cyl + hp, data = dat)
mm <- marginalmeans(mod)
summary(mm)
#> Estimated marginal means 
#>   Term Group  Mean Std. Error z value   Pr(>|z|) 2.5 % 97.5 %
#> 1   am FALSE 18.32     0.7854   23.33 < 2.22e-16 16.78  19.86
#> 2   am  TRUE 22.48     0.8343   26.94 < 2.22e-16 20.84  24.11
#> 3  cyl     4 22.88     1.3566   16.87 < 2.22e-16 20.23  25.54
#> 4  cyl     6 18.96     1.0729   17.67 < 2.22e-16 16.86  21.06
#> 5  cyl     8 19.35     1.3771   14.05 < 2.22e-16 16.65  22.05
#> 
#> Model type:  lm 
#> Prediction type:  response
```
