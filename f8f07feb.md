---
date: 2021-07-30T16:33
---

# save objects

[[[snips]]]
[[R]]


    df1 <- data.frame()
    df2 <- data.frame()
    df3 <- data.frame()
    frames <- ls(pattern = "df.")
    dfiles <- list()
    for (i in seq_along(frames)) {
      dfiles[i] = paste0("data_",
                  frames[i],
                  "_",gsub("-","",Sys.Date()),
                  ".csv")
    }
    # iterate along dfiles to save   
