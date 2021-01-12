---
date: 2021-01-12T02:25
---

# gannt

[[[VIZ]]]
[[script]]
[[R]]

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
