---
date: 2021-02-06T16:28
---

# group observations by time interval

[[[script]]]
[[R]]

``` r
suppressPackageStartupMessages({
  library(dplyr)
  library(magrittr)
})

date_time <- c(
  "Jan 29 2020 13:46:08",
  "Jan 29 2020 13:42:53",
  "Jan 29 2020 12:13:27",
  "Jan 29 2020 12:11:19",
  "Jan 29 2020 12:09:21",
  "Jan 28 2020 12:22:26",
  "Jan 27 2020 8:22:20",
  "Jan 25 2020 14:34:22",
  "Jan 25 2020 14:31:13",
  "Jan 23 2020 12:16:16",
  "Jan 23 2020 12:13:30",
  "Jan 20 2020 12:12:59",
  "Jan 20 2020 12:05:30",
  "Jan 20 2020 12:01:54"
)

systol <- c(
  132, 132, 118, 115, 110, 148, 120,
  115, 117, 134, 136, 131, 132, 137
)

# df and data are also names of built-in functions
# usually, other objects of the same names peacefully
# co-exist, but there are some operations in which
# the built-in takes precedence, so I avoid 

DF <- data.frame(date_time, systol) %>%
  mutate(dtetime = lubridate::mdy_hms(date_time)) %>%
  arrange(dtetime)

# creates difftime object; no provision for DST

DF %<>% mutate(hiatus = dtetime - lag(dtetime,1))

# create a plug value for first row's hiatus

DF[1,4] <- (DF[2,4] - DF[2,4])

# identifiers for grouping, extend as needed

grp <- c(LETTERS,c(paste(LETTERS,LETTERS,sep = "")))

# codes whether a new group is starting and assign a group number

DF %<>% mutate(newone = ifelse(hiatus <= 10,0,1))
DF %<>% mutate(thegrp = cumsum(newone))

# assign a group name

DF %<>% mutate(thegrp = case_when(
              thegrp == 0 ~ grp[1],
              thegrp == 1 ~ grp[2],
              thegrp == 2 ~ grp[3],
              thegrp == 3 ~ grp[4],
              thegrp == 4 ~ grp[5],
              thegrp == 5 ~ grp[6],
              thegrp == 6 ~ grp[7]
              ))
# cleanup

DF %<>% select(dtetime,systol,thegrp)

# group and summarize
DF %>% 
  group_by(thegrp) %>%
  summarize(meansys = mean(systol))
#> # A tibble: 7 x 2
#>   thegrp meansys
#> * <chr>    <dbl>
#> 1 A         133.
#> 2 B         135 
#> 3 C         116 
#> 4 D         120 
#> 5 E         148 
#> 6 F         114.
#> 7 G         132
```
