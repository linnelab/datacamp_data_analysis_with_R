# Lesson 2 : Introduction to the Tidyverse

## 2-3 & 3-2. Aggregating data
* __Count data__ :
  * use verb **`count(column_name1, wt = column_name2, sort = TRUE)`** function.
    * you can add this argument
      * **column_name1** : count this column.
      * **wt** : "weight", it will according to column_name1 to calculate the number of column_name2.
      * **sort** : If TRUE, it will sort in descending order for the count column result.
      
  * 📝 **example 1** : 
    ```
    # Loading package
    library(dplyr) %>%
    
    # Find the number of counties in each region
    counties %>%
        count(region, sort = TRUE)
    ```
    
  * 🔎 **result 1** :
    ```
    # A tibble: 4 x 2
      region            n
      <chr>         <int>
    1 South          1420
    2 North Central  1054
    3 West            447
    4 Northeast       217
    ```
    
  * 📝 **example 2** : 
    ```
    # Loading package
    library(dplyr)
    
    # Find the number of population_walk in each state
    ## step 1- add population_walk containing the total number of people who walk to work   
    ## step 2 - count weighted by the new column, and sort in descending order.
    counties %>%
        mutate(population_walk = population * walk / 100) %>%    
        count(state, wt = population_walk, sort = TRUE)
    ```
    
  * 🔎 **result 2** :
    ```
     # A tibble: 50 x 2
       state            n
       <chr>          <dbl>
     1 New York       1237938.
     2 California     1017964.
     3 Pennsylvania   505397.
     4 Texas          430783.
     5 Illinois       400346.
     6 Massachusetts  316765.
     7 Florida        284723.
     8 New Jersey     273047.
     9 Ohio           266911.
    10 Washington     239764.
    # ... with 40 more rows
    ```

* __Summarize data__ :
  * use verb **`summarize()`** function.
  * you can use these functions for summarizing :
    * **mean()** : the sum of the values / the number of values.
    * **sum()** 
    * **median()** : the middle most value in a data series is called the median.
    * **max()** 
    * **min()**
    * **n()** : calculate row count, equal count() function. 
  * 📝 **example** : 
    ```
    # Loading package
    library(gapminder)
    library(dplyr)
    
    # Filter for 1957 then summarize the median life expectancy and the maximum GDP per capita
    gapminder %>%
        filter(year == 1957) %>%
        summarize(medianLifeExp = median(lifeExp), maxGdpPerCap = max(gdpPercap))
    ```
  * 🔎 **result** :
    ```
    # A tibble: 1 × 2
      medianLifeExp  maxGdpPerCap
              <dbl>         <dbl>
    1          48.4       113523.
    ```
* __Group by data__ :
  * use verb **`group_by()`** funciton.
  * 📝 **example** : 
    ```
    # Loading package
    library(gapminder)
    library(dplyr)
    
    # Find median life expectancy and maximum GDP per capita in each continent/year combination
    gapminder %>%
        group_by(continent, year) %>%
        summarize(medianLifeExp = median(lifeExp), maxGdpPerCap = max(gdpPercap))
    ```
  * 🔎 **result** :
    ```
    # A tibble: 60 × 4
    # Groups:   continent [5]
       continent  year medianLifeExp maxGdpPerCap
       <fct>     <int>         <dbl>        <dbl>
     1 Africa     1952          38.8        4725.
     2 Africa     1957          40.6        5487.
     3 Africa     1962          42.6        6757.
     4 Africa     1967          44.7       18773.
     5 Africa     1972          47.0       21011.
     6 Africa     1977          49.3       21951.
     7 Africa     1982          50.8       17364.
     8 Africa     1987          51.6       11864.
     9 Africa     1992          52.4       13522.
    10 Africa     1997          52.8       14723.
    # … with 50 more rows
    ```
* __Visualizing summarized data__ :
  * If you want to specify the **y-axis to start at zero**, you can add **`expand_limits(y = 0)`** to the end of the ggplot() function.
  * 📝 **example** : 
    ```
    # Loading package
    library(gapminder)
    library(dplyr)
    library(ggplot2)
    
    # Summarize the median GDP and median life expectancy per continent in 2007
    by_continent_2007 <- gapminder %>%
        filter(year == 2007) %>%
        group_by(continent) %>%
        summarize(meidanGdpPerCap = median(gdpPercap), medianLifeExp = median(lifeExp))

    # Use a scatter plot to compare the median GDP and median life expectancy
    ggplot(by_continent_2007, aes(x = meidanGdpPerCap, y = medianLifeExp, color = continent)) +
        geom_point() +
        expand_limits(y = 0)
    ```
  * 🔎 **result** :
    ![image](https://user-images.githubusercontent.com/15766139/185286125-c4d0f4a5-4183-44e3-9cf1-270f277eebe9.png)
