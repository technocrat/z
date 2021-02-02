---
date: 2021-02-02T02:23
---

# weekday labels

[[R]]
[[snips]]
[[[lubridate]]]

``` r
#zetted
library(lubridate)
#> 
#> Attaching package: 'lubridate'
#> The following objects are masked from 'package:base':
#> 
#>     date, intersect, setdiff, union

seq(c(ISOdate(2000,3,19)), by = "day", length.out = 7) -> the_days

wday(the_days)
#> [1] 1 2 3 4 5 6 7
wday(the_days, label = TRUE)
#> [1] Sun Mon Tue Wed Thu Fri Sat
#> Levels: Sun < Mon < Tue < Wed < Thu < Fri < Sat
wday(the_days, label = TRUE, abbr = FALSE)
#> [1] Sunday    Monday    Tuesday   Wednesday Thursday  Friday    Saturday 
#> 7 Levels: Sunday < Monday < Tuesday < Wednesday < Thursday < ... < Saturday
# locale argument is OS specific
wday(the_days, label = TRUE, locale = "fr_FR.utf8")
#> [1] dim\\. lun\\. mar\\. mer\\. jeu\\. ven\\. sam\\.
#> Levels: dim\\. < lun\\. < mar\\. < mer\\. < jeu\\. < ven\\. < sam\\.
wday(the_days, label = TRUE, abbr = FALSE, locale = "fr_FR.utf8")
#> [1] dimanche lundi    mardi    mercredi jeudi    vendredi samedi  
#> 7 Levels: dimanche < lundi < mardi < mercredi < jeudi < ... < samedi
```
