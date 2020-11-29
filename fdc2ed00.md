---
date: 2020-11-28T02:34
---

# remove NAs

	rm_na <- function(x) {
	  x <- x[complete.cases(x),]
	}
    
[[[R]]]