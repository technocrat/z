---
date: 2021-12-18T01:50
---

# collapse

[[[packages]]]
[[R]]

``` r
# https://sebkrantz.github.io/collapse/articles/collapse_and_dplyr.html
library(collapse)
#> collapse 1.6.5, see ?`collapse-package` or ?`collapse-documentation`
#> Note: stats::D  ->  D.expression, D.call, D.name
#> 
#> Attaching package: 'collapse'
#> The following object is masked from 'package:stats':
#> 
#>     D
library(dplyr)
#> 
#> Attaching package: 'dplyr'
#> The following objects are masked from 'package:stats':
#> 
#>     filter, lag
#> The following objects are masked from 'package:base':
#> 
#>     intersect, setdiff, setequal, union
head(GGDC10S)
#>   Country Regioncode             Region Variable Year      AGR      MIN
#> 1     BWA        SSA Sub-saharan Africa       VA 1960       NA       NA
#> 2     BWA        SSA Sub-saharan Africa       VA 1961       NA       NA
#> 3     BWA        SSA Sub-saharan Africa       VA 1962       NA       NA
#> 4     BWA        SSA Sub-saharan Africa       VA 1963       NA       NA
#> 5     BWA        SSA Sub-saharan Africa       VA 1964 16.30154 3.494075
#> 6     BWA        SSA Sub-saharan Africa       VA 1965 15.72700 2.495768
#>         MAN        PU       CON      WRT      TRA     FIRE      GOV      OTH
#> 1        NA        NA        NA       NA       NA       NA       NA       NA
#> 2        NA        NA        NA       NA       NA       NA       NA       NA
#> 3        NA        NA        NA       NA       NA       NA       NA       NA
#> 4        NA        NA        NA       NA       NA       NA       NA       NA
#> 5 0.7365696 0.1043936 0.6600454 6.243732 1.658928 1.119194 4.822485 2.341328
#> 6 1.0181992 0.1350976 1.3462312 7.064825 1.939007 1.246789 5.695848 2.678338
#>        SUM
#> 1       NA
#> 2       NA
#> 3       NA
#> 4       NA
#> 5 37.48229
#> 6 39.34710
descr(GGDC10S, cols = is_categorical)
#> Dataset: GGDC10S, 4 Variables, N = 5027
#> --------------------------------------------------------------------------------
#> Country (character): Country
#> Stats: 
#>      N  Ndist
#>   5027     43
#> Table: 
#>      Freq  Perc
#> ARG   124  2.47
#> BOL   123  2.45
#> BRA   124  2.47
#> BWA   104  2.07
#> CHL   125  2.49
#> CHN   125  2.49
#> COL   123  2.45
#>   ---
#>      Freq  Perc
#> SWE   126  2.51
#> THA   124  2.47
#> TWN   126  2.51
#> TZA   104  2.07
#> USA   129  2.57
#> VEN   125  2.49
#> ZAF   104  2.07
#> ZMB   104  2.07
#> 
#> Summary of Table: 
#>    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#>       4     105     124     117     126     129 
#> --------------------------------------------------------------------------------
#> Regioncode (character): Region code
#> Stats: 
#>      N  Ndist
#>   5027      6
#> Table: 
#>       Freq   Perc
#> ASI   1372  27.29
#> EUR   1004  19.97
#> LAM   1117  22.22
#> MENA   257   5.11
#> NAM    129   2.57
#> SSA   1148  22.84
#> --------------------------------------------------------------------------------
#> Region (character): Region
#> Stats: 
#>      N  Ndist
#>   5027      6
#> Table: 
#>                               Freq   Perc
#> Asia                          1372  27.29
#> Europe                        1004  19.97
#> Latin America                 1117  22.22
#> Middle East and North Africa   257   5.11
#> North America                  129   2.57
#> Sub-saharan Africa            1148  22.84
#> --------------------------------------------------------------------------------
#> Variable (character): Variable
#> Stats: 
#>      N  Ndist
#>   5027      2
#> Table: 
#>      Freq   Perc
#> EMP  2516  50.05
#> VA   2511  49.95
#> --------------------------------------------------------------------------------
aperm(qsu(GGDC10S, ~Variable, cols = is.numeric))
#> , , EMP
#> 
#>          N        Mean          SD       Min         Max
#> Year  2516   1981.3843     17.6077      1947        2012
#> AGR   2225  16746.4339  55644.8433    5.2407      390980
#> MIN   2216     359.605   1295.2851    0.1123  12908.3636
#> MAN   2216    5204.331  13924.8173    1.0416  145898.403
#> PU    2215    153.4192    365.1154      0.12   3903.8074
#> CON   2216   1793.6096   5114.1267    1.7136  69887.5583
#> WRT   2216   4368.3826   8616.8499    1.6373  84165.1129
#> TRA   2216   1442.4432   3289.4172    1.7332  31222.7358
#> FIRE  2216    1330.678   3113.7356    0.7807  28092.6863
#> GOV   1780   4196.8056   7278.0363         0  44817.3409
#> OTH   2109   2268.1121   8022.2413    4.0746  104517.871
#> SUM   2225  36846.8741  96318.6544  173.8829      764200
#> 
#> , , VA
#> 
#>          N         Mean           SD         Min             Max
#> Year  2511    1981.7762      17.5343        1947            2013
#> AGR   2139  5'137560.88  52'913681.8           0  1.19187778e+09
#> MIN   2139  3'802686.57  46'062895.7           0  1.10344053e+09
#> MAN   2139  11'270966.4  89'674720.3           0  1.86843541e+09
#> PU    2139   683126.976  3'643270.26           0     65'324543.8
#> CON   2139  3'666191.22    34'696912           0      860'638677
#> WRT   2139   6'903431.8  52'500538.4           0  1.15497404e+09
#> TRA   2139  2'998080.02  23'900671.1           0      547'047040
#> FIRE  2139  3'372504.14    19'416463  -2848.8087      387'997506
#> GOV   1702  3'498683.46  24'143501.2           0      485'535400
#> OTH   2139  3'343192.42  21'880087.7           0      402'671182
#> SUM   2139  43'961639.1   358'350627           0  8.06794210e+09
GGDC10S <- qTBL(GGDC10S)
GGDC10S
#> # A tibble: 5,027 × 16
#>    Country Regioncode Region     Variable  Year   AGR   MIN    MAN     PU    CON
#>    <chr>   <chr>      <chr>      <chr>    <dbl> <dbl> <dbl>  <dbl>  <dbl>  <dbl>
#>  1 BWA     SSA        Sub-sahar… VA        1960  NA   NA    NA     NA     NA    
#>  2 BWA     SSA        Sub-sahar… VA        1961  NA   NA    NA     NA     NA    
#>  3 BWA     SSA        Sub-sahar… VA        1962  NA   NA    NA     NA     NA    
#>  4 BWA     SSA        Sub-sahar… VA        1963  NA   NA    NA     NA     NA    
#>  5 BWA     SSA        Sub-sahar… VA        1964  16.3  3.49  0.737  0.104  0.660
#>  6 BWA     SSA        Sub-sahar… VA        1965  15.7  2.50  1.02   0.135  1.35 
#>  7 BWA     SSA        Sub-sahar… VA        1966  17.7  1.97  0.804  0.203  1.35 
#>  8 BWA     SSA        Sub-sahar… VA        1967  19.1  2.30  0.938  0.203  0.897
#>  9 BWA     SSA        Sub-sahar… VA        1968  21.1  1.84  0.750  0.203  1.22 
#> 10 BWA     SSA        Sub-sahar… VA        1969  21.9  5.24  2.14   0.578  3.47 
#> # … with 5,017 more rows, and 6 more variables: WRT <dbl>, TRA <dbl>,
#> #   FIRE <dbl>, GOV <dbl>, OTH <dbl>, SUM <dbl>
GGDC10S %>% fnobs
#>    Country Regioncode     Region   Variable       Year        AGR        MIN 
#>       5027       5027       5027       5027       5027       4364       4355 
#>        MAN         PU        CON        WRT        TRA       FIRE        GOV 
#>       4355       4354       4355       4355       4355       4355       3482 
#>        OTH        SUM 
#>       4248       4364
GGDC10S %>% fndistinct
#>    Country Regioncode     Region   Variable       Year        AGR        MIN 
#>         43          6          6          2         67       4353       4224 
#>        MAN         PU        CON        WRT        TRA       FIRE        GOV 
#>       4353       4237       4339       4344       4334       4349       3470 
#>        OTH        SUM 
#>       4238       4364
GGDC10S %>% select_at(6:16) %>% fmedian
#>        AGR        MIN        MAN         PU        CON        WRT        TRA 
#>  4394.5194   173.2234  3718.0981   167.9500  1473.4470  3773.6430  1174.8000 
#>       FIRE        GOV        OTH        SUM 
#>   960.1251  3928.5127  1433.1722 23186.1936
GGDC10S %>% select_at(6:16) %>% fmean
#>        AGR        MIN        MAN         PU        CON        WRT        TRA 
#>  2526696.5  1867908.9  5538491.4   335679.5  1801597.6  3392909.5  1473269.7 
#>       FIRE        GOV        OTH        SUM 
#>  1657114.8  1712300.3  1684527.3 21566436.8
GGDC10S %>% fmode
#>            Country         Regioncode             Region           Variable 
#>              "USA"              "ASI"             "Asia"              "EMP" 
#>               Year                AGR                MIN                MAN 
#>             "2010" "171.315882316326"                "0" "4645.12507642586" 
#>                 PU                CON                WRT                TRA 
#>                "0" "1.34623115930777" "21.8380052682527" "8.97743416914571" 
#>               FIRE                GOV                OTH                SUM 
#> "40.0701608636442"                "0" "3626.84423577048" "37.4822945751317"
GGDC10S %>% fmode(drop = FALSE)
#> # A tibble: 1 × 16
#>   Country Regioncode Region Variable  Year   AGR   MIN   MAN    PU   CON   WRT
#> * <chr>   <chr>      <chr>  <chr>    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
#> 1 USA     ASI        Asia   EMP       2010  171.     0 4645.     0  1.35  21.8
#> # … with 5 more variables: TRA <dbl>, FIRE <dbl>, GOV <dbl>, OTH <dbl>,
#> #   SUM <dbl>
GGDC10S %>% 
  group_by(Variable, Country) %>%
  select_at(6:16) %>% fmean
#> # A tibble: 85 × 13
#>    Variable Country     AGR     MIN     MAN      PU     CON    WRT    TRA   FIRE
#>    <chr>    <chr>     <dbl>   <dbl>   <dbl>   <dbl>   <dbl>  <dbl>  <dbl>  <dbl>
#>  1 EMP      ARG       1420.   52.1   1932.   102.     742.  1.98e3 6.49e2  628. 
#>  2 EMP      BOL        964.   56.0    235.     5.35   123.  2.82e2 1.15e2   44.6
#>  3 EMP      BRA      17191.  206.    6991.   365.    3525.  8.51e3 2.05e3 4414. 
#>  4 EMP      BWA        188.   10.5     18.1    3.09    25.3 3.63e1 8.36e0   15.3
#>  5 EMP      CHL        702.  101.     625.    29.4    296.  6.95e2 2.58e2  272. 
#>  6 EMP      CHN     287744. 7050.   67144.  1606.   20852.  2.89e4 1.39e4 4929. 
#>  7 EMP      COL       3091.  145.    1175.    33.9    524.  2.07e3 4.70e2  649. 
#>  8 EMP      CRI        231.    1.70   136.    14.3     57.6 1.57e2 4.24e1   54.9
#>  9 EMP      DEW       2490.  407.    8473.   226.    2093.  4.44e3 1.48e3 1689. 
#> 10 EMP      DNK        236.    8.03   507.    13.8    171.  4.55e2 1.61e2  181. 
#> # … with 75 more rows, and 3 more variables: GOV <dbl>, OTH <dbl>, SUM <dbl>
GGDC10S %>% group_by(Variable, Country) %>% attr("groups")
#> # A tibble: 85 × 3
#>    Variable Country       .rows
#>    <chr>    <chr>   <list<int>>
#>  1 EMP      ARG            [62]
#>  2 EMP      BOL            [61]
#>  3 EMP      BRA            [62]
#>  4 EMP      BWA            [52]
#>  5 EMP      CHL            [63]
#>  6 EMP      CHN            [62]
#>  7 EMP      COL            [61]
#>  8 EMP      CRI            [62]
#>  9 EMP      DEW            [61]
#> 10 EMP      DNK            [64]
#> # … with 75 more rows
GGDC10S %>% group_by(Variable, Country) %>% GRP %>% str
#> List of 8
#>  $ N.groups   : int 85
#>  $ group.id   : int [1:5027] 46 46 46 46 46 46 46 46 46 46 ...
#>  $ group.sizes: int [1:85] 62 61 62 52 63 62 61 62 61 64 ...
#>  $ groups     :List of 2
#>   ..$ Variable: chr [1:85] "EMP" "EMP" "EMP" "EMP" ...
#>   .. ..- attr(*, "label")= chr "Variable"
#>   .. ..- attr(*, "format.stata")= chr "%9s"
#>   ..$ Country : chr [1:85] "ARG" "BOL" "BRA" "BWA" ...
#>   .. ..- attr(*, "label")= chr "Country"
#>   .. ..- attr(*, "format.stata")= chr "%9s"
#>  $ group.vars : chr [1:2] "Variable" "Country"
#>  $ ordered    : logi [1:2] TRUE TRUE
#>  $ order      : NULL
#>  $ call       : language GRP.grouped_df(X = .)
#>  - attr(*, "class")= chr "GRP"
GGDC10S %>% fgroup_by(Variable, Country) %>% get_vars(6:16) %>% fmedian
#> # A tibble: 85 × 13
#>    Variable Country     AGR     MIN     MAN      PU     CON    WRT    TRA   FIRE
#>    <chr>    <chr>     <dbl>   <dbl>   <dbl>   <dbl>   <dbl>  <dbl>  <dbl>  <dbl>
#>  1 EMP      ARG       1325.   47.4   1988.   105.     782.  1.85e3 5.80e2  464. 
#>  2 EMP      BOL        943.   53.5    167.     4.46    66.0 1.32e2 9.70e1   15.3
#>  3 EMP      BRA      17481.  225.    7208.   376.    4055.  6.45e3 1.58e3 4355. 
#>  4 EMP      BWA        175.   12.2     13.1    3.71    19.0 2.11e1 6.75e0   10.4
#>  5 EMP      CHL        690.   93.9    607.    25.8    230.  4.84e2 2.05e2  106. 
#>  6 EMP      CHN     293915  8150.   61761.  1139.   10578.  1.70e4 9.56e3 4328. 
#>  7 EMP      COL       3006.   84.0   1033.    37.1    419.  1.55e3 3.91e2  655. 
#>  8 EMP      CRI        216.    1.49   114.     7.92    55.0 8.98e1 2.55e1   19.6
#>  9 EMP      DEW       2178   320.    8459.   247     2095.  4.45e3 1.53e3 1656  
#> 10 EMP      DNK        187.    3.75   508.    13.6    165.  4.61e2 1.61e2  169. 
#> # … with 75 more rows, and 3 more variables: GOV <dbl>, OTH <dbl>, SUM <dbl>
GGDC10S |> fsubset(Variable == "VA" & Year > 1990, Country, Year, AGR:GOV) |> head(3)
#> # A tibble: 3 × 11
#>   Country  Year   AGR   MIN   MAN    PU   CON   WRT   TRA  FIRE   GOV
#>   <chr>   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
#> 1 BWA      1991  303. 2647.  473.  161.  580.  807.  233.  433. 1073.
#> 2 BWA      1992  333. 2691.  537.  178.  679.  725.  285.  517. 1234.
#> 3 BWA      1993  405. 2625.  567.  219.  634.  772.  350.  673. 1487.
GGDC10S %>%
  fgroup_by(Variable, Country) %>%
  get_vars(6:16) %>% {
    cbind(fmedian(.),
          add_stub(fmean(., keep.group_vars = FALSE), "mean_"))
  } %>% head(3)
#>   Variable Country        AGR       MIN       MAN         PU        CON
#> 1      EMP     ARG  1324.5255  47.35255 1987.5912 104.738825  782.40283
#> 2      EMP     BOL   943.1612  53.53538  167.1502   4.457895   65.97904
#> 3      EMP     BRA 17480.9810 225.43693 7207.7915 375.851832 4054.66103
#>        WRT        TRA       FIRE      GOV       OTH       SUM   mean_AGR
#> 1 1854.612  579.93982  464.39920 1738.836  866.1119  9743.223  1419.8013
#> 2  132.225   96.96828   15.34259       NA  384.0678  1842.055   964.2103
#> 3 6454.523 1580.81120 4354.86210 4449.942 4478.6927 51881.110 17191.3529
#>    mean_MIN  mean_MAN    mean_PU  mean_CON  mean_WRT  mean_TRA  mean_FIRE
#> 1  52.08903 1931.7602 101.720936  742.4044 1982.1775  648.5119  627.79291
#> 2  56.03295  235.0332   5.346433  122.7827  281.5164  115.4728   44.56442
#> 3 206.02389 6991.3710 364.573404 3524.7384 8509.4612 2054.3731 4413.54448
#>   mean_GOV  mean_OTH  mean_SUM
#> 1 2043.471  992.4475 10542.177
#> 2       NA  395.5650  2220.524
#> 3 5307.280 5710.2665 54272.985

# This efficiently scales and centers (i.e. standardizes) the data
GGDC10S %>%
  fgroup_by(Variable, Country) %>%
  fselect(Country, Variable, AGR:SUM) %>% fscale
#> # A tibble: 5,027 × 13
#>    Country Variable    AGR    MIN    MAN     PU    CON    WRT    TRA   FIRE
#>  * <chr>   <chr>     <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>
#>  1 BWA     VA       NA     NA     NA     NA     NA     NA     NA     NA    
#>  2 BWA     VA       NA     NA     NA     NA     NA     NA     NA     NA    
#>  3 BWA     VA       NA     NA     NA     NA     NA     NA     NA     NA    
#>  4 BWA     VA       NA     NA     NA     NA     NA     NA     NA     NA    
#>  5 BWA     VA       -0.738 -0.717 -0.668 -0.805 -0.692 -0.603 -0.589 -0.635
#>  6 BWA     VA       -0.739 -0.717 -0.668 -0.805 -0.692 -0.603 -0.589 -0.635
#>  7 BWA     VA       -0.736 -0.717 -0.668 -0.805 -0.692 -0.603 -0.589 -0.635
#>  8 BWA     VA       -0.734 -0.717 -0.668 -0.805 -0.692 -0.604 -0.589 -0.635
#>  9 BWA     VA       -0.730 -0.717 -0.668 -0.805 -0.692 -0.604 -0.588 -0.635
#> 10 BWA     VA       -0.729 -0.716 -0.667 -0.803 -0.690 -0.603 -0.588 -0.635
#> # … with 5,017 more rows, and 3 more variables: GOV <dbl>, OTH <dbl>, SUM <dbl>
#> 
#> Grouped by:  Variable, Country  [85 | 59 (7.7)]
```
