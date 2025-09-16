STAT 545A Troubleshooting Exercise for Milestone 1
================

There are **3 code chunks with errors** in this Rmd. Your objective is
to fix all of the errors in this worksheet. Make sure to indicate what
lines you changed and why (by commenting \# in the code).

For the purpose of grading, each erroneous code chunk is equally
weighted.

## Welcome to R and Rmd!

This document is written in **R Markdown**. We’ll use this document to
explore the `mtcars` dataset.

First, let’s store the current date as a variable. We can use the
function `Sys.Date` with no arguments to get the current date:

``` r
## ERROR 1 ##
_today_ <- Sys.Date()
```

    ## Error in parse(text = input): <text>:2:2: unexpected symbol
    ## 1: ## ERROR 1 ##
    ## 2: _today_
    ##     ^

You may notice that, although an error might appear in these cells, this
Rmd file knits just fine. That’s because the `error = TRUE` *chunk
option* is included in each chunk, allowing the Rmd file to knit, even
when an error is encountered.

Now, let’s load the `tidyverse` (meta-) package:

``` r
## ERROR 2 ##
libraries(tidyverse)
```

    ## Error in libraries(tidyverse): could not find function "libraries"

By loading the tidyverse, a function called `glimpse` has been made
available. This function is useful for viewing a data set. Let’s take a
look at the `mtcars` dataset by applying the `glimpse` function to
`mtcars`!

``` r
## ERROR 3 ##
glimpse mtcars
```

    ## Error in parse(text = input): <text>:2:9: unexpected symbol
    ## 1: ## ERROR 3 ##
    ## 2: glimpse mtcars
    ##            ^

## Attribution

Thanks to Icíar Fernández Boyano for coming up with most of this
worksheet.
