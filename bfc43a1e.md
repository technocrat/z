---
date: 2021-12-04T01:04
---

# subset a country from spData::world

[[[snips]]]
[[sf]]
[[logistic]]

``` r
library(ggplot2)
library(sf)
#> Linking to GEOS 3.9.0, GDAL 3.2.2, PROJ 7.2.1
library(magrittr)
library(spData)
#> To access larger datasets in this package, install the spDataLarge
#> package with: `install.packages('spDataLarge',
#> repos='https://nowosad.github.io/drat/', type='source')`
data("world")
world[140,] %>% st_geometry() %>% ggplot() + geom_sf() + theme_minimal()
```

![](https://i.imgur.com/Tf32SbB.png)

<sup>Created on 2021-12-03 by the [reprex package](https://reprex.tidyverse.org) (v2.0.1)</sup>