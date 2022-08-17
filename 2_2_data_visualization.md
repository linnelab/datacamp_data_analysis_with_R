# Lesson 2 : Introduction to the Tidyverse

## 2-2. Data visualization
* __Create a scatter plot__ :
  * 🔆 Step 1 : load package : 
    * **`ggplot2`** : data visualization.
    * **gapminder** : get dataset.
    * **dplyr** : transfrom data, like filter(), mutate(), arrange() function.
    * 📝 **example** : 
      ```
      library(gapminder)
      library(dplyr)
      library(ggplot2)
      ```
  * 🔆 Step 2 : use variable assignment to create a data subset, this data subset will use to draw plot.
    * 📝 **example** : 
      ```
      # create gapminder_2007 data subset
      gapminder_2007 <- gapminder %>%
          filter(year == 2007)

      # print out gapminder_2007
      gapminder_2007
      ```
    * 🔎 **result** :
      ```
      gapminder_2007
      # A tibble: 142 × 6
         country     continent  year lifeExp       pop gdpPercap
         <fct>       <fct>     <int>   <dbl>     <int>     <dbl>
       1 Afghanistan Asia       2007    43.8  31889923      975.
       2 Albania     Europe     2007    76.4   3600523     5937.
       3 Algeria     Africa     2007    72.3  33333216     6223.
       4 Angola      Africa     2007    42.7  12420476     4797.
       5 Argentina   Americas   2007    75.3  40301927    12779.
       6 Australia   Oceania    2007    81.2  20434176    34435.
       7 Austria     Europe     2007    79.8   8199783    36126.
       8 Bahrain     Asia       2007    75.6    708573    29796.
       9 Bangladesh  Asia       2007    64.1 150448339     1391.
      10 Belgium     Europe     2007    79.4  10392226    33693.
      # … with 132 more rows
      ```
  * 🔆 Step 3 : use **ggplot()** function to draw scatter plot.
    * Introduction :
      ```
      ggplot(dataframe_name, aes(x = column_name1, y = column_name2, color = column_name3, size = column_name4)) +
          geom_point() +
          scale_x_log10() +
          scale_y_log10()
      ```
      * **dataframe_name** : place the source data you want to draw plot.
      * **aes** : aesthetic.
      * **x** : plot x axis.
      * **y** : plot y axis.
      * **color** : according to a column to distinguish point colors in the figure.
      * **size** : according to a column to show point size in the figure.
      * **geom_point** : use scatter plot (geom = geometric).
      * **scale_x_log10 or scale_y_log10** : 
        <br>If the values in the column are big different, causes many points in the graph to be biased to one side,
        <br>it will let the plot not to easy read. (refer to the figure below) 
        <br>you can use log to reduce x axis or y axis value, and let point clearly distributed, increase readability for the plot.</br>  

        ![image](https://user-images.githubusercontent.com/15766139/185030567-62c0fa08-679b-4fc7-aa06-2250e274f9c9.png)

    * 📝 **example** : 
      ```
      # Scatter plot comparing pop and gdpPercap, with x axes on a log scale
      ggplot(gapminder_2007, aes(x = pop, y = lifeExp, color = continent, size = gdpPercap)) +
          geom_point() +
          scale_x_log10()
      ```
    * 🔎 **result** :

      ![image](https://user-images.githubusercontent.com/15766139/185029887-697ae00b-a93e-49f0-ad26-ba018232c083.png)
       
 * __Create scatter subplot__ : 
   * You can add function **`facet_wrap(~ column_name)`**
     * **~** : means **"by"**, meaning that you're splitting the plot by this column.
     * 📝 **example** : 
       ```
       ggplot(gapminder_2007, aes(x = pop, y = lifeExp, color = continent, size = gdpPercap)) +
           geom_point() +
           scale_x_log10() +
           facet_wrap(~ year)
       ```
     * 🔎 **result** : 
       ![image](https://user-images.githubusercontent.com/15766139/185040187-752aba68-cb44-44b8-89af-a56645602194.png)

