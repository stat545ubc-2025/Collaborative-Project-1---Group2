Team Troubleshooting Deliverable 2
================

\<\<\<\<\<\<\< HEAD \>\>\>\>\>\>\>
86450465753fb8614ac54a8cf802d27b14f7645f

There are **11 code chunks with errors** in this Rmd. Your objective is
to fix all of the errors in this worksheet. For the purpose of grading,
each erroneous code chunk is equally weighted.

Note that errors are not all syntactic (i.e., broken code)! Some are
logical errors as well (i.e. code that does not do what it was intended
to do).

## Exercise 1: Exploring with `select()` and `filter()`

[MovieLens](https://dl.acm.org/doi/10.1145/2827872) are a series of
datasets widely used in education, that describe movie ratings from the
MovieLens [website](https://movielens.org/). There are several MovieLens
datasets, collected by the [GroupLens Research
Project](https://grouplens.org/datasets/movielens/) at the University of
Minnesota. Here, we load the MovieLens 100K dataset from Rafael Irizarry
and Amy Gill’s R package,
[dslabs](https://cran.r-project.org/web/packages/dslabs/dslabs.pdf),
which contains datasets useful for data analysis practice, homework, and
projects in data science courses and workshops. We’ll also load other
required packages.

``` r
### ERROR HERE ### (Change load.package() to library() by Teng-Wei) and reviewed by Vahid
library(dslabs)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   4.0.0     ✔ tibble    3.3.0
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.1.0     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(stringr)
#install the following tools by deleteing #sign in the following lines
#install.packages("devtools") # Do not run this if you already have this package installed! 
#devtools::install_github("JoeyBernhardt/singer")
library(gapminder)
```

    ## 
    ## Attaching package: 'gapminder'
    ## 
    ## The following object is masked from 'package:dslabs':
    ## 
    ##     gapminder

Let’s have a look at the dataset! My goal is to:

- Find out the “class” of the dataset.
- If it isn’t a tibble already, coerce it into a tibble and store it in
  the variable “movieLens”.
- Have a quick look at the tibble, using a *dplyr function*.

``` r
### ERROR HERE ### (Add Head() function by Teng-Wei) and reviewed by Vahid
class(dslabs::movielens)
```

    ## [1] "data.frame"

``` r
movieLens <- as_tibble(dslabs::movielens)
dim(movieLens)
```

    ## [1] 100004      7

``` r
head(movieLens)
```

    ## # A tibble: 6 × 7
    ##   movieId title                              year genres userId rating timestamp
    ##     <int> <chr>                             <int> <fct>   <int>  <dbl>     <int>
    ## 1      31 Dangerous Minds                    1995 Drama       1    2.5    1.26e9
    ## 2    1029 Dumbo                              1941 Anima…      1    3      1.26e9
    ## 3    1061 Sleepers                           1996 Thril…      1    3      1.26e9
    ## 4    1129 Escape from New York               1981 Actio…      1    2      1.26e9
    ## 5    1172 Cinema Paradiso (Nuovo cinema Pa…  1989 Drama       1    4      1.26e9
    ## 6    1263 Deer Hunter, The                   1978 Drama…      1    2      1.26e9

Now that we’ve had a quick look at the dataset, it would be interesting
to explore the rows (observations) in some more detail. I’d like to
consider the movie entries that…

- belong *exclusively* to the genre *“Drama”*;
- don’t belong *exclusively* to the genre *“Drama”*;
- were filmed *after* the year 2000;
- were filmed in 1999 *or* 2000;
- have *more than* 4.5 stars, and were filmed *before* 1995.

``` r
### ERROR HERE ### (Change month to year by Teng-Wei) and reviewed by Vahid
filter(movieLens, genres == "Drama")
```

    ## # A tibble: 7,757 × 7
    ##    movieId title                             year genres userId rating timestamp
    ##      <int> <chr>                            <int> <fct>   <int>  <dbl>     <int>
    ##  1      31 Dangerous Minds                   1995 Drama       1    2.5    1.26e9
    ##  2    1172 Cinema Paradiso (Nuovo cinema P…  1989 Drama       1    4      1.26e9
    ##  3    1293 Gandhi                            1982 Drama       1    2      1.26e9
    ##  4      62 Mr. Holland's Opus                1995 Drama       2    3      8.35e8
    ##  5     261 Little Women                      1994 Drama       2    4      8.35e8
    ##  6     300 Quiz Show                         1994 Drama       2    3      8.35e8
    ##  7     508 Philadelphia                      1993 Drama       2    4      8.35e8
    ##  8     537 Sirens                            1994 Drama       2    4      8.35e8
    ##  9    2702 Summer of Sam                     1999 Drama       3    3.5    1.30e9
    ## 10    3949 Requiem for a Dream               2000 Drama       3    5      1.30e9
    ## # ℹ 7,747 more rows

``` r
filter(movieLens, !genres == "Drama")
```

    ## # A tibble: 92,247 × 7
    ##    movieId title                            year genres  userId rating timestamp
    ##      <int> <chr>                           <int> <fct>    <int>  <dbl>     <int>
    ##  1    1029 Dumbo                            1941 Animat…      1    3      1.26e9
    ##  2    1061 Sleepers                         1996 Thrill…      1    3      1.26e9
    ##  3    1129 Escape from New York             1981 Action…      1    2      1.26e9
    ##  4    1263 Deer Hunter, The                 1978 Drama|…      1    2      1.26e9
    ##  5    1287 Ben-Hur                          1959 Action…      1    2      1.26e9
    ##  6    1339 Dracula (Bram Stoker's Dracula)  1992 Fantas…      1    3.5    1.26e9
    ##  7    1343 Cape Fear                        1991 Thrill…      1    2      1.26e9
    ##  8    1371 Star Trek: The Motion Picture    1979 Advent…      1    2.5    1.26e9
    ##  9    1405 Beavis and Butt-Head Do America  1996 Advent…      1    1      1.26e9
    ## 10    1953 French Connection, The           1971 Action…      1    4      1.26e9
    ## # ℹ 92,237 more rows

``` r
filter(movieLens, year >= 2000)
```

    ## # A tibble: 29,535 × 7
    ##    movieId title                             year genres userId rating timestamp
    ##      <int> <chr>                            <int> <fct>   <int>  <dbl>     <int>
    ##  1    3510 Frequency                         2000 Drama…      3    4      1.30e9
    ##  2    3949 Requiem for a Dream               2000 Drama       3    5      1.30e9
    ##  3    5349 Spider-Man                        2002 Actio…      3    3      1.30e9
    ##  4    5669 Bowling for Columbine             2002 Docum…      3    3.5    1.30e9
    ##  5    6377 Finding Nemo                      2003 Adven…      3    3      1.30e9
    ##  6    7153 Lord of the Rings: The Return o…  2003 Actio…      3    2.5    1.30e9
    ##  7    7361 Eternal Sunshine of the Spotles…  2004 Drama…      3    3      1.30e9
    ##  8    8622 Fahrenheit 9/11                   2004 Docum…      3    3.5    1.30e9
    ##  9    8636 Spider-Man 2                      2004 Actio…      3    3      1.30e9
    ## 10   27369 Daria: Is It Fall Yet?            2000 Anima…      3    3.5    1.30e9
    ## # ℹ 29,525 more rows

``` r
filter(movieLens, year == 1999 | year == 2000)
```

    ## # A tibble: 9,088 × 7
    ##    movieId title                             year genres userId rating timestamp
    ##      <int> <chr>                            <int> <fct>   <int>  <dbl>     <int>
    ##  1    2694 Big Daddy                         1999 Comedy      3    3      1.30e9
    ##  2    2702 Summer of Sam                     1999 Drama       3    3.5    1.30e9
    ##  3    2762 Sixth Sense, The                  1999 Drama…      3    3.5    1.30e9
    ##  4    2841 Stir of Echoes                    1999 Horro…      3    4      1.30e9
    ##  5    2858 American Beauty                   1999 Drama…      3    4      1.30e9
    ##  6    2959 Fight Club                        1999 Actio…      3    5      1.30e9
    ##  7    3510 Frequency                         2000 Drama…      3    4      1.30e9
    ##  8    3949 Requiem for a Dream               2000 Drama       3    5      1.30e9
    ##  9   27369 Daria: Is It Fall Yet?            2000 Anima…      3    3.5    1.30e9
    ## 10    2628 Star Wars: Episode I - The Phan…  1999 Actio…      4    5      9.50e8
    ## # ℹ 9,078 more rows

``` r
filter(movieLens, rating > 4.5, year < 1995)
```

    ## # A tibble: 8,386 × 7
    ##    movieId title                             year genres userId rating timestamp
    ##      <int> <chr>                            <int> <fct>   <int>  <dbl>     <int>
    ##  1     265 Like Water for Chocolate (Como …  1992 Drama…      2      5    8.35e8
    ##  2     266 Legends of the Fall               1994 Drama…      2      5    8.35e8
    ##  3     551 Nightmare Before Christmas, The   1993 Anima…      2      5    8.35e8
    ##  4     589 Terminator 2: Judgment Day        1991 Actio…      2      5    8.35e8
    ##  5     590 Dances with Wolves                1990 Adven…      2      5    8.35e8
    ##  6     592 Batman                            1989 Actio…      2      5    8.35e8
    ##  7     318 Shawshank Redemption, The         1994 Crime…      3      5    1.30e9
    ##  8     356 Forrest Gump                      1994 Comed…      3      5    1.30e9
    ##  9    1197 Princess Bride, The               1987 Actio…      3      5    1.30e9
    ## 10     260 Star Wars: Episode IV - A New H…  1977 Actio…      4      5    9.50e8
    ## # ℹ 8,376 more rows

While filtering for *all movies that do not belong to the genre drama*
above, I noticed something interesting. I want to filter for the same
thing again, this time selecting variables **title and genres first,**
and then *everything else*. But I want to do this in a robust way, so
that (for example) if I end up changing `movieLens` to contain more or
less columns some time in the future, the code will still work. Hint:
there is a function to select “everything else”…

``` r
### ERROR HERE ### (Substitute year,rating, timestamp by everything() by Teng-Wei)
#and reviewed by Vahid
movieLens %>%
  filter(!genres == "Drama") %>%
  select(title, genres, everything())
```

    ## # A tibble: 92,247 × 7
    ##    title                           genres  movieId  year userId rating timestamp
    ##    <chr>                           <fct>     <int> <int>  <int>  <dbl>     <int>
    ##  1 Dumbo                           Animat…    1029  1941      1    3      1.26e9
    ##  2 Sleepers                        Thrill…    1061  1996      1    3      1.26e9
    ##  3 Escape from New York            Action…    1129  1981      1    2      1.26e9
    ##  4 Deer Hunter, The                Drama|…    1263  1978      1    2      1.26e9
    ##  5 Ben-Hur                         Action…    1287  1959      1    2      1.26e9
    ##  6 Dracula (Bram Stoker's Dracula) Fantas…    1339  1992      1    3.5    1.26e9
    ##  7 Cape Fear                       Thrill…    1343  1991      1    2      1.26e9
    ##  8 Star Trek: The Motion Picture   Advent…    1371  1979      1    2.5    1.26e9
    ##  9 Beavis and Butt-Head Do America Advent…    1405  1996      1    1      1.26e9
    ## 10 French Connection, The          Action…    1953  1971      1    4      1.26e9
    ## # ℹ 92,237 more rows

## Exercise 2: Calculating with `mutate()`-like functions

Some of the variables in the `movieLens` dataset are in *camelCase* (in
fact, *movieLens* is in camelCase). Let’s clean these two variables to
use *snake_case* instead, and assign our post-rename object back to
“movieLens”.

``` r
### ERROR HERE ### changed by Melinda and reviewed by Xu
library(tidyverse)
movieLens <- movieLens %>%
  rename(user_id = userId,
         movie_id = movieId)
# changed "==" to "=" for rename(new_name = old_name)
```

As you already know, `mutate()` defines and inserts new variables into a
tibble. There is *another mystery function similar to `mutate()`* that
adds the new variable, but also drops existing ones. I wanted to create
an `average_rating` column that takes the `mean(rating)` across all
entries, and I only want to see that variable (i.e drop all others!) but
I forgot what that mystery function is. Can you remember?

``` r
### ERROR HERE ### changed by Melinda and reviewed by Xu
transmute(movieLens,
       average_rating = mean(rating,na.rm = TRUE))
```

    ## # A tibble: 100,004 × 1
    ##    average_rating
    ##             <dbl>
    ##  1           3.54
    ##  2           3.54
    ##  3           3.54
    ##  4           3.54
    ##  5           3.54
    ##  6           3.54
    ##  7           3.54
    ##  8           3.54
    ##  9           3.54
    ## 10           3.54
    ## # ℹ 99,994 more rows

``` r
#changed mutate to transmute to add new variable and drops all the others.
```

## Exercise 3: Calculating with `summarise()`-like functions

Alone, `tally()` is a short form of `summarise()`. `count()` is
short-hand for `group_by()` and `tally()`.

Each entry of the movieLens table corresponds to a movie rating by a
user. Therefore, if more than one user rated the same movie, there will
be several entries for the same movie. I want to find out how many times
each movie has been reviewed, or in other words, how many times each
movie title appears in the dataset.

``` r
movieLens %>%
  group_by(title) %>%
  tally()
```

    ## # A tibble: 8,832 × 2
    ##    title                                  n
    ##    <chr>                              <int>
    ##  1 "\"Great Performances\" Cats"          2
    ##  2 "$9.99"                                3
    ##  3 "'Hellboy': The Seeds of Creation"     1
    ##  4 "'Neath the Arizona Skies"             1
    ##  5 "'Round Midnight"                      2
    ##  6 "'Salem's Lot"                         1
    ##  7 "'Til There Was You"                   4
    ##  8 "'burbs, The"                         19
    ##  9 "'night Mother"                        3
    ## 10 "(500) Days of Summer"                45
    ## # ℹ 8,822 more rows

Without using `group_by()`, I want to find out how many movie reviews
there have been for each year.

``` r
### ERROR HERE ### changed by Melinda and reviewed by Xu
movieLens %>%
  count(year)
```

    ## # A tibble: 104 × 2
    ##     year     n
    ##    <int> <int>
    ##  1  1902     6
    ##  2  1915     2
    ##  3  1916     1
    ##  4  1917     2
    ##  5  1918     2
    ##  6  1919     1
    ##  7  1920    15
    ##  8  1921    12
    ##  9  1922    28
    ## 10  1923     3
    ## # ℹ 94 more rows

``` r
#changed tally to count
```

Both `count()` and `tally()` can be grouped by multiple columns. Below,
I want to count the number of movie reviews by title and rating, and
sort the results.

``` r
### ERROR HERE ### changed by Melinda and reviewed by Xu
movieLens %>%
  count(title, rating, sort = TRUE)
```

    ## # A tibble: 28,297 × 3
    ##    title                              rating     n
    ##    <chr>                               <dbl> <int>
    ##  1 Shawshank Redemption, The               5   170
    ##  2 Pulp Fiction                            5   138
    ##  3 Star Wars: Episode IV - A New Hope      5   122
    ##  4 Forrest Gump                            4   113
    ##  5 Schindler's List                        5   109
    ##  6 Godfather, The                          5   107
    ##  7 Forrest Gump                            5   102
    ##  8 Silence of the Lambs, The               4   102
    ##  9 Fargo                                   5   100
    ## 10 Silence of the Lambs, The               5   100
    ## # ℹ 28,287 more rows

``` r
# removed c() from count(c(title, rating), sort = TRUE)
```

Not only do `count()` and `tally()` quickly allow you to count items
within your dataset, `add_tally()` and `add_count()` are handy shortcuts
that add an additional columns to your tibble, rather than collapsing
each group.

## Exercise 4: Calculating with `group_by()`

We can calculate the mean rating by year, and store it in a new column
called `avg_rating`:

``` r
movieLens %>%
  group_by(year) %>%
  summarize(avg_rating = mean(rating))
```

    ## # A tibble: 104 × 2
    ##     year avg_rating
    ##    <int>      <dbl>
    ##  1  1902       4.33
    ##  2  1915       3   
    ##  3  1916       3.5 
    ##  4  1917       4.25
    ##  5  1918       4.25
    ##  6  1919       3   
    ##  7  1920       3.7 
    ##  8  1921       4.42
    ##  9  1922       3.80
    ## 10  1923       4.17
    ## # ℹ 94 more rows

Using `summarize()`, we can find the minimum and the maximum rating by
title, stored under columns named `min_rating`, and `max_rating`,
respectively.

``` r
### ERROR HERE ### 
movieLens %>%
  group_by(title) %>%
  summarize(
    min_rating = min(rating),
    max_rating = max(rating)
  )
```

    ## # A tibble: 8,832 × 3
    ##    title                              min_rating max_rating
    ##    <chr>                                   <dbl>      <dbl>
    ##  1 "\"Great Performances\" Cats"             0.5        3  
    ##  2 "$9.99"                                   2.5        4.5
    ##  3 "'Hellboy': The Seeds of Creation"        2          2  
    ##  4 "'Neath the Arizona Skies"                0.5        0.5
    ##  5 "'Round Midnight"                         0.5        4  
    ##  6 "'Salem's Lot"                            3.5        3.5
    ##  7 "'Til There Was You"                      0.5        4  
    ##  8 "'burbs, The"                             1.5        4.5
    ##  9 "'night Mother"                           5          5  
    ## 10 "(500) Days of Summer"                    0.5        5  
    ## # ℹ 8,822 more rows

``` r
#mutate() works row-by-row, not across groups. 
#To calculate summary min/max per group, we should use summarise() 
#after grouping changed by Xu and reviewed by Teng
```

## Exercise 5: Scoped variants with `across()`

`across()` is a newer dplyr function (`dplyr` 1.0.0) that allows you to
apply a transformation to multiple variables selected with the
`select()` and `rename()` syntax. For this section, we will use the
`starwars` dataset, which is built into R. First, let’s transform it
into a tibble and store it under the variable `starWars`.

``` r
starWars <- as_tibble(starwars)
```

We can find the mean for all columns that are numeric, ignoring the
missing values:

``` r
starWars %>%
  summarise(across(where(is.numeric), function(x) mean(x, na.rm=TRUE)))
```

    ## # A tibble: 1 × 3
    ##   height  mass birth_year
    ##    <dbl> <dbl>      <dbl>
    ## 1   175.  97.3       87.6

We can find the minimum height and mass within each species, ignoring
the missing values:

``` r
### ERROR HERE ### 
starWars %>%
  group_by(species) %>%
  summarise(across(c(height, mass), ~min(.x, na.rm = TRUE)))
```

    ## Warning: There were 6 warnings in `summarise()`.
    ## The first warning was:
    ## ℹ In argument: `across(c(height, mass), ~min(.x, na.rm = TRUE))`.
    ## ℹ In group 4: `species = "Chagrian"`.
    ## Caused by warning in `min()`:
    ## ! no non-missing arguments to min; returning Inf
    ## ℹ Run `dplyr::last_dplyr_warnings()` to see the 5 remaining warnings.

    ## # A tibble: 38 × 3
    ##    species   height  mass
    ##    <chr>      <int> <dbl>
    ##  1 Aleena        79    15
    ##  2 Besalisk     198   102
    ##  3 Cerean       198    82
    ##  4 Chagrian     196   Inf
    ##  5 Clawdite     168    55
    ##  6 Droid         96    32
    ##  7 Dug          112    40
    ##  8 Ewok          88    20
    ##  9 Geonosian    183    80
    ## 10 Gungan       196    66
    ## # ℹ 28 more rows

``` r
#across() takes the first argument as column(s), change to c(height, mass) # changed by Xu and reviewed by Teng
```

Note that here R has taken the convention that the minimum value of a
set of `NA`s is `Inf`.

## Exercise 6: Making tibbles

Manually create a tibble with 4 columns:

- `birth_year` should contain years 1998 to 2005 (inclusive);
- `birth_weight` should take the `birth_year` column, subtract 1995, and
  multiply by 0.45;
- `birth_location` should contain three locations (Liverpool, Seattle,
  and New York).

``` r
### ERROR HERE ### 
fakeStarWars <- tribble(
  ~name,            ~birth_weight,  ~birth_year, ~birth_location      ,
  "Luke Skywalker",  1.35      ,   1998        ,  "Liverpool, England", 
  "C-3PO"         ,  1.80      ,   1999        ,  "Liverpool, England",
  "R2-D2"         ,  2.25      ,   2000        ,  "Seattle, WA",
  "Darth Vader"   ,  2.70      ,   2001        ,  "Liverpool, England",
  "Leia Organa"   ,  3.15      ,   2002        ,  "New York, NY",
  "Owen Lars"     ,  3.60      ,   2003        ,  "Seattle, WA",
  "Beru Whitesun Iars", 4.05   ,   2004        ,  "Liverpool, England",
  "R5-D4"         ,  4.50      ,   2005        ,  "New York, NY",
)

# add a comma after the last column name ~birth_location
# Put strings in quotes "Liverpool, England" instead of Liverpool, England
#changed by Xu and reviewed by Teng
```

## Attributions

Thanks to Icíar Fernández-Boyano for writing most of this document, and
Albina Gibadullina, Diana Lin, Yulia Egorova, and Vincenzo Coia for
their edits.
