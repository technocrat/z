---
date: 2021-01-02T17:10
---

# format every other row as percentage

[[[snips]]]
[[R]]

    ctab <- function(tab, dec = 2, ...) {
      tab <- as.table(tab)
      ptab <- paste(round(prop.table(tab) * 100, dec), "%", sep = "")
      res <- matrix(NA, nrow = nrow(tab) * 2, ncol = ncol(tab), byrow = TRUE)
      oddr <- 1:nrow(tab) %% 2 == 1
      evenr <- 1:nrow(tab) %% 2 == 0
      res[oddr, ] <- tab
      res[evenr, ] <- ptab
      res <- as.table(res)
      colnames(res) <- colnames(tab)
      rownames(res) <- rep(rownames(tab), each = 2)
      return(res)
    }
    HairEyeColor

    tb <- HairEyeColor[, , 1]
    tb
    ctab(tb)

  
[source](http://bit.ly/1N0FI24)