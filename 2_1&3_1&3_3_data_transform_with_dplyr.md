# Lesson 2 & 3 : Introduction to the Tidyverse and dplyr

## 2-1 & 3-1 & 3-3. Data transform with dplyr
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

* __Install package__ :
  * ✒ use **`install.packages("package_name")`**.
  * run this script on R console.
  * 📝 **example** :
    ```
    install.packages("gapminder")
    install.packages("dplyr")
    ```
    
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

* __Look at datasets__ :
  * ✒ use **`glimpse(dataset_name)`** function.
  * If you get a new datasets, you can use this function to view data content.
  * 📝 **example** :
    ```
    # Loading package
    library(gapminder)
    library(dplyr)
    
    # Take a look at the gapminder dataset
    glimpse(gapminder)
    ```
  * 🔎 **result** :
    ```
    Rows: 1,704
    Columns: 6
    $ country   <fct> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", …
    $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Europe, Europe, Eu…
    $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997, 2002, 2007, 1952, 1957, 1962, …
    $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 40.822, 41.674, 41.763, 42.129, 43…
    $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372, 12881816, 13867957, 16317921, 22…
    $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.1134, 978.0114, 852.3959, 649.3414, …
    ```

* __Select columns__ :
  * ✒ use verb **`select(column_name1, column_name2, ...)`** function, and use the following different methods to get columns.
  * 💡 method 1 : select specific columns
    * For example :
      ```
      select(column_name1, column_name2, column_name3, ...)
      ```
    * 📝 **example** :
      ```
      # Loading package
      library(gapminder)
      library(dplyr)

      # Select columns
      gapminder %>%
        select(country, continent, year, lifeExp)
      ```
    * 🔎 **result** :
      ```
      # A tibble: 1,704 × 4
         country      continent  year lifeExp
         <fct>        <fct>     <int>   <dbl>
       1 Afghanistan  Asia       1952    28.8
       2 Afghanistan  Asia       1957    30.3
       3 Afghanistan  Asia       1962    32.0
       4 Afghanistan  Asia       1967    34.0
       5 Afghanistan  Asia       1972    36.1
       6 Afghanistan  Asia       1977    38.4
       7 Afghanistan  Asia       1982    39.9
       8 Afghanistan  Asia       1987    40.8
       9 Afghanistan  Asia       1992    41.7
      10 Afghanistan  Asia       1997    41.8
      # … with 1,694 more rows
      ```
   * 💡 method 2 : use **`:`** to select a range columns
      * For example :
        ```
        select(column_name1, column_name2, column_name3:column_name10)
        ```
      * 📝 **example** :
        ```
        # Loading package
        library(dplyr)
        
        # step 1 - select state, county, population, and industry-related columns
        # step 2 - arrange service in descending order 
        counties %>%
            select(state, county, population, professional:production) %>%
            arrange(service)
        ```
      * 🔎 **result** :
        ```
        # A tibble: 3,138 × 8
           state        county    population professional service office construction production
           <chr>        <chr>          <dbl>        <dbl>   <dbl>  <dbl>        <dbl>      <dbl>
         1 Texas        Glasscock       1180         44.1     5     19.2         27.3        4.4
         2 Montana      McCone          1728         52.4     6.2   22.7         13.6        5.1
         3 North Dakota Slope            673         46.3     7.5   14.9         19.7       11.6
         4 South Dakota Sully           1469         40.9     8.2   19.4         23.1        8.4
         5 Montana      Petroleum        443         43.7     8.3   21.7         20.1        6.3
         6 Kansas       Sheridan        2531         39.1     8.4   20.5         14.5       17.5
         7 North Dakota Cavalier        3890         43.5     8.4   20.4         14.6       13  
         8 Oklahoma     Ellis           4121         35.9     8.9   21.9         19         14.3
         9 Texas        Lipscomb        3483         32.1     8.9   16.5         20.5       22  
        10 Nebraska     Dundy           2015         41.3     9.1   16.4         22.5       10.6
        # … with 3,128 more rows
        ```
   * 💡 method 3 : use **`contains()`** to select columns name contain keyword 
      * For example :
        ```
        select(column_name1, column_name2, contains(column_name3))
        ```
      * 📝 **example** :
        ```
        # Loading package
        library(dplyr)
        
        # Select state, county, and columns name contain work string.
        counties %>%
            select(state, county, contains("work"))  
        ```
      * 🔎 **result** :
        ```
        # A tibble: 3,138 × 6
           state   county   work_at_home private_work public_work family_work
           <chr>   <chr>           <dbl>        <dbl>       <dbl>       <dbl>
         1 Alabama Autauga           1.8         73.6        20.9         0  
         2 Alabama Baldwin           3.9         81.5        12.3         0.4
         3 Alabama Barbour           1.6         71.8        20.8         0.1
         4 Alabama Bibb              0.7         76.8        16.1         0.4
         5 Alabama Blount            2.3         82          13.5         0.4
         6 Alabama Bullock           2.8         79.5        15.1         0  
         7 Alabama Butler            1.7         77.4        16.2         0.2
         8 Alabama Calhoun           2.7         74.1        20.8         0.1
         9 Alabama Chambers          2.1         85.1        12.1         0  
        10 Alabama Cherokee          2.5         73.1        18.5         0.5
        # … with 3,128 more rows
        ```
   * 💡 method 4 : use **`starts_with()`** to select columns name starts with keyword 
      * For example :
        ```
        select(column_name1, column_name2, starts_with("string_name"))
        ```
      * 📝 **example** :
        ``` 
        # Loading package
        library(dplyr)

        # Select state, county, and columns name starts with income keyword
        counties %>%
          select(state, county, starts_with("income"))
        ```
      * 🔎 **result** :
        ```
        # A tibble: 3,138 × 6
           state   county   income income_err income_per_cap income_per_cap_err
           <chr>   <chr>     <dbl>      <dbl>          <dbl>              <dbl>
         1 Alabama Autauga   51281       2391          24974               1080
         2 Alabama Baldwin   50254       1263          27317                711
         3 Alabama Barbour   32964       2973          16824                798
         4 Alabama Bibb      38678       3995          18431               1618
         5 Alabama Blount    45813       3141          20532                708
         6 Alabama Bullock   31938       5884          17580               2055
         7 Alabama Butler    32229       1793          18390                714
         8 Alabama Calhoun   41703        925          21374                489
         9 Alabama Chambers  34177       2949          21071               1366
        10 Alabama Cherokee  36296       1710          21811               1556
        # … with 3,128 more rows
        ```
   * 💡 method 5 : use **`ends_with()`** to select columns name end with keyword 
      * For example :
        ```
        select(column_name1, column_name2, ends_with("string_name"))
        ```
      * 📝 **example** :
        ```
        # Loading package
        library(dplyr)

        # step 1 - select the state, county, population, and columns name end with "work" keyword
        # step 2 - filter for counties that have at least 50% of people engaged in public work
        counties %>%
            select(state, county, population, ends_with("work")) %>%
            filter(public_work >= 50.0)
        ```
      * 🔎 **result** :
        ```
        # A tibble: 7 × 6
          state        county                     population private_work public_work family_work
          <chr>        <chr>                           <dbl>        <dbl>       <dbl>       <dbl>
        1 Alaska       Lake and Peninsula Borough       1474         42.2        51.6         0.2
        2 Alaska       Yukon-Koyukuk Census Area        5644         33.3        61.7         0  
        3 California   Lassen                          32645         42.6        50.5         0.1
        4 Hawaii       Kalawao                            85         25          64.1         0  
        5 North Dakota Sioux                            4380         32.9        56.8         0.1
        6 South Dakota Todd                             9942         34.4        55           0.8
        7 Wisconsin    Menominee                        4451         36.8        59.1         0.4
        ```
   * 💡 method 6 : use **`last_col()`** to select last column
      * For example :
        ```
        # select last one column
        select(column_name1, column_name2, last_col())
        
        # select last two column
        select(column_name1, column_name2, last_col(offset = 1L))
        ```
      * 📝 **example** :
        ```  
        # Loading package
        library(dplyr)

        # select last one column (i.e. land_area)
        counties %>%
          select(state, county, last_col())
          
        # select last two column (i.e. unemployment)
        counties %>%
           select(state, county, last_col(offset = 1L))
        ```
      * 🔎 **result** :
        ```
        # A tibble: 3,138 × 3
           state   county   land_area
           <chr>   <chr>        <dbl>
         1 Alabama Autauga       594.
         2 Alabama Baldwin      1590.
         3 Alabama Barbour       885.
         4 Alabama Bibb          623.
         5 Alabama Blount        645.
         6 Alabama Bullock       623.
         7 Alabama Butler        777.
         8 Alabama Calhoun       606.
         9 Alabama Chambers      597.
        10 Alabama Cherokee      554.
        # … with 3,128 more row
        
        # A tibble: 3,138 × 3
           state   county   unemployment
           <chr>   <chr>           <dbl>
         1 Alabama Autauga           7.6
         2 Alabama Baldwin           7.5
         3 Alabama Barbour          17.6
         4 Alabama Bibb              8.3
         5 Alabama Blount            7.7
         6 Alabama Bullock          18  
         7 Alabama Butler           10.9
         8 Alabama Calhoun          12.3
         9 Alabama Chambers          8.9
        10 Alabama Cherokee          7.9
        # … with 3,128 more rows
        ```
   * 💡 method 7 : use **`-`** to remove column
      * 🌟 remove column : the original dataframe column is not removed, it just doesn't show the columns.
      * For example :
        ```
        # don't to select these column
        select(-column_name1, -column_name2)
        ```
      * 📝 **example** :
        ``` 
        # Loading package
        library(dplyr)
        library(gapminder)

        # check data content
        glimpse(gapminder)
        
        # not to select gdpPercap and continent column
        gapminder %>%
          select(-gdpPercap, -continent)
        ```
      * 🔎 **result** :
        ```
        Rows: 1,704
        Columns: 6
        $ country   <fct> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan"…
        $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Europe, Europe, Europe, Europe,…
        $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997, 2002, 2007, 1952, 1957, 1962, 1967, 1972, 1…
        $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 40.822, 41.674, 41.763, 42.129, 43.828, 55.230,…
        $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372, 12881816, 13867957, 16317921, 22227415, 25268…
        $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.1134, 978.0114, 852.3959, 649.3414, 635.3414, 726…
        
        # A tibble: 1,704 × 4
           country      year lifeExp      pop
           <fct>       <int>   <dbl>    <int>
         1 Afghanistan  1952    28.8  8425333
         2 Afghanistan  1957    30.3  9240934
         3 Afghanistan  1962    32.0 10267083
         4 Afghanistan  1967    34.0 11537966
         5 Afghanistan  1972    36.1 13079460
         6 Afghanistan  1977    38.4 14880372
         7 Afghanistan  1982    39.9 12881816
         8 Afghanistan  1987    40.8 13867957
         9 Afghanistan  1992    41.7 16317921
        10 Afghanistan  1997    41.8 22227415
        # … with 1,694 more rows  
        ```

  * 💡 another method : you can enter **`?select_helpers`** on console (e.g. pic 1), then it will show detail select usage (e.g. pic 2).
     * pic 1 :

       ![image](https://user-images.githubusercontent.com/15766139/185779034-ca34fa48-22cc-4af3-9265-6c3c77d5391b.png)

     * pic 2 :

       ![image](https://user-images.githubusercontent.com/15766139/185779059-07809d1d-059e-470a-be59-f1104c857970.png)

* __Rename column__ :
  * use the following methods :
  * 💡 method 1 : 
    * For example :
      ```
      select(column_name1, column_name2, new_column_name3 = old_column_name3)
      ```
    * 📝 **example** :
      ```
      # Loading package
      library(dplyr)

      # Select state, county, and change poverty to poverty_rate
      counties %>%
        select(state, county, poverty, poverty_rate = poverty)
      ```
    * 🔎 **result** :
      ```  
            # A tibble: 3,138 × 3
         state   county   poverty_rate
         <chr>   <chr>           <dbl>
       1 Alabama Autauga          12.9
       2 Alabama Baldwin          13.4
       3 Alabama Barbour          26.7
       4 Alabama Bibb             16.8
       5 Alabama Blount           16.7
       6 Alabama Bullock          24.6
       7 Alabama Butler           25.4
       8 Alabama Calhoun          20.5
       9 Alabama Chambers         21.6
      10 Alabama Cherokee         19.2
      # … with 3,128 more rows
      ```
  * 💡 method 2 : 
    * For example :
      ```
      rename(new_column_name1 = old_column_name1)
      ```
    * 📝 **example** :
      ```
      # step 1 - count the number of counties in each state
      # step 2 - rename the n column to num_counties
      counties %>%
          count(state) %>%
          rename(num_counties = n)
      ```
    * 🔎 **result** :
      ``` 
      # A tibble: 50 x 2
         state       num_counties
         <chr>              <int>
       1 Alabama               67
       2 Alaska                28
       3 Arizona               15
       4 Arkansas              75
       5 California            58
       6 Colorado              64
       7 Connecticut            8
       8 Delaware               3
       9 Florida               67
      10 Georgia              159
      # ... with 40 more rows
      ```

* __Filter data__ :
  * ✒ use verb **`filter(condition1, condition2, ...)`** funciton.
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
  * ✒ use verb **`arrange()`** function
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
  * ✒ use verb **`mutate()`** function.
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

* __Combine select and mutate__ :
  * use verb **`transmute()`** function.
  * **transmute() = select() + mutate()**, 
    * this function can **select columns** (equal **select()** function) and 
      <br>**calculate columns** at the same time to get new column (equal **mutate()** function), then get a subset result.
  * 📝 **example** :
    ```
    # loading package
    library(dplyr)
    
    # step 1 - keep the state, county, populations, and add a density column
    # step 2 - filter for counties with a population greater than one million 
    # step 3 - sort density in ascending order 
    counties %>%
        transmute(state, county, population, density = population / land_area) %>%
        filter(population >= 1000000) %>%
        arrange(density)
    ```
  * 🔎 **result** :
    ```
    # A tibble: 41 × 4
       state      county         population density
       <chr>      <chr>               <dbl>   <dbl>
     1 California San Bernardino    2094769    104.
     2 Nevada     Clark             2035572    258.
     3 California Riverside         2298032    319.
     4 Arizona    Maricopa          4018143    437.
     5 Florida    Palm Beach        1378806    700.
     6 California San Diego         3223096    766.
     7 Washington King              2045756    967.
     8 Texas      Travis            1121645   1133.
     9 Florida    Hillsborough      1302884   1277.
    10 Florida    Orange            1229039   1360.
    # … with 31 more rows
    ```

* __Summary practice__ :
  * 📝 **example** :
    ```
    # read rds file
    filename <- file.choose()          # it will show a windows as pic 1, you can choice path file.
    counties <- readRDS(filename)

    # Loading package
    library(dplyr)
    
    # Select the five columns
    # Calculate men percentage and save to the proportion_men variable
    # Filter for population of at least 10,000
    # Arrange proportion of men in descending order
    counties %>% 
      select(state, county, population, men, women) %>% 
      mutate(proportion_men = men / population) %>% 
      filter(population > 10000) %>% 
      arrange(desc(proportion_men))
    ```
    * 🍀 pic 1 :
    
      ![image](https://user-images.githubusercontent.com/15766139/185534134-f30ae5cd-c8fa-4b22-8666-292c4fcb39bb.png)
 
  * 🔎 **result** :
    ```
    # A tibble: 2,437 × 6
       state      county         population   men women proportion_men
       <chr>      <chr>               <dbl> <dbl> <dbl>          <dbl>
     1 Virginia   Sussex              11864  8130  3734          0.685
     2 California Lassen              32645 21818 10827          0.668
     3 Georgia    Chattahoochee       11914  7940  3974          0.666
     4 Louisiana  West Feliciana      15415 10228  5187          0.664
     5 Florida    Union               15191  9830  5361          0.647
     6 Texas      Jones               19978 12652  7326          0.633
     7 Missouri   DeKalb              12782  8080  4702          0.632
     8 Texas      Madison             13838  8648  5190          0.625
     9 Virginia   Greensville         11760  7303  4457          0.621
    10 Texas      Anderson            57915 35469 22446          0.612
    # … with 2,427 more rows    
    ```
