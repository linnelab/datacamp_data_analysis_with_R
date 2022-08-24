# Lesson 3 : Joining Data with dplyr

## 3-2. Left Join

* left join table :
  * use verb **`left_join()`** function.
  * For example :
    * join **one column** and **column name** of two tables are **same**.
      ```
      first_table >%>
          left_join(second_table, by = column_name, suffix = c("_name1", "_name2"))
      ```
    * join **mutiple column** and **column name** of two tables are **same**.
      ```
      first_table >%>
          left_join(second_table, by = c("column_name1", "column_name2"), suffix = c("_name1", "_name2"))    
      ```
  * diff with inner_join() : only change verb function from inner_join() to left_join(), other argument usage same as inner_join().
  * result table will contain blue square.
  
    ![image](https://user-images.githubusercontent.com/15766139/186307141-dc1063d9-02c3-4dd6-a062-7b92fcd8fa5b.png)
    
  * 📝 **example 1** : 
    ```
    # Aggregate Millennium Falcon for the total quantity in each part
    millennium_falcon_colors <- millennium_falcon %>%
        group_by(color_id) %>%
        summarize(total_quantity = sum(quantity))
    
    # Print out aggregate result
    millennium_falcon_colors
    
    # Aggregate Star Destroyer for the total quantity in each part
    star_destroyer_colors <- star_destroyer %>%
        group_by(color_id) %>%
        summarize(total_quantity = sum(quantity))
    
    # Print out aggregate result
    star_destroyer_colors
    
    # Left join the Millennium Falcon colors to the Star Destroyer colors
    millennium_falcon_colors %>%
        left_join(star_destroyer_colors, by = "color_id", suffix = c("_falcon", "_star_destroyer"))
    ```
  * 🔎 **result 1** :
    ```
    # millennium_falcon_colors
    # A tibble: 21 × 2
       color_id total_quantity
          <dbl>          <dbl>
     1        0            201
     2        1             15
     3        4             17
     4       14              3
     5       15             15
     6       19             95
     7       28              3
     8       33              5
     9       36              1
    10       41              6
    # … with 11 more rows
    
    # star_destroyer_colors
    # A tibble: 20 × 2
       color_id total_quantity
          <dbl>          <dbl>
     1        0            336
     2        1             23
     3        4             53
     4       14              4
     5       15             17
     6       19             12
     7       25              1
     8       28             16
     9       35             16
    10       36             14
    11       41             15
    12       57              1
    13       70              1
    14       71            517
    15       72            370
    16       78              5
    17      148              3
    18      297              2
    19      320              2
    20     9999              1
    
    # left join result
    # A tibble: 21 × 3
       color_id total_quantity_falcon total_quantity_star_destroyer
          <dbl>                 <dbl>                         <dbl>
     1        0                   201                           336
     2        1                    15                            23
     3        4                    17                            53
     4       14                     3                             4
     5       15                    15                            17
     6       19                    95                            12
     7       28                     3                            16
     8       33                     5                            NA
     9       36                     1                            14
    10       41                     6                            15
    # … with 11 more rows
    ```
    
  * 📝 **example 2** : 
    ```
    # Combine the star_destroyer and millennium_falcon tables
    millennium_falcon %>%
        left_join(star_destroyer, by = c("part_num", "color_id"), suffix = c("_falcon", "_star_destroyer"))
    ```
  * 🔎 **result 2** :
    ```
    # millennium_falcon
    # A tibble: 263 × 4
       set_num part_num color_id quantity
       <chr>   <chr>       <dbl>    <dbl>
     1 7965-1  63868          71       62
     2 7965-1  3023            0       60
     3 7965-1  3021           72       46
     4 7965-1  2780            0       37
     5 7965-1  60478          72       36
     6 7965-1  6636           71       34
     7 7965-1  3009           71       28
     8 7965-1  3665           71       22
     9 7965-1  2412b          72       20
    10 7965-1  3010           71       19
    # … with 253 more rows
    # star_destroyer
    # A tibble: 293 × 4
       set_num part_num color_id quantity
       <chr>   <chr>       <dbl>    <dbl>
     1 75190-1 6141           72       66
     2 75190-1 3020            0       38
     3 75190-1 2780            0       36
     4 75190-1 3710           72       34
     5 75190-1 3666           71       26
     6 75190-1 3069b          72       18
     7 75190-1 99563          71       18
     8 75190-1 98286          71       17
     9 75190-1 3020           71       16
    10 75190-1 6141           35       16
    # … with 283 more rows
    
    
    # A tibble: 263 × 6
       set_num_falcon part_num color_id quantity_falcon set_num_star_destroyer
       <chr>          <chr>       <dbl>           <dbl> <chr>                 
     1 7965-1         63868          71              62 <NA>                  
     2 7965-1         3023            0              60 <NA>                  
     3 7965-1         3021           72              46 75190-1               
     4 7965-1         2780            0              37 75190-1               
     5 7965-1         60478          72              36 <NA>                  
     6 7965-1         6636           71              34 75190-1               
     7 7965-1         3009           71              28 75190-1               
     8 7965-1         3665           71              22 <NA>                  
     9 7965-1         2412b          72              20 75190-1               
    10 7965-1         3010           71              19 <NA>                  
    # … with 253 more rows, and 1 more variable: quantity_star_destroyer <dbl>
    ```
