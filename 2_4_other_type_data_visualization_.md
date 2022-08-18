# Lesson 2 : Introduction to the Tidyverse

## 2-4. Other type data visualization
* 🌟 create other type plot method almost **same as "2-2. Data Visualization - Scatter Plot"**, so use ggplot() method can refer to 2-2 chapter, 
      only **different** from using **`geom_xxxx()`** function **(xxxx indicate other type plot)**. 
* __Line plot__ :
  * use **`geom_line()`**
  * can use **expand_limits(y = 0)** to set y axis to start from 0.
  * 📝 **example** : 
    ```
    # Loading package
    library(gapminder)
    library(dplyr)
    library(ggplot2)

    # Summarize the median gdpPercap by year & continent, save as by_year_continent
    by_year_continent <- gapminder %>%
        group_by(year, continent) %>%
        summarize(medianGdpPercap = median(gdpPercap))


    # Create a line plot showing the change in medianGdpPercap by continent over time
    ggplot(by_year_continent, aes(x = year, y = medianGdpPercap, color = continent)) +
        geom_line()
        expand_limits(y = 0)
    ```

  * 🔎 **result** :
  
    ![image](https://user-images.githubusercontent.com/15766139/185350014-f4a95ef5-b103-45eb-96fb-282821b9e390.png)

* __Bar plot__ :
  * use **`geom_col()`**
  * 🌟 note : unlike scatter plots or line plots, bar plots **always start at zero**.
  * 📝 **example** : 
    ```
    # Loading package
    library(gapminder)
    library(dplyr)
    library(ggplot2)

    # Summarize the median gdpPercap by continent in 1952
    by_continent <- gapminder %>%
        filter(year == 1952) %>%
        group_by(continent) %>%
        summarize(medianGdpPercap = median(gdpPercap))
        
    # Create a bar plot showing medianGdp by continent
    ggplot(by_continent, aes(x = continent, y = medianGdpPercap)) +
        geom_col()
    ```
  
  * 🔎 **result** :
  
    ![image](https://user-images.githubusercontent.com/15766139/185352286-c4ec57de-7a42-4e7e-afc6-7377ff488bf5.png)

* __Histogram__ :
  * use **`geom_histogram()`**
    * argument : 
      * bins = <number> : setting a little binwidth like this makes the histogram a bit blockier (ref example 1).
      * binwidth = <number> : setting a wide binwidth like this makes the histogram a bit blockier (ref example 2).
  * 🌟 note : only set x axis.
  * 📝 **example 1** : 
    ```
    # Loading package
    library(gapminder)
    library(dplyr)
    library(ggplot2)
    
    # Get pop by milion and year is 1952
    gapminder_1952 <- gapminder %>%
        filter(year == 1952) %>%
        mutate(pop_by_mil = pop / 1000000)

    # Create a histogram of population (pop_by_mil)
    ggplot(gapminder_1952, aes(x = pop_by_mil)) +
        geom_histogram(bins = 50)
    ```  
  * 🔎 **result 1** :
  
    ![image](https://user-images.githubusercontent.com/15766139/185354301-d844304b-e81e-4d7b-b164-ac30eaf16035.png)

  * 📝 **example 2** : 
    ```
    # Loading package
    library(gapminder)
    library(dplyr)
    library(ggplot2)

    # get all data in 2007 year
    gapminder_2007 <- gapminder %>%
        filter(year == 2007)

    # Create a histogram of population (pop_by_mil)
    ggplot(gapminder_2007, aes(x = lifeExp)) +
        geom_histogram(binwidth = 5)
    ```   
  * 🔎 **result 2** :
  
    ![image](https://user-images.githubusercontent.com/15766139/185355607-74c260a6-0612-4f1d-ac45-0cf524438c35.png)
  
* __Box plot__ :
  * use **`geom_boxplot()`**
  * Description : 
  
      ![image](https://user-images.githubusercontent.com/15766139/185361460-f86d33c4-4bd1-4f7e-a498-858e16a8c87d.png)

      ![image](https://user-images.githubusercontent.com/15766139/185358722-e12fbaa7-3da1-41fa-9522-ef1f03ce21f9.png)
      
      * median (Q2, 50th percentile): the median value of the dataset.
      * 1st quartile (Q1, 25th percentile): the middle number between the smallest number (not the "minimum") and the median of the dataset.
      * 3rd quartile (Q3, 75th Percentile): between the median and the maximum value of the dataset.
      * IQR : the distance between the 25th and 75th percentiles.
      * whiskers : shown in blue.
      * outliers : shown as green circles.
      * max : Q3 + 1.5 * IQR
      * lowest : Q1 -1.5 * IQR
      
  * 📝 **example** : 
    ```
    library(gapminder)
    library(dplyr)
    library(ggplot2)

    gapminder_1952 <- gapminder %>%
      filter(year == 1952)

    # Add a title to this graph: "Comparing GDP per capita across continents"
    ggplot(gapminder_1952, aes(x = continent, y = gdpPercap)) +
      geom_boxplot() +
      ggtitle("Comparing GDP per capita across continents") +
      scale_y_log10()
    ```
    
  * 🔎 **result** :
    ![image](https://user-images.githubusercontent.com/15766139/185356339-b368f8b0-f070-481b-b1a3-7cc890f33705.png)
