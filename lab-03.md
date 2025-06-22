Lab 03 - Nobel laureates
================
Anahatt Virk
06/21/2025

### Load packages and data

``` r
library(tidyverse) 
```

``` r
nobel <- read_csv("data/nobel.csv")
```

## Exercises

### Exercise 1

``` r
nobel <- read_csv("data/nobel.csv")
```

    ## Rows: 935 Columns: 26
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (21): firstname, surname, category, affiliation, city, country, gender,...
    ## dbl   (3): id, year, share
    ## date  (2): born_date, died_date
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

The dataset contains 935 observations and 26 variables. Each row
contains the information for a Nobel Prize awarded to one laureate.
Details such as the recipient’s name, gender, and year recieved are
present in each row.

### Exercise 2

``` r
nobel_living <- nobel %>%
  filter(is.na(died_date), !is.na(country), gender !="org")
```

This data frame contains 228 observations.

### Exercise 3

Remove this text, and add your answer for Exercise 1 here. Add code
chunks as needed. Don’t forget to label your code chunk. Do not use
spaces in code chunk labels.

### Exercise 4

…

### Exercise 5

…

### Exercise 6

…
