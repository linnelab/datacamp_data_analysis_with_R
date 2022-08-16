# Lesson 2 : Introduction to the Tidyverse

## 2-1. Data wrangling
* __Introdution__ :
  * tidyverse tool : 
    * A collection of **`data science tools`** within R for **`transforming and visualizing data`**.
    * This is not the only set of tools in R, but it's a powerful and **`popular approach for exploring data`**.
  
  * gapminder package : 
    * contains the **`dataset`** : tracks economic and social indicators like life expectancy and the GDP per capita of countries over time. 
    * data structure is a **`data frame`**.
    * if you print gapminder data frame : 
      * first line will show **tibble**, it's a special data frame. 
      * default show **10 rows**.
  
  * dplyr package
    * **`transforming data`**, such as filtering, sorting, and summarizing it.
  
* __Import package__ :
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
* __Filter data__ :
  * use verb **`filter(condition1, condition2, ...)`** funciton.
    * it will not to change original dataframe data (e.g. gapminder), it will create a new data frame.
  * 🌟 **note** : 
    * every time you apply a **`verb`**, you'll use a **`pipe (%>%)`**.
    * this pipe means take whatever is before it, and feed it into the next step.
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
  * 📝 **example** :
    ```
    # loading gapminder package to get dataset
    library(gapminder)

    # loading dplyr package
    library(dplyr)

    # Filter the gapminder dataset for the year 1957
    gapminder %>%
      filter(year == 1957)
      
    # Filter for China in 2002
    gapminder %>%
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
* __Sorting data__ :
  * use verb **`arrange()`** function
  * sorting a table based on variable (i.e. column).
    * it will not to change original dataframe data (e.g. gapminder), it will create a new data frame.
  * 📝 **example** :
    ```
    # loading package
    library(gapminder)
    library(dplyr)
    
    # Sort in ascending order of lifeExp
    gapminder %>%
        arrange(lifeExp)
        
    # Sort in descending order of lifeExp
    gapminder %>%
        arrange(desc(lifeExp))
        
    # Filter for the year 1957, then arrange in descending order of population
    gapminder %>%
        filter(year == 1957) %>%
        arrange(desc(pop))
    ```
  * 🔎 **result** :
    ```
    # A tibble: 1,704 × 6
       country      continent  year lifeExp     pop gdpPercap
       <fct>        <fct>     <int>   <dbl>   <int>     <dbl>
     1 Rwanda       Africa     1992    23.6 7290203      737.
     2 Afghanistan  Asia       1952    28.8 8425333      779.
     3 Gambia       Africa     1952    30    284320      485.
     4 Angola       Africa     1952    30.0 4232095     3521.
     5 Sierra Leone Africa     1952    30.3 2143249      880.
     6 Afghanistan  Asia       1957    30.3 9240934      821.
     7 Cambodia     Asia       1977    31.2 6978607      525.
     8 Mozambique   Africa     1952    31.3 6446316      469.
     9 Sierra Leone Africa     1957    31.6 2295678     1004.
    10 Burkina Faso Africa     1952    32.0 4469979      543.
    # … with 1,694 more rows
    
    # A tibble: 1,704 × 6
       country          continent  year lifeExp       pop gdpPercap
       <fct>            <fct>     <int>   <dbl>     <int>     <dbl>
     1 Japan            Asia       2007    82.6 127467972    31656.
     2 Hong Kong, China Asia       2007    82.2   6980412    39725.
     3 Japan            Asia       2002    82   127065841    28605.
     4 Iceland          Europe     2007    81.8    301931    36181.
     5 Switzerland      Europe     2007    81.7   7554661    37506.
     6 Hong Kong, China Asia       2002    81.5   6762476    30209.
     7 Australia        Oceania    2007    81.2  20434176    34435.
     8 Spain            Europe     2007    80.9  40448191    28821.
     9 Sweden           Europe     2007    80.9   9031088    33860.
    10 Israel           Asia       2007    80.7   6426679    25523.
    # … with 1,694 more rows
    
    # A tibble: 142 × 6
       country        continent  year lifeExp       pop gdpPercap
       <fct>          <fct>     <int>   <dbl>     <int>     <dbl>
     1 China          Asia       1957    50.5 637408000      576.
     2 India          Asia       1957    40.2 409000000      590.
     3 United States  Americas   1957    69.5 171984000    14847.
     4 Japan          Asia       1957    65.5  91563009     4318.
     5 Indonesia      Asia       1957    39.9  90124000      859.
     6 Germany        Europe     1957    69.1  71019069    10188.
     7 Brazil         Americas   1957    53.3  65551171     2487.
     8 United Kingdom Europe     1957    70.4  51430000    11283.
     9 Bangladesh     Asia       1957    39.3  51365468      662.
    10 Italy          Europe     1957    67.8  49182000     6249.
    # … with 132 more rows
    ```
    
* __Change column data or add new column__ :
  * use verb **`mutate()`** function.
  * changes or adds variables (i.e. variable = column).
    * it will not to change original dataframe data (e.g. gapminder), it will create a new data frame.
  * 📝 **example** :
    ```
    # loading package
    library(gapminder)
    library(dplyr)
    
    # Use mutate to change lifeExp to be in months
    gapminder %>%
        mutate(lifeExp = lifeExp * 12)
        
    # Use mutate to create a new column called lifeExpMonths
    gapminder %>%
        mutate(lifeExpMonths = lifeExp * 12)
        
    # if you want to change a variable and add a new variable
    gapminder %>%
        mutate(pop = pop / 1000000, gdp = pop * gdpPercap)
        
    # find the countries with the highest life expectancy, in months, in the year 2007
    gapminder %>%
        filter(year == 2007) %>%
        mutate(lifeExpMonths = lifeExp * 12) %>%
        arrange(desc(lifeExpMonths))
    ```
  * 🔎 **result** :
    ```
    # A tibble: 1,704 × 6
       country      continent  year lifeExp      pop gdpPercap
       <fct>        <fct>     <int>   <dbl>    <int>     <dbl>
     1 Afghanistan  Asia       1952    346.  8425333      779.
     2 Afghanistan  Asia       1957    364.  9240934      821.
     3 Afghanistan  Asia       1962    384. 10267083      853.
     4 Afghanistan  Asia       1967    408. 11537966      836.
     5 Afghanistan  Asia       1972    433. 13079460      740.
     6 Afghanistan  Asia       1977    461. 14880372      786.
     7 Afghanistan  Asia       1982    478. 12881816      978.
     8 Afghanistan  Asia       1987    490. 13867957      852.
     9 Afghanistan  Asia       1992    500. 16317921      649.
    10 Afghanistan  Asia       1997    501. 22227415      635.
    # … with 1,694 more rows
    
    # A tibble: 1,704 × 7
       country      continent  year lifeExp      pop gdpPercap lifeExpMonths
       <fct>        <fct>     <int>   <dbl>    <int>     <dbl>         <dbl>
     1 Afghanistan  Asia       1952    28.8  8425333      779.          346.
     2 Afghanistan  Asia       1957    30.3  9240934      821.          364.
     3 Afghanistan  Asia       1962    32.0 10267083      853.          384.
     4 Afghanistan  Asia       1967    34.0 11537966      836.          408.
     5 Afghanistan  Asia       1972    36.1 13079460      740.          433.
     6 Afghanistan  Asia       1977    38.4 14880372      786.          461.
     7 Afghanistan  Asia       1982    39.9 12881816      978.          478.
     8 Afghanistan  Asia       1987    40.8 13867957      852.          490.
     9 Afghanistan  Asia       1992    41.7 16317921      649.          500.
    10 Afghanistan  Asia       1997    41.8 22227415      635.          501.
    # … with 1,694 more rows
      
    # A tibble: 1,704 × 7
       country      continent  year lifeExp   pop gdpPercap    gdp
       <fct>        <fct>     <int>   <dbl> <dbl>     <dbl>  <dbl>
     1 Afghanistan  Asia       1952    28.8  8.43      779.  6567.
     2 Afghanistan  Asia       1957    30.3  9.24      821.  7585.
     3 Afghanistan  Asia       1962    32.0  10.3      853.  8759.
     4 Afghanistan  Asia       1967    34.0  11.5      836.  9648.
     5 Afghanistan  Asia       1972    36.1  13.1      740.  9679.
     6 Afghanistan  Asia       1977    38.4  14.9      786.  11698.
     7 Afghanistan  Asia       1982    39.9  12.9      978.  12599.
     8 Afghanistan  Asia       1987    40.8  13.9      852.  11821.
     9 Afghanistan  Asia       1992    41.7  16.3      649.  10596.
    10 Afghanistan  Asia       1997    41.8  22.2      635.  14122.
    # … with 1,694 more rows
    
    # A tibble: 142 × 7
       country           continent  year lifeExp       pop gdpPercap lifeExpMonths
       <fct>             <fct>     <int>   <dbl>     <int>     <dbl>         <dbl>
     1 Japan             Asia       2007    82.6 127467972    31656.          991.
     2 Hong Kong, China  Asia       2007    82.2   6980412    39725.          986.
     3 Iceland           Europe     2007    81.8    301931    36181.          981.
     4 Switzerland       Europe     2007    81.7   7554661    37506.          980.
     5 Australia         Oceania    2007    81.2  20434176    34435.          975.
     6 Spain             Europe     2007    80.9  40448191    28821.          971.
     7 Sweden            Europe     2007    80.9   9031088    33860.          971.
     8 Israel            Asia       2007    80.7   6426679    25523.          969.
     9 France            Europe     2007    80.7  61083916    30470.          968.
    10 Canada            Americas   2007    80.7  33390141    36319.          968.
    # … with 132 more rows
    ```
