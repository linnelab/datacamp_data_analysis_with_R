# Lesson 2 : Introduction to the Tidyverse

## 2-3. Grouping and summarizing
* __Summarize data__ :
  * use verb **`summarize()`** function.
  * you can use these functions for summarizing :
    * **mean()** : the sum of the values / the number of values.
    * **sum()** 
    * **median()** : the middle most value in a data series is called the median.
    * **max()** 
    * **min()**
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
