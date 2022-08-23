# Lesson 3 : Joining Data with dplyr

## 3-1. Inner Join

* __Inner join one or multiple table__ :
  * use verb **`inner_join()`** function :
    * **table_name1** : put first join table, and all columns of the table will show on the left. 
    * **table_name2** or **table_name3** : put another join table, and all columns of the table will show on the right.
    * **by** : join column name.
    * **suffix** : if two join table contain same column name, will use it to distinguish only same column names.
  * For example :
    * join **one table** and join **column name different**, use **`by = c("col_name1" = "col_name2")`**  (Ref example 1)
      ```
      table_name1 %>%
          inner_join(table_name2, by = c("column_name1" = "column_name2"), suffix = c("_name1", "_name2"))
      ```
    * join **one table** and join **column name same**, use **`by = "col_name"`**   (Ref example 2)
    * can refer to example 2
      ```
      table_name1 %>%
          inner_join(table_name2, by = column_name, suffix = c("_name1", "_name2"))
      ```
    * join **multiple table** : use **`mutiple inner_join()`** function  (Ref example 3)
    * can refer to example 3
      ```
      table_name1 %>%
          inner_join(table_name2, by = c("column_name1" = "column_name2"), suffix = c("_name1", "_name2")) %>%
          inner_join(table_name3, by = c("column_name2" = "column_name3"), suffix = c("_name1", "_name2"))
      ```
  * 📝 **example 1** : 
    ```
    # Print out data source - sets
    sets
    
    # Print out data source - themes
    themes
    
    # Inner join sets and themes tables by theme_id and id column
    sets %>%
        inner_join(themes, by = c("theme_id" = "id"), suffix = c("_set", "_theme"))
        
    # Find most common themes
    sets %>%
        inner_join(themes, by = c("theme_id" = "id"), suffix = c("_set", "_theme")) %>%
        count(name_theme, sort = TRUE)
    ```

  * 🔎 **result 1** :
    ```
    # sets
    # A tibble: 4,977 × 4
       set_num   name                                                       year theme_id
       <chr>     <chr>                                                     <dbl>    <dbl>
     1 700.3-1   Medium Gift Set (ABB)                                      1949      365
     2 700.1.1-1 Single 2 x 4 Brick (ABB)                                   1950      371
     3 700.B.2-1 Single 1 x 2 x 3 Window without Glass (ABB)                1950      371
     4 700.1-2   Extra-Large Gift Set (Mursten)                             1953      366
     5 700.F-1   Automatic Binding Bricks - Small Brick Set (Lego Mursten)  1953      371
     6 700.24-1  Individual 2 x 12 Bricks                                   1954      371
     7 700.C.1-1 Individual 1 x 6 x 4 Panorama Window (with glass)          1954      371
     8 700.C.4-1 Individual 1 x 4 x 3 Window (with glass)                   1954      371
     9 700.H-1   Individual 4 x 4 Corner Bricks                             1954      371
    10 1200-1    LEGO Town Plan Board, Large Plastic                        1955      372
    # … with 4,967 more rows
    
    
    # themes
    # A tibble: 665 × 3
          id name           parent_id
       <dbl> <chr>              <dbl>
     1     1 Technic               NA
     2     2 Arctic Technic         1
     3     3 Competition            1
     4     4 Expert Builder         1
     5     5 Model                  1
     6     6 Airport                5
     7     7 Construction           5
     8     8 Farm                   5
     9     9 Fire                   5
    10    10 Harbor                 5
    # … with 655 more rows
    

    # inner join
    # A tibble: 4,977 × 6
       set_num   name_set                                                   year theme_id name_theme   parent_id
       <chr>     <chr>                                                     <dbl>    <dbl> <chr>            <dbl>
     1 700.3-1   Medium Gift Set (ABB)                                      1949      365 System              NA
     2 700.1.1-1 Single 2 x 4 Brick (ABB)                                   1950      371 Supplemental       365
     3 700.B.2-1 Single 1 x 2 x 3 Window without Glass (ABB)                1950      371 Supplemental       365
     4 700.1-2   Extra-Large Gift Set (Mursten)                             1953      366 Basic Set          365
     5 700.F-1   Automatic Binding Bricks - Small Brick Set (Lego Mursten)  1953      371 Supplemental       365
     6 700.24-1  Individual 2 x 12 Bricks                                   1954      371 Supplemental       365
     7 700.C.1-1 Individual 1 x 6 x 4 Panorama Window (with glass)          1954      371 Supplemental       365
     8 700.C.4-1 Individual 1 x 4 x 3 Window (with glass)                   1954      371 Supplemental       365
     9 700.H-1   Individual 4 x 4 Corner Bricks                             1954      371 Supplemental       365
    10 1200-1    LEGO Town Plan Board, Large Plastic                        1955      372 Town Plan          365
    # … with 4,967 more rows
    
    # count
    # A tibble: 419 × 2
       name_theme        n
       <chr>         <int>
     1 Supplemental    180
     2 Basic Set       171
     3 Technic         144
     4 Friends         133
     5 Gear            122
     6 City            120
     7 Town            117
     8 Ninjago          95
     9 Service Packs    94
    10 Star Wars        94
    # … with 409 more rows
    ```
    
  * 📝 **example 2** : 
    ```
    # Print out data source - parts
    parts
    
    # Print out data source - inventory_parts
    inventory_parts
    
    # Inner join parts and inventory_parts tables by part_num column
    parts %>%
        inner_join(inventory_parts, by = "part_num")
    ```

  * 🔎 **result 2** :
    ```
    # parts
    # A tibble: 17,501 × 3
       part_num   name                                                      part_cat_id
       <chr>      <chr>                                                           <dbl>
     1 0901       Baseplate 16 x 30 with Set 080 Yellow House Print                   1
     2 0902       Baseplate 16 x 24 with Set 080 Small White House Print              1
     3 0903       Baseplate 16 x 24 with Set 080 Red House Print                      1
     4 0904       Baseplate 16 x 24 with Set 080 Large White House Print              1
     5 1          Homemaker Bookcase 2 x 4 x 4                                        7
     6 10016414   Sticker Sheet #1 for 41055-1                                       58
     7 10026stk01 Sticker for Set 10026 - (44942/4184185)                            58
     8 10039      Pullback Motor 8 x 4 x 2/3                                         44
     9 10048      Minifig Hair Tousled                                               65
    10 10049      Minifig Shield Broad with Spiked Bottom and Cutout Corner          27
    # … with 17,491 more rows
    
    # inventory_parts
    # A tibble: 258,958 × 4
       inventory_id part_num             color_id quantity
              <dbl> <chr>                   <dbl>    <dbl>
     1           21 3009                        7       50
     2           25 21019c00pat004pr1033       15        1
     3           25 24629pr0002                78        1
     4           25 24634pr0001                 5        1
     5           25 24782pr0001                 5        1
     6           25 88646                       0        1
     7           25 973pr3314c01                5        1
     8           26 14226c11                    0        3
     9           26 2340px2                    15        1
    10           26 2340px3                    15        1
    # … with 258,948 more rows
    
    # inner join 
    # A tibble: 258,958 × 6
       part_num name                                                   part_cat_id inventory_id color_id quantity
       <chr>    <chr>                                                        <dbl>        <dbl>    <dbl>    <dbl>
     1 0901     Baseplate 16 x 30 with Set 080 Yellow House Print                1         1973        2        1
     2 0902     Baseplate 16 x 24 with Set 080 Small White House Print           1         1973        2        1
     3 0903     Baseplate 16 x 24 with Set 080 Red House Print                   1         1973        2        1
     4 0904     Baseplate 16 x 24 with Set 080 Large White House Print           1         1973        2        1
     5 1        Homemaker Bookcase 2 x 4 x 4                                     7          508       15        1
     6 1        Homemaker Bookcase 2 x 4 x 4                                     7         1158       15        2
     7 1        Homemaker Bookcase 2 x 4 x 4                                     7         6590       15        2
     8 1        Homemaker Bookcase 2 x 4 x 4                                     7         9679       15        2
     9 1        Homemaker Bookcase 2 x 4 x 4                                     7        12256        1        2
    10 1        Homemaker Bookcase 2 x 4 x 4                                     7        13356       15        1
    # … with 258,948 more rows
    ```
    
  * 📝 **example 3** : 
    * join multiple tables can refer to the table schema :
    
      ![image](https://user-images.githubusercontent.com/15766139/186061431-dbad976c-089b-491a-8400-35f778558895.png)
    
    ```
    # Print out data source - inventories
    inventories
    
    # Print out data source - colors
    colors
    
    # Inner join mutiple tables
    sets %>%
        inner_join(inventories, by = "set_num") %>%
        inner_join(inventory_parts, by = c("id" = "inventory_id")) %>%
        inner_join(colors, by = c("color_id" = "id"), suffix = c("_set", "_color"))
        
    # Find the most common color
    ## Count the name_color column and sort the results so the most prominent colors appear first.
    sets %>%
        inner_join(inventories, by = "set_num") %>%
        inner_join(inventory_parts, by = c("id" = "inventory_id")) %>%
        inner_join(colors, by = c("color_id" = "id"), suffix = c("_set", "_color")) %>%
        count(name_color, sort = TRUE)
    ```

  * 🔎 **result 3** :
    ```
    # inventories
    # A tibble: 15,174 × 3
          id version set_num 
       <dbl>   <dbl> <chr>   
     1     1       1 7922-1  
     2     3       1 3931-1  
     3     4       1 6942-1  
     4    15       1 5158-1  
     5    16       1 903-1   
     6    17       1 850950-1
     7    19       1 4444-1  
     8    21       1 3474-1  
     9    22       1 30277-1 
    10    25       1 71012-11
    # … with 15,164 more rows
    
    # colors
    # A tibble: 179 × 3
          id name           rgb    
       <dbl> <chr>          <chr>  
     1    -1 [Unknown]      #0033B2
     2     0 Black          #05131D
     3     1 Blue           #0055BF
     4     2 Green          #237841
     5     3 Dark Turquoise #008F9B
     6     4 Red            #C91A09
     7     5 Dark Pink      #C870A0
     8     6 Brown          #583927
     9     7 Light Gray     #9BA19D
    10     8 Dark Gray      #6D6E5C
    # … with 169 more rows
    
    # inner join
    # A tibble: 258,958 × 11
       set_num name_set               year theme_id    id version part_num color_id quantity name_color rgb    
       <chr>   <chr>                 <dbl>    <dbl> <dbl>   <dbl> <chr>       <dbl>    <dbl> <chr>      <chr>  
     1 700.3-1 Medium Gift Set (ABB)  1949      365 24197       1 bdoor01         2        2 Green      #237841
     2 700.3-1 Medium Gift Set (ABB)  1949      365 24197       1 bdoor01        15        1 White      #FFFFFF
     3 700.3-1 Medium Gift Set (ABB)  1949      365 24197       1 bdoor01         4        1 Red        #C91A09
     4 700.3-1 Medium Gift Set (ABB)  1949      365 24197       1 bslot02        15        6 White      #FFFFFF
     5 700.3-1 Medium Gift Set (ABB)  1949      365 24197       1 bslot02         2        6 Green      #237841
     6 700.3-1 Medium Gift Set (ABB)  1949      365 24197       1 bslot02         4        6 Red        #C91A09
     7 700.3-1 Medium Gift Set (ABB)  1949      365 24197       1 bslot02         1        6 Blue       #0055BF
     8 700.3-1 Medium Gift Set (ABB)  1949      365 24197       1 bslot02        14        6 Yellow     #F2CD37
     9 700.3-1 Medium Gift Set (ABB)  1949      365 24197       1 bslot02a       15        6 White      #FFFFFF
    10 700.3-1 Medium Gift Set (ABB)  1949      365 24197       1 bslot02a        2        6 Green      #237841
    # … with 258,948 more rows
    
    # count
    # A tibble: 134 × 2
       name_color            n
       <chr>             <int>
     1 Black             48068
     2 White             30105
     3 Light Bluish Gray 26024
     4 Red               21602
     5 Dark Bluish Gray  19948
     6 Yellow            17088
     7 Blue              12980
     8 Light Gray         8632
     9 Reddish Brown      6960
    10 Tan                6664
    # … with 124 more rows
    ```
