---
date: 2020-12-31T01:19
---

# defactor
		cdefactor <- function(x) {as.character(levels(x))[x]}
		ndefactor <- function(x) as.numeric(levels(x))[x]
        
        murders %>% mutate_if(is.factor, as.character)
        
[[[R]]]
[[snips]]