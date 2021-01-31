---
date: 2021-01-30T21:22
---

# {stringdist}

clustering text

[[[snips]]]
[[R]]
``` r
subj <- c("physics", "astrophysics", "metaphysics", "astronomy","chemistry")

M <- stringdist::stringdistmatrix(subj,subj,useNames = TRUE)
H <- hclust(as.dist(M),method="single")
H            
#> 
#> Call:
#> hclust(d = as.dist(M), method = "single")
#> 
#> Cluster method   : single 
#> Number of objects: 5
plot(H)
```

![](https://i.imgur.com/pxJqLcZ.png)

