---
date: 2021-03-04T17:39
---

# feasts example

[[Package]]

``` r
suppressPackageStartupMessages({
  library(feasts)
})

seas_adj <- tsibbledata::aus_retail %>% 
  model(stl_model = STL(Turnover ~ trend(window = 10) + 
                          season(window = "periodic"))) %>%
  components() %>%
  dplyr::select(State,Industry,Month,Turnover,season_adjust)

seas_adj
#> # A tsibble: 64,532 x 5 [1M]
#> # Key:       State, Industry [152]
#>    State              Industry                      Month Turnover season_adjust
#>    <chr>              <chr>                         <mth>    <dbl>         <dbl>
#>  1 Australian Capita… Cafes, restaurants and ca… 1982 Apr      4.4          4.85
#>  2 Australian Capita… Cafes, restaurants and ca… 1982 May      3.4          3.21
#>  3 Australian Capita… Cafes, restaurants and ca… 1982 Jun      3.6          4.12
#>  4 Australian Capita… Cafes, restaurants and ca… 1982 Jul      4            4.06
#>  5 Australian Capita… Cafes, restaurants and ca… 1982 Aug      3.6          3.47
#>  6 Australian Capita… Cafes, restaurants and ca… 1982 Sep      4.2          3.88
#>  7 Australian Capita… Cafes, restaurants and ca… 1982 Oct      4.8          3.85
#>  8 Australian Capita… Cafes, restaurants and ca… 1982 Nov      5.4          4.68
#>  9 Australian Capita… Cafes, restaurants and ca… 1982 Dec      6.9          5.22
#> 10 Australian Capita… Cafes, restaurants and ca… 1983 Jan      3.8          6.21
#> # … with 64,522 more rows
```

