# Lesson 3 : Data Manipulation with dplyr

## 3-5. Summary Practice

* practice for chapter 3 content.
* use babynames dataset, link : https://github.com/linnelab/datacamp_data_analysis_with_R/blob/main/dataset/babynames.rds
* 🌻 practice 1 :
  * filter for only the year 1990.
  * sort the table in descending order of the number of babies born.
  ```
  # Loading package
  library(dplyr)
  
  babynames %>%
      filter(year == 1990) %>%
      arrange(desc(number))
  ```
* 🚀 result 1 :
  ```
  # A tibble: 21,223 × 3
      year name        number
     <dbl> <chr>        <int>
   1  1990 Michael      65560
   2  1990 Christopher  52520
   3  1990 Jessica      46615
   4  1990 Ashley       45797
   5  1990 Matthew      44925
   6  1990 Joshua       43382
   7  1990 Brittany     36650
   8  1990 Amanda       34504
   9  1990 Daniel       33963
  10  1990 David        33862
  # … with 21,213 more rows  
  ```
  
* 🌻 practice 2 :
  * find the most common name for US babies in each year.
  ```
  # Loading package
  library(dplyr)
  
  babynames %>%
      group_by(year) %>%
      top_n(1, number)
  ```
* 🚀 result 2 :
  ```
  # A tibble: 28 × 3
  # Groups:   year [28]
        year name  number
       <dbl> <chr>  <int>
     1  1880 John    9701
     2  1885 Mary    9166
     3  1890 Mary   12113
     4  1895 Mary   13493
     5  1900 Mary   16781
     6  1905 Mary   16135
     7  1910 Mary   22947
     8  1915 Mary   58346
     9  1920 Mary   71175
    10  1925 Mary   70857
    # … with 18 more rows
  ```
  
* 🌻 practice 3 :
  * filter for the names Steven, Thomas, and Matthew.
  * plot the names using a different color for each name.
  ```
  # Loading package
  library(dplyr)
  library(ggplot2)

  selected_names <- babynames %>%
    filter(name %in% c("Steven", "Thomas", "Matthew"))

  ggplot(selected_names, aes(x = year, y = number, color = name)) +
    geom_line()
  ```
