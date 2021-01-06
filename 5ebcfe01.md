---
date: 2021-01-01T18:05
---

# control order of factors

    mons = c("March","April","January","November","January",
     "September","October","September","November","August",
     "January","November","November","February","May","August",
     "July","December","August","August","September","November",
     "February","April")
     mons = factor(mons)
     table(mons)

    mons
        April    August  December  February   January      July
            2         4         1         2         3         1
        March       May  November   October September
            1         1         5         1         3

Although the months clearly have an ordering, this is not reflected in the output of the table function. Additionally, comparison operators are not supported for unordered factors. Creating an ordered factor solves these problems:

      mons = factor(mons,levels=c("January","February","March", 
     "April","May","June","July","August","September",
     "October","November","December"),ordered=TRUE)
      mons[1] < mons[2]
      [1] TRUE
      table(mons)
      mons
      January  February     March     April       May      June
          3         2         1         2         1         0
       July    August September   October  November  December
          1         4         3         1         5         1
		
[source](https://goo.gl/dyCyWn)
        
[[R]]
[[[snips]]]

