Netflix
================
Fanyi Zeng
2022-05-03

``` r
netflix_titles <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-04-20/netflix_titles.csv')
```

    ## Rows: 7787 Columns: 12

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr (11): show_id, type, title, director, cast, country, date_added, rating,...
    ## dbl  (1): release_year

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.6     v dplyr   1.0.7
    ## v tidyr   1.1.4     v stringr 1.4.0
    ## v readr   2.1.1     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

Let’s take a look at the trend of movies and tv shows. We can see that
both movies and TV shows are increasing. Since 2020, however, there is a
sudden drop in production due to the COVID pandemic.

``` r
netflix_titles %>%
  ggplot(aes(x=release_year, fill=type)) +
  geom_bar()
```

![](Netflix_files/figure-gfm/trend-1.png)<!-- -->

Although historically movies have been more dominant than TV shows, in
recent years Netflix seems to focus more on TV shows.

``` r
netflix_titles %>%
  filter(release_year >= 1975) %>%
  ggplot(aes(y=release_year, fill=type)) +
  geom_bar(position="fill")
```

![](Netflix_files/figure-gfm/year-1.png)<!-- -->

What are the most prolific countries? Below are the top 10.

``` r
Top10 <- netflix_titles %>%
  filter(country!="NA") %>%
  count(country) %>%
  arrange(desc(n)) %>%
  slice(1:10) 
Top10 %>%
  ggplot(aes(x=reorder(country,-n),y=n,fill=country)) +
  geom_col() +
  labs(x="country",y="production")
```

![](Netflix_files/figure-gfm/country-1.png)<!-- -->
