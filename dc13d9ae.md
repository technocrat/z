---
date: 2021-02-06T01:44
---

# configuration

[[[R]]]

**.Rprofile** files are user-controllable files to set options and environment variables. .Rprofile files can be either at the user or project level. User-level .Rprofile files live in the base of the user's home directory, and project-level .Rprofile files live in the base of the project directory. 

R will source only one .Rprofile file. So if you have both a project-specific .Rprofile file and a user .Rprofile file that you want to use, you explicitly source the user-level .Rprofile at the top of your project-level .Rprofile with source("~/.Rprofile").

.Rprofile files are sourced as regular R code, so setting environment variables must be done inside a Sys.setenv(key = "value") call. 

One *easy way to edit* your .Rprofile file is to use the usethis::edit_r_profile() function from within an R session. You can specify whether you want to edit the user or project level

.**Renviron** is a user-controllable file that can be used to create environment variables. This is especially useful to avoid including credentials like API keys inside R scripts. This file is written in a key-value format, so environment variables are created in the format:

    Key1=value1
    Key2=value2
    ...

And then Sys.getenv("Key1") will return "value1" in an R session.

Like with the .Rprofile file, .Renviron files can be at either the user or project level. If there is a project-level .Renviron, the user-level file will not be sourced. The usethis package includes a helper function for editing .Renviron files from an R session with usethis::edit_r_environ().



