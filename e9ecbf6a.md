---
date: 2020-12-29T17:20
---

# Permutation of n items

		library(combinat)

		v = letters[1:3]

		# Returns a list
		permn(v)

		# If you want a matrix
		do.call("rbind", permn(v))

[[[R]]]
[[snips]]