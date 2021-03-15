---
date: 2021-03-15T01:21
---

# simple write to file

[[[snips]]]
[[R]]

    fileConn<-file("output.txt")
    writeLines(c("Hello","World"), fileConn)
    close(fileConn)