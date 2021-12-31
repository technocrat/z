---
date: 2021-12-30T21:09
---

# odds ratio explainer

[[[logistic]]]
[[packages]]
[[R]]

[S/O](https://stackoverflow.com/questions/41384075/r-calculate-and-interpret-odds-ratio-in-logistic-regression)

To convert logits to probabilities, you can use the function exp(logit)/(1+exp(logit)).

or

library(oddsratio)


``` r
library(ggplot2)
library(MASS)
data(menarche)
m <-  glm(cbind(Menarche, Total-Menarche) ~ Age, family=binomial, data=menarche)
summary(m)
#> 
#> Call:
#> glm(formula = cbind(Menarche, Total - Menarche) ~ Age, family = binomial, 
#>     data = menarche)
#> 
#> Deviance Residuals: 
#>     Min       1Q   Median       3Q      Max  
#> -2.0363  -0.9953  -0.4900   0.7780   1.3675  
#> 
#> Coefficients:
#>              Estimate Std. Error z value Pr(>|z|)    
#> (Intercept) -21.22639    0.77068  -27.54   <2e-16 ***
#> Age           1.63197    0.05895   27.68   <2e-16 ***
#> ---
#> Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
#> 
#> (Dispersion parameter for binomial family taken to be 1)
#> 
#>     Null deviance: 3693.884  on 24  degrees of freedom
#> Residual deviance:   26.703  on 23  degrees of freedom
#> AIC: 114.76
#> 
#> Number of Fisher Scoring iterations: 4

#predict gives the predicted value in terms of logits
plot.dat <- data.frame(prob = menarche$Menarche/menarche$Total,
                       age = menarche$Age,
                       fit = predict(m, menarche))
#convert those logit values to probabilities
plot.dat$fit_prob <- exp(plot.dat$fit)/(1+exp(plot.dat$fit))

ggplot(plot.dat, aes(x=age, y=prob)) + 
  geom_point() +
  geom_line(aes(x=age, y=fit_prob))
```

![](https://i.imgur.com/TkQCzEP.png)


