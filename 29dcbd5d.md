---
date: 2020-12-29T18:10
---

# factory

		power1 <- function(exp) {
			function(x) {
				x ^ exp
			}
		}

		square <- power1(2)
		cube <- power1(3)

[[R]]
[[[snips]]]