---
date: 2021-01-02T14:05
---

# group by quantile

Note that for any numeric vector x, you can create groups based on quantiles like this:

 	cut(x, quantile(x, seq(0, 1, 0.1)), include.lowest = TRUE)
    
[[[R]]]
[[snips]]