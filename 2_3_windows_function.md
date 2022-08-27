# Lesson 2 : Introduction to the Tidyverse and dplyr

## 2-3. Windows Function

* __Compare consecutive steps__ :
  * use verb **`lag()`** function.
  * For example :
    ```
    # create a vector
    v <- c(1, 3, 6, 14)
    
    # print out these vector
    v
    
    # print out lag vector result
    lag(v)
    
    # get each value once we've subtracted the previous one
    v - lag(v)
    ```
  * Result :
    ```
    # v
    1   3  6  14
    
    # lag(v)
    NA  1  3  6
    
    # v - lag(v)
    NA  2  3  8
    ```
  * 📝 **example** : 
    ```
    library(dplyr)

    babynames_fraction <- babynames %>%
      group_by(year) %>%
      mutate(year_total = sum(number)) %>%
      ungroup() %>%
      mutate(fraction = number / year_total)


    babynames_fraction %>%
      arrange(name, year) %>%
      mutate(difference = fraction - lag(fraction)) %>%
      group_by(name) %>%
      arrange(desc(difference))
    ```
  * 🔎 **result** :
    ```
    # A tibble: 332,595 × 6
    # Groups:   name [48,040]
        year name    number year_total fraction difference
       <dbl> <chr>    <int>      <int>    <dbl>      <dbl>
     1  1880 John      9701     201478   0.0481     0.0481
     2  1880 William   9562     201478   0.0475     0.0475
     3  1880 Mary      7092     201478   0.0352     0.0352
     4  1880 James     5949     201478   0.0295     0.0295
     5  1880 Charles   5359     201478   0.0266     0.0266
     6  1880 George    5152     201478   0.0256     0.0256
     7  1880 Frank     3255     201478   0.0162     0.0162
     8  1935 Shirley  42790    2088487   0.0205     0.0137
     9  1880 Joseph    2642     201478   0.0131     0.0131
    10  1880 Anna      2616     201478   0.0130     0.0129
    # … with 332,585 more rows
    ```
