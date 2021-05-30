---
date: 2021-05-29T22:28
---

# Convert data frame with lat lng to simple features sf object

[[[sf]]]
[[GIS]]

``` r
suppressPackageStartupMessages({
  library(dplyr)
  library(sf)
})

all_trips <- data.frame(
  ride_id =c("89E7AA6C29227EFF", "0FEFDE2603568365", "E6159D746B2DBB91", "B32D3199F1C2E75B", "83E463F23575F4BF", "BDAA7E3494E8D545"),
  rideable_type = c("classic_bike", "classic_bike", "electric_bike", "classic_bike", "electric_bike", "electric_bike"),
  started_at = c("2021-02-12 16:14:56", "2021-02-14 17:52:38", "2021-02-09 19:10:18", "2021-02-02 17:49:41", "2021-02-23 15:07:23", "2021-02-24 15:43:33"),
  ended_at = c("2021-02-12 16:21:43", "2021-02-14 18:12:09", "2021-02-09 19:19:10", "2021-02-02 17:54:06", "2021-02-23 15:22:37", "2021-02-24 15:49:05"),
  start_station_name = c("Glenwood Ave & Touhy Ave", "Glenwood Ave & Touhy Ave", "Clark St & Lake St", "Wood St & Chicago Ave", "State St & 33rd St", "Fairbanks St & Superior St"),
  start_station_id = c("525", "525", "KA1503000012", "637", "13216", "18003"),
  end_station_name = c("Sheridan Rd & Columbia Ave", "Bosworth Ave & Howard St", "State St & Randolph St", "Honore St & Division St", "Emerald Ave & 31st St", "LaSalle Dr & Huron St"),
  end_station_id = c("660", "16806", "TA1305000029", "TA1305000034", "TA1309000055", "KP1705001026"),
  start_lat = c(42.012701, 42.012701, 41.88579467, 41.895634, 41.8347335, 41.89580767),
  start_lng = c(-87.666058, -87.666058, -87.63110067, -87.672069, -87.6258275, -87.62025317),
  end_lat = c(42.004583, 42.019537, 41.884866, 41.903119, 41.83816333, 41.89488583),
  end_lng = c(-87.661406, -87.669563, -87.62749767, -87.673935, -87.6451235, -87.63197917),
  member_casual = c("member", "casual", "member", "member", "member", "casual"), distance = structure(c(980.592826277737, 812.908380101462, 316.336005494772, 845.665751357776, 1647.42627713684, 978.470177223537)))


starts <- tibble(pnt = "start",
                 lat = all_trips$start_lat,
                 lon = all_trips$start_lng)
                    
ends <- tibble(pnt = "end",
                 lat = all_trips$end_lat,
                 lon = all_trips$end_lng)

start_sf <- st_as_sf(starts, coords = c('lon','lat'))
end_sf   <- st_as_sf(ends,   coords = c('lon','lat'))
st_crs(start_sf) = 4326
st_crs(end_sf) = 4326

distances <- st_distance(start_sf,end_sf, by_element = TRUE)

all_trips["distance"] <- distances

all_trips
#>            ride_id rideable_type          started_at            ended_at
#> 1 89E7AA6C29227EFF  classic_bike 2021-02-12 16:14:56 2021-02-12 16:21:43
#> 2 0FEFDE2603568365  classic_bike 2021-02-14 17:52:38 2021-02-14 18:12:09
#> 3 E6159D746B2DBB91 electric_bike 2021-02-09 19:10:18 2021-02-09 19:19:10
#> 4 B32D3199F1C2E75B  classic_bike 2021-02-02 17:49:41 2021-02-02 17:54:06
#> 5 83E463F23575F4BF electric_bike 2021-02-23 15:07:23 2021-02-23 15:22:37
#> 6 BDAA7E3494E8D545 electric_bike 2021-02-24 15:43:33 2021-02-24 15:49:05
#>           start_station_name start_station_id           end_station_name
#> 1   Glenwood Ave & Touhy Ave              525 Sheridan Rd & Columbia Ave
#> 2   Glenwood Ave & Touhy Ave              525   Bosworth Ave & Howard St
#> 3         Clark St & Lake St     KA1503000012     State St & Randolph St
#> 4      Wood St & Chicago Ave              637    Honore St & Division St
#> 5         State St & 33rd St            13216      Emerald Ave & 31st St
#> 6 Fairbanks St & Superior St            18003      LaSalle Dr & Huron St
#>   end_station_id start_lat start_lng  end_lat   end_lng member_casual
#> 1            660  42.01270 -87.66606 42.00458 -87.66141        member
#> 2          16806  42.01270 -87.66606 42.01954 -87.66956        casual
#> 3   TA1305000029  41.88579 -87.63110 41.88487 -87.62750        member
#> 4   TA1305000034  41.89563 -87.67207 41.90312 -87.67394        member
#> 5   TA1309000055  41.83473 -87.62583 41.83816 -87.64512        member
#> 6   KP1705001026  41.89581 -87.62025 41.89489 -87.63198        casual
#>        distance
#> 1  980.5928 [m]
#> 2  812.9084 [m]
#> 3  316.3360 [m]
#> 4  845.6658 [m]
#> 5 1647.4263 [m]
#> 6  978.4702 [m]
```
