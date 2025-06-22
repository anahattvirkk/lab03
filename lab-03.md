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

``` r
nobel_living <- nobel_living %>%
  mutate(country_us = if_else(country == "USA", "USA", "Other"))

nobel_living_science <- nobel_living %>%
  filter(category %in% c("Physics", "Medicine", "Chemistry", "Economics"))

ggplot(nobel_living_science, aes(y = country_us)) +
  geom_bar() + 
  facet_wrap(~category) + 
  labs(title = "Nobel Prize Laureates by Category and Country", x = "Laureate Count", y ="Country")
```

![](lab-03_files/figure-gfm/USA-laureates-1.png)<!-- -->

From the graphs above, it can be seen that Buzzfeed’s headline is
supported by the data as the US has the most amount of laureates for
each scientific category.

### Exercise 4

``` r
nobel_living_science <- nobel_living_science %>%
  mutate(born_country_us = if_else(born_country == "USA", "USA", "Other"))
```

There are 105 Nobel laureates born in the US.

### Exercise 5

``` r
ggplot(nobel_living_science, aes(y = country_us, fill = born_country_us)) +
  geom_bar(position = "stack") + 
  facet_wrap(~category) + 
  labs(title = "Nobel Prize Laureates by Category and Country", x = "Laureate Count", y ="Country", fill = "Birth Country")
```

![](lab-03_files/figure-gfm/US-born-1.png)<!-- -->

Based on these graphs, the data supports Buzzfeed’s claim that many US
laureates were born in other countries.

### Exercise 6

``` r
nobel_living_science %>%
  filter(country == "USA", born_country_us == "Other") %>%
  count(born_country) %>%
  arrange(desc(n))
```

    ## # A tibble: 21 × 2
    ##    born_country       n
    ##    <chr>          <int>
    ##  1 Germany            7
    ##  2 United Kingdom     7
    ##  3 China              5
    ##  4 Canada             4
    ##  5 Japan              3
    ##  6 Australia          2
    ##  7 Israel             2
    ##  8 Norway             2
    ##  9 Austria            1
    ## 10 Finland            1
    ## # ℹ 11 more rows

From the data above, the country that is most common is Germany.
