---
date: 2021-01-10T17:54
---

# boxcox

	library(fpp3)
    lambda <- past %>%
      features(kwh, features = guerrero) %>%
      pull(lambda_guerrero)
    past %>%
      model(
        ETS_bc = ETS(box_cox(kwh, lambda), ic = "aicc", opt_crit = "lik"),
        ARIMA_bc = ARIMA(box_cox(kwh, lambda), ic = "aicc", stepwise = F),
        snaive_bc = SNAIVE(box_cox(kwh, lambda) ~ drift())
      ) -> fc
    fc %>% forecast(h = 56) -> fc
    accuracy(fc,future) 
 
[[[7d9a7afc]]]
[[TS]]
[[snips]]
[[R]]