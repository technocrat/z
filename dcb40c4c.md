---
date: 2020-12-31T19:56
---

# waldo object diff

    library(waldo)
    # addition
    compare(c("a", "b", "c"), c("a", "b"))

    #> `old`: "a" "b" "c"
    #> `new`: "a" "b"


    # deletion
    compare(c("a", "b"), c("a", "b", "c"))

    #> `old`: "a" "b"    
    #> `new`: "a" "b" "c"


    # modification
    compare(c("a", "b", "c"), c("a", "B", "c"))

    #> `old`: "a" "b" "c"
    #> `new`: "a" "B" "c"
