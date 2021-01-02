---
date: 2021-01-02T14:20
---

# ls list files with grep

    ls	list.files()	Lists all the files in a directory
    ls -R	list.files(recursive = TRUE)	Recursively lists all the files in a directory and all sub-directories
    ls | grep “something”	list.files(pattern = “something”)	Lists all the files in a directory containing the regex “something”
    
[[R]]
[[[snips]]]
[[bash]]