* 🚀 result 3 :
  
  ![image](https://user-images.githubusercontent.com/15766139/185846721-5f017e09-efe4-4174-a37c-878bcd9bef20.png)

* 🌻 practice 4 : 
  * step 1 - calculate the fraction of people born each year with the same name
    * calculate the total number of people born in that year in this dataset as year_total.
    * use year_total to calculate the fraction of people born in each year that have each name.
  * step 2 - find the year each name is most common
  ```
  # Loading package
  library(dplyr)
  
  babynames %>%
      group_by(year) %>%
      mutate(year_total = sum(number)) %>%
      ungroup() %>%
      mutate(fraction = number / year_total) %>%
      group_by(name) %>%
      top_n(1, fraction)
  ```
* 🚀 result 4 :
  ```
  # A tibble: 48,040 × 5
  # Groups:   name [48,040]
      year name      number year_total  fraction
     <dbl> <chr>      <int>      <int>     <dbl>
   1  1880 Abbott         5     201478 0.0000248
   2  1880 Abe           50     201478 0.000248 
   3  1880 Abner         27     201478 0.000134 
   4  1880 Adelbert      28     201478 0.000139 
   5  1880 Adella        26     201478 0.000129 
   6  1880 Adolf          6     201478 0.0000298
   7  1880 Adolph        93     201478 0.000462 
   8  1880 Agustus        5     201478 0.0000248
   9  1880 Albert      1493     201478 0.00741  
  10  1880 Albertina      7     201478 0.0000347
  # … with 48,030 more rows
  ```

* 🌻 practice 5 : 
  * step 1 - adding the total and maximum for each name
    * add name_total column, the sum of the number of babies born with that name in the dataset
    * add name_max column, with the maximum number of babies born in any year
  * step 2 - adding the maximum fraction
    * ungroup the table
    * add the fraction_max column containing the number in the year divided by name_max
    * save process result as names_normalized variable
  * step 3 - filter specific names for names_normalized dataset
    * filter the names "Steven", "Thomas", "Matthew" for names_normalized dataset, and as names_filtered variable
  * step 4 - create a line plot to visualize fraction_max over time, colored by name
  ```
  # Loading package
  library(dplyr)

  names_normalized <- babynames %>%
      group_by(name) %>%
      mutate(name_total = sum(number), name_max = max(number)) %>%
      ungroup() %>%
      mutate(fraction_max = number / name_max)
  
  names_normalized
  
  names_filtered <- names_normalized %>%
      filter(name %in% c("Steven", "Thomas", "Matthew"))
      
  ggplot(names_filtered,  aes(x = year, y = fraction_max, color = name)) +
      geom_line()
  ```
* 🚀 result 5 :
  ```
  # A tibble: 332,595 × 6
      year name    number name_total name_max fraction_max
     <dbl> <chr>    <int>      <int>    <int>        <dbl>
   1  1880 Aaron      102     114739    14635     0.00697 
   2  1880 Ab           5         77       31     0.161   
   3  1880 Abbie       71       4330      445     0.160   
   4  1880 Abbott       5        217       51     0.0980  
   5  1880 Abby         6      11272     1753     0.00342 
   6  1880 Abe         50       1832      271     0.185   
   7  1880 Abel         9      10565     3245     0.00277 
   8  1880 Abigail     12      72600    15762     0.000761
   9  1880 Abner       27       1552      199     0.136   
  10  1880 Abraham     81      17882     2449     0.0331  
  # … with 332,585 more rows
  ```
  
  ![image](https://user-images.githubusercontent.com/15766139/185863117-0bdf95f1-7d5b-489f-9a35-6e4b21c17b6f.png)

* 🌻 practice 6 : 
  * Step 1 - practice 4 process result to save as babynames_fraction
  * Step 2 - using ratios to describe the frequency of a name
    * arrange the data in ascending order of name and then year.
    * group by name so that your mutate works within each name
    * add a column ratio containing the ratio (not difference) of fraction between each year
  (notice that the first observation for each name is missing a ratio, since there is no previous year)
  ```
  # Loading package
  library(dplyr)
  
  babynames_fraction <- babynames %>%
      group_by(year) %>%
      mutate(year_total = sum(number)) %>%
      ungroup() %>%
      mutate(fraction = number / year_total) %>%
      group_by(name) %>%
      top_n(1, fraction)
  
  babynames_fraction
  
  babynames_fraction %>%
      arrange(name, year) %>%
      group_by(name) %>%
      mutate(ratio = fraction / lag(fraction))
  ```
* 🚀 result 6 :
  ```  
  # A tibble: 332,595 x 5
      year name    number year_total  fraction
     <dbl> <chr>    <int>      <int>     <dbl>
   1  1880 Aaron      102     201478 0.000506 
   2  1880 Ab           5     201478 0.0000248
   3  1880 Abbie       71     201478 0.000352 
   4  1880 Abbott       5     201478 0.0000248
   5  1880 Abby         6     201478 0.0000298
   6  1880 Abe         50     201478 0.000248 
   7  1880 Abel         9     201478 0.0000447
   8  1880 Abigail     12     201478 0.0000596
   9  1880 Abner       27     201478 0.000134 
  10  1880 Abraham     81     201478 0.000402 
  # ... with 332,585 more rows


  # A tibble: 332,595 x 6
  # Groups:   name [48,040]
      year name    number year_total   fraction  ratio
     <dbl> <chr>    <int>      <int>      <dbl>  <dbl>
   1  2010 Aaban        9    3672066 0.00000245 NA    
   2  2015 Aaban       15    3648781 0.00000411  1.68 
   3  1995 Aadam        6    3652750 0.00000164 NA    
   4  2000 Aadam        6    3767293 0.00000159  0.970
   5  2005 Aadam        6    3828460 0.00000157  0.984
   6  2010 Aadam        7    3672066 0.00000191  1.22 
   7  2015 Aadam       22    3648781 0.00000603  3.16 
   8  2010 Aadan       11    3672066 0.00000300 NA    
   9  2015 Aadan       10    3648781 0.00000274  0.915
  10  2000 Aadarsh      5    3767293 0.00000133 NA    
  # ... with 332,585 more rows
  ```
  
* 🌻 practice 7 : 
  * Step 1 - use practice 6 to filter fraction greater than or equal to 0.00001
  * Step 2 - 
    * extract the largest ratio from each name 
    * sort the ratio column in descending order
    * filtering the fraction column to only display results greater than or equal to 0.001
  ```
  # Loading package
  library(dplyr)
  
  babynames_ratios_filtered <- babynames_fraction %>%
     arrange(name, year) %>%
     group_by(name) %>%
     mutate(ratio = fraction / lag(fraction)) %>%
     filter(fraction >= 0.00001)
     
  babynames_ratios_filtered %>%
      top_n(1, ratio) %>%
      arrange(desc(ratio)) %>%
      filter(fraction >= 0.001)
  ```
* 🚀 result 7 :
  ```  
  # A tibble: 291 x 6
  # Groups:   name [291]
      year name    number year_total fraction ratio
     <dbl> <chr>    <int>      <int>    <dbl> <dbl>
   1  1960 Tammy    14365    4152075  0.00346  70.1
   2  2005 Nevaeh    4610    3828460  0.00120  45.8
   3  1940 Brenda    5460    2301630  0.00237  37.5
   4  1885 Grover     774     240822  0.00321  36.0
   5  1945 Cheryl    8170    2652029  0.00308  24.9
   6  1955 Lori      4980    4012691  0.00124  23.2
   7  2010 Khloe     5411    3672066  0.00147  23.2
   8  1950 Debra     6189    3502592  0.00177  22.6
   9  2010 Bentley   4001    3672066  0.00109  22.4
  10  1935 Marlene   4840    2088487  0.00232  16.8
  # ... with 281 more rows
  ```
