# Lesson 2 : Introduction to the Tidyverse

## 2-1. Data wrangling
* __Introdution__ :
  * Tidyverse tool : 
    * A collection of **`data science tools`** within R for **`transforming and visualizing data`**.
    * This is not the only set of tools in R, but it's a powerful and **`popular approach for exploring data`**.
  
  * Gapminder package : 
    * contains the **`dataset`** : tracks economic and social indicators like life expectancy and the GDP per capita of countries over time. 
    * data structure is a **`data frame`**.
    * if you output Gapminder data frame : 
      * first line will show **tibble**, it's a special data frame. 
      * default show **10 rows**.
  
  * dplyr package
    * **`transforming data`**, such as filtering, sorting, and summarizing it.
  
* import package :
  * ✒ use **`library()`** function.
  * 📝 **example** :
    ```
    # loading Gapminder package to get dataset
    library(gapminder)

    # loading dplyr package
    library(dplyr)

    # Look at the gapminder dataset 
    gapminder
    ```
  * 🔎 **result** :
    ```
    gapminder
    # A tibble: 1,704 × 6
       country     continent  year lifeExp      pop gdpPercap
       <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
     1 Afghanistan Asia       1952    28.8  8425333      779.
     2 Afghanistan Asia       1957    30.3  9240934      821.
     3 Afghanistan Asia       1962    32.0 10267083      853.
     4 Afghanistan Asia       1967    34.0 11537966      836.
     5 Afghanistan Asia       1972    36.1 13079460      740.
     6 Afghanistan Asia       1977    38.4 14880372      786.
     7 Afghanistan Asia       1982    39.9 12881816      978.
     8 Afghanistan Asia       1987    40.8 13867957      852.
     9 Afghanistan Asia       1992    41.7 16317921      649.
    10 Afghanistan Asia       1997    41.8 22227415      635.
    # … with 1,694 more rows
    ```
* filter data :
  * use verb **`filter(condition1, condition2, ...)`** funciton.
  * 🌟 **Note** : 
    * every time you apply a **`verb`**, you'll use a **`pipe (%>%)`**
    * **correct** : the pipe (%>%) put the verb at the end of the previous line.
      * For example :
        ```
        gapminder %>%
          filter(year == 2002, country == "China")
        ```
    * **incorrect** : put pipe (%>%) before the verb, it will get error message.
      * For example :
        ```
        gapminder  
          %>% filter(year == 2002, country == "China")
        ```
      * Error message :
        ```
        Parsing error in script.R:6:5: unexpected SPECIAL
        5: gapminder  
        6:     %>%
               ^
        ```
    * this pipe means take whatever is before it, and feed it into the next step.
  * 📝 **example** :
    ```
    # loading Gapminder package to get dataset
    library(Gapminder)

    # loading dplyr package
    library(dplyr)

    # Filter the gapminder dataset for the year 1957
    Gapminder %>%
      filter(year == 1957)
      
    # Filter for China in 2002
    Gapminder %>%
      filter(year == 2002, country == "China")
    ```
  * 🔎 **result** :
    ```
    # A tibble: 142 × 6
       country     continent  year lifeExp      pop gdpPercap
       <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
     1 Afghanistan Asia       1957    30.3  9240934      821.
     2 Albania     Europe     1957    59.3  1476505     1942.
     3 Algeria     Africa     1957    45.7 10270856     3014.
     4 Angola      Africa     1957    32.0  4561361     3828.
     5 Argentina   Americas   1957    64.4 19610538     6857.
     6 Australia   Oceania    1957    70.3  9712569    10950.
     7 Austria     Europe     1957    67.5  6965860     8843.
     8 Bahrain     Asia       1957    53.8   138655    11636.
     9 Bangladesh  Asia       1957    39.3 51365468      662.
    10 Belgium     Europe     1957    69.2  8989111     9715.
    # … with 132 more rows
    
    
    # A tibble: 1 × 6
        country continent  year lifeExp       pop    gdpPercap
        <fct>   <fct>     <int>   <dbl>      <int>      <dbl>
      1 China   Asia       2002    72.0   1280400000    3119.
    ```
