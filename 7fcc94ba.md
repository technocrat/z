---
date: 2020-12-25T18:15
---

# [Time series count data](https://personal.utdallas.edu/~pxb054000/code/count-examples/ECTS-I-2010.pdf)

[Examples](https://personal.utdallas.edu/~pxb054000/code/count-examples/)

Count data are the result of a process of measuring the number of discrete events over some period of time.

Typically, these models assume that the process that generates the events is independent of time (t).  

This means that they are memoryless. 

The times between events are assumed to be independent and exponentially distributed.

This is a very strong set of restrictions:  most event data violate them in one or more ways. 

However,

> In practice, this rarely matters provided our counts are sufficiently large. If the minimum number of customers is at least 100, then the difference between a continuous sample space [100,∞) and the discrete sample space {100,101,102,…} has no perceivable effect on our forecasts. However, if our data contains small counts (0,1,2,…), then we need to use forecasting methods that are more appropriate for a sample space of non-negative integers.

[Hyndman](https://otexts.com/fpp3/counts.html)

[[[R]]]
[[[TS]]]
[[Statistics]]