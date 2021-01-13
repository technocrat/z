---
date: 2021-01-12T02:25
---

# gannt

[[[VIZ]]]
[[script]]
[[R]]

[source](https://community.rstudio.com/t/graphing-attendance-at-event-with-join-and-leave-times/92870/2)

``` r
library(tidyverse)

data <- structure(list(
  Email = c(
    "email1@gmail.com", "email2@gmail.com", "email3@gmail.com",
    "email4@gmail.com", "email5@gmail.com"
  ), Join.Time = structure(c(
    as.POSIXct("2020-12-09 13:04:00"),
    as.POSIXct("2020-12-09 13:20:00"), as.POSIXct("2020-12-09 13:30:00"), as.POSIXct("2020-12-09 13:07:00"),
    as.POSIXct("2020-12-09 13:29:00")
  ), class = c("POSIXct", "POSIXt"), tzone = "America/New_York"),
  Leave.Time = structure(c(
    as.POSIXct("2020-12-09 13:25:00"), as.POSIXct("2020-12-09 13:22:00"),
    as.POSIXct("2020-12-09 14:01:00"), as.POSIXct("2020-12-09 13:29:00"), as.POSIXct("2020-12-09 14:33:00")
  ),
  class = c("POSIXct", "POSIXt"), tzone = "America/New_York"
  )
),
.Names = c("Email", "Join.Time", "Leave.Time"),
row.names = c(NA, -5L), class = "data.frame"
) %>%
  as_tibble()


data %>%
  ggplot(aes(y = Email, color = Email)) +
  geom_point(aes(x = Join.Time), size = 3) +
  geom_point(aes(x = Leave.Time), size = 3) +
  geom_segment(aes(
    x = Join.Time, xend = Leave.Time,
    y = Email, yend = Email
  ), size = 1) +
  labs(x = "Time", y = "") +
  theme_light() +
  theme(
    text = element_text(size = 14),
    legend.position = "none"
  )
```

![](https://i.imgur.com/YHVUfs3.png)

	suppressPackageStartupMessages({
      library(vistime)
    })
    
    DF <- data.frame(
      Event = c(1,1,1,1,1),
      Email = c(
        "email1@gmail.com", "email2@gmail.com", "email2@gmail.com",
        "email3@gmail.com", "email3@gmail.com"
      ), 
      Join.Time = c(
        as.POSIXct("2020-12-09 13:04:00"),
        as.POSIXct("2020-12-09 13:20:00"), 
        as.POSIXct("2020-12-09 13:30:00"),
        as.POSIXct("2020-12-09 13:07:00"),
        as.POSIXct("2020-12-09 13:29:00")),
      Leave.Time =c(
        as.POSIXct("2020-12-09 13:25:00"),
        as.POSIXct("2020-12-09 13:22:00"),
        as.POSIXct("2020-12-09 14:01:00"), 
        as.POSIXct("2020-12-09 13:29:00"), 
        as.POSIXct("2020-12-09 14:33:00")))
    
    DF
    
    vistime(DF,
      col.event = "Event", 
      col.start = "Join.Time", 
      col.end = "Leave.Time", 
      col.group = "Email")
