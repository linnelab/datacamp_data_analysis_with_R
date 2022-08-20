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
    
* __Summarize data__ :
  * use verb **`summarize()`** function.
  * you can use these functions for summarizing :
    * **mean()** : the sum of the values / the number of values.
    * **sum()** 
    * **median()** : the middle most value in a data series is called the median.
    * **max()** 
    * **min()**
    * **n()** : calculate row count, equal count() function. 
  * 📝 **example 1** : 
    ```
    # Loading package
    library(gapminder)
    library(dplyr)
    
    # Filter for 1957 then summarize the median life expectancy and the maximum GDP per capita
    gapminder %>%
        filter(year == 1957) %>%
        summarize(medianLifeExp = median(lifeExp), maxGdpPerCap = max(gdpPercap))
    ```
  * 🔎 **result 1** :
    ```
    # A tibble: 1 × 2
      medianLifeExp  maxGdpPerCap
              <dbl>         <dbl>
    1          48.4       113523.
    ```
  * 📝 **example 2** : 
    ```
    # Loading package
    library(dplyr)
    
    # Find the total population in each region and state, then use total_get average and median population in each region
    ## step 1 - group region and state
    ## step 2 - calculate the total population
    ## step 3 - calculate the average_pop and median_pop
    counties %>%
        group_by(region, state) %>%
        summarize(total_pop = sum(population)) %>%
        summarize(average_pop = mean(total_pop),
                  median_pop = median(total_pop))
    ```
  * 🔎 **result 2** :
    ```
    # A tibble: 4 x 3
      region        average_pop median_pop
      <chr>               <dbl>      <dbl>
    1 North Central    5627687.    5580644
    2 Northeast        6221058.    3593222
    3 South            7370486     4804098
    4 West             5722755.    2798636
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
 
* __Get top n data__ :
  * use verb **`top_n()`** function.
  * 📝 **example** : 
    ```
    # Loading package
    library(dplyr)

    # Finding the highest avgerage income state in each region
    counties %>%
        group_by(region, state) %>%
        summarize(avg_income = mean(income)) %>%
        top_n(1, avg_income)
    ```
  * 🔎 **result** :
    ```
    # A tibble: 4 x 3
    # Groups:   region [4]
      region        state        average_income
      <chr>         <chr>                 <dbl>
    1 North Central North Dakota         55575.
    2 Northeast     New Jersey           73014.
    3 South         Maryland             69200.
    4 West          Alaska               65125.  
    ```
    
* __Cancel group by__ :
  * use verb **`ungroup()`** function.
  * If you don't want to keep columns as a group, you can use this function.
  * 📝 **example** : 
    ```
    # Loading package
    library(dplyr)
    
    # Find the total population for each combination of state and metro
    # Extract the most populated row for each state
    counties %>%
        group_by(state, metro) %>%
        summarize(total_pop = sum(population)) %>%
        top_n(1, total_pop)
        
    # Count the states with more people in Metro or Nonmetro areas    
    counties %>%
        group_by(state, metro) %>%
        summarize(total_pop = sum(population)) %>%
        top_n(1, total_pop) %>%
        ungroup() %>%
        count(metro)
    ```
  * 🔎 **result** :
    ```
    # A tibble: 50 × 3
    # Groups:   state [50]
       state       metro total_pop
       <chr>       <chr>     <dbl>
     1 Alabama     Metro   3671377
     2 Alaska      Metro    494990
     3 Arizona     Metro   6295145
     4 Arkansas    Metro   1806867
     5 California  Metro  37587429
     6 Colorado    Metro   4590896
     7 Connecticut Metro   3406918
     8 Delaware    Metro    926454
     9 Florida     Metro  18941821
    10 Georgia     Metro   8233886
    # … with 40 more rows
    
    # A tibble: 2 × 2
      metro        n
      <chr>    <int>
    1 Metro       44
    2 Nonmetro     6
    ```
