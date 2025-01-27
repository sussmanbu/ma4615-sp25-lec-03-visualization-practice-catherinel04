# Week 02: COVID Visualization Activity
**`[[`**Your Name**`]]`**

Today, we’ll be working with a data set related to COVID. This data is
based on data from the the [COVID Tracking
Project](https://covidtracking.com/). I cleaned up this data and also
added total populations from the 2020 for each of the relevant
categories. Note, due to differences in the way race and ethnicity are
encoded in the census as compared to the the COVID Tracking Project, the
population counts for LatinX may be somewhat inaccurate.

``` r
library(tidyverse)
```

    ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ✔ purrr     1.0.2     
    ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()
    ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
load("CRDT Data.RData")
ls()
```

    [1] "covid_data_count"  "covid_data_long"   "covid_data_orig"  
    [4] "covid_data_race"   "covid_data_simple"

I’ve include 4 different data sets. They all have the same data but have
it represented in different ways. Try using the different data sets and
see which ones are good for making which plots.

``` r
ggplot(covid_data_count, aes(x = date, y = Cases)) + geom_point()
```

    Warning: Removed 1385 rows containing missing values or values outside the scale range
    (`geom_point()`).

![](lecture-03-covid-vis_files/figure-commonmark/first_plot-1.png)

If you want to only look at a specific state, you can do it like this.
For now, see what you can do just using `ggplot`.

``` r
covid_data_count |> 
  filter(state %in% c("MA", "MD")) |> 
  ggplot(aes(x = date, y = Cases, color = race)) + geom_line()
```

![](lecture-03-covid-vis_files/figure-commonmark/unnamed-chunk-1-1.png)

``` r
ggplot(covid_data_count, aes(x = state_name, y = Cases/population)) + geom_bar(stat = "identity", fill = "pink") + theme(axis.text.x = element_text(angle = 60, hjust = 1))
```

    Warning: Removed 1385 rows containing missing values or values outside the scale range
    (`geom_bar()`).

![](lecture-03-covid-vis_files/figure-commonmark/unnamed-chunk-2-1.png)

``` r
ggplot(covid_data_count, aes(x = date)) +
  geom_line(aes(y = Cases, color = "Cases")) +
  geom_line(aes(y = Deaths, color = "Deaths")) +
  scale_color_manual(values = c("Cases" = "blue", "Deaths" = "red"))
```

    Warning: Removed 13 rows containing missing values or values outside the scale range
    (`geom_line()`).

![](lecture-03-covid-vis_files/figure-commonmark/unnamed-chunk-3-1.png)

1.  After making and refining some plots, pick one and save the code and
    describe what you observe? I made a plot for stat vs the percentage
    of cases to population. I noticed from this is that lousiana, utahm
    and south dakota had the highest cases to population ratio whereas
    even for states like cali which have the most cases actually have a
    generally pretty low case to population ratio.

2.  What conclusions can you draw? Population isnt the sole factor in
    determining case to population ratio and perhaps theres ia
    correlation between prevention efforts and ratio more.

3.  What were you not able to do due to not having the coding knowledge?
    I wasnt able to filter out the states to only show the top 10 states
    instead of all 50.

4.  What made previous plots you made hard to interpret/understand? What
    did you do to improve/change them to ease interpretation? I played
    around the orientation of the axes for the ones where I plotted
    state names so that I could read the state names. I rotated the
    names.

5.  What other data would be useful to better understand this data? It
    would be nice to see factors like education levels, or vaccine
    rates.
