---
date: 2020-12-31T02:57
---

# regex

	singleton <- "(^\\d{1}$)"
    [[:digit:]]
    [[foo]
    

    s <- "here is a <em>tagged</em> string"
    gsub(pattern = "<.*>", replacement = "", x=s)  #greedy defalt
    #> [1] "here is a  string"
    gsub(pattern = "<.*?>", replacement = "", x=s) #lazy flab
    #> [1] "here is a tagged string"




[[R]]
[[[snips]]]