---
date: 2020-10-18
---

# pairwise
    
    is_even <- function(x) x%%2 == 0
    is_hit  <- function(x) is_even(x[1]) & !is_even(x[2]) | !is_even(x[1]) & is_even(x[2])
    gen_data <- function(x) sample(seq(from = 1, to = x),replace = TRUE)
    mk_pairs <- function(x) split(x, ceiling(seq_along(x)/2))
    prepare <- function(x) mk_pairs(gen_data(x))
    exchange <- function(x) if(is_hit(x)) rev(x) else x
    swap <- function(x) unlist(lapply(prepare(x), exchange), recursive = FALSE, use.names = FALSE)
    
    # MAIN
    
    set.seed(137)
    swap(100)
    set.seed(137)
    unlist(prepare(100), recursive = FALSE, use.names = FALSE)

[[[R]]]
[[[snips]]]
