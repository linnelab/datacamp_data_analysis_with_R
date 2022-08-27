# Lesson 2 : Introduction to data transform with dplyr

## 2-5. Join data

* Method :
  
  |name       |verb function|
  |-----------|-------------|
  |inner join |inner_join() |
  |self  join |inner_join() |
  |left  join |left_join()  |
  |right join |right_join() |
  |full  join |full_join()  |
  |semi  join |semi_join()  |
  |anti  join |anti_join()  |
  
  ![image](https://user-images.githubusercontent.com/15766139/187019210-663644e9-e406-4fe9-931d-be13ed3efeee.png)

* Sample :
  * inner join :
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

  * self join :
    * use inner_join() function, and join table to itself
    * 📝 **example 1** : 
      ```
      # Join themes to itself again to find the child relationships
      themes %>% 
          inner_join(themes, by = c("id" = "parent_id"), suffix = c("_parent", "_child"))

      # Join themes to itself again to find the grandchild relationships
      themes %>% 
          inner_join(themes, by = c("id" = "parent_id"), suffix = c("_parent", "_child")) %>%
          inner_join(themes, by = c("id_child" = "parent_id"), suffix = c("_parent", "_grandchild"))
      ```      
    * 🔎 **result 1** :
      ```
      # A tibble: 544 × 5
            id name_parent parent_id id_child name_child            
         <dbl> <chr>           <dbl>    <dbl> <chr>                 
       1     1 Technic            NA        2 Arctic Technic        
       2     1 Technic            NA        3 Competition           
       3     1 Technic            NA        4 Expert Builder        
       4     1 Technic            NA        5 Model                 
       5     1 Technic            NA       16 RoboRiders            
       6     1 Technic            NA       17 Speed Slammers        
       7     1 Technic            NA       18 Star Wars             
       8     1 Technic            NA       19 Supplemental          
       9     1 Technic            NA       20 Throwbot Slizer       
      10     1 Technic            NA       21 Universal Building Set
      # … with 534 more rows

      # A tibble: 158 × 7
         id_parent name_parent parent_id id_child name_child id_grandchild name       
             <dbl> <chr>           <dbl>    <dbl> <chr>              <dbl> <chr>      
       1         1 Technic            NA        5 Model                  6 Airport    
       2         1 Technic            NA        5 Model                  7 Constructi…
       3         1 Technic            NA        5 Model                  8 Farm       
       4         1 Technic            NA        5 Model                  9 Fire       
       5         1 Technic            NA        5 Model                 10 Harbor     
       6         1 Technic            NA        5 Model                 11 Off-Road   
       7         1 Technic            NA        5 Model                 12 Race       
       8         1 Technic            NA        5 Model                 13 Riding Cyc…
       9         1 Technic            NA        5 Model                 14 Robot      
      10         1 Technic            NA        5 Model                 15 Traffic    
      # … with 148 more rows
      ```
  * left join :
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
  * right join :
    * 📝 **example 1** : 
      ```
      # Print out parts dataset
      parts

      # Print out part_categories dataset
      part_categories

      # Show data contain missing value in the n column
      parts %>%
          count(part_cat_id) %>%
          right_join(part_categories, by = c("part_cat_id" = "id")) %>%
          filter(is.na(n))

      # replace missing value to zero in the n column
      ## Use replace_na to replace missing values in the n column
      parts %>%
          count(part_cat_id) %>%
          right_join(part_categories, by = c("part_cat_id" = "id")) %>%
          replace_na(list(n = 0))
      ```
    * 🔎 **result 1** :
      ```
      # parts
      # A tibble: 17,501 × 3
         part_num   name                                                   part_cat_id
         <chr>      <chr>                                                        <dbl>
       1 0901       Baseplate 16 x 30 with Set 080 Yellow House Print                1
       2 0902       Baseplate 16 x 24 with Set 080 Small White House Print           1
       3 0903       Baseplate 16 x 24 with Set 080 Red House Print                   1
       4 0904       Baseplate 16 x 24 with Set 080 Large White House Print           1
       5 1          Homemaker Bookcase 2 x 4 x 4                                     7
       6 10016414   Sticker Sheet #1 for 41055-1                                    58
       7 10026stk01 Sticker for Set 10026 - (44942/4184185)                         58
       8 10039      Pullback Motor 8 x 4 x 2/3                                      44
       9 10048      Minifig Hair Tousled                                            65
      10 10049      Minifig Shield Broad with Spiked Bottom and Cutout Co…          27
      # … with 17,491 more rows


      # part_categories
      # A tibble: 64 × 2
            id name                   
         <dbl> <chr>                  
       1     1 Baseplates             
       2     3 Bricks Sloped          
       3     4 Duplo, Quatro and Primo
       4     5 Bricks Special         
       5     6 Bricks Wedged          
       6     7 Containers             
       7     8 Technic Bricks         
       8     9 Plates Special         
       9    11 Bricks                 
      10    12 Technic Connectors     
      # … with 54 more rows


      # right join + is.na()
      # A tibble: 1 × 3
        part_cat_id     n name   
              <dbl> <int> <chr>  
      1          66    NA Modulex


      # right join + replace_na
      # A tibble: 64 × 3
         part_cat_id     n name                   
               <dbl> <dbl> <chr>                  
       1           1   135 Baseplates             
       2           3   303 Bricks Sloped          
       3           4  1900 Duplo, Quatro and Primo
       4           5   107 Bricks Special         
       5           6   128 Bricks Wedged          
       6           7    97 Containers             
       7           8    24 Technic Bricks         
       8           9   167 Plates Special         
       9          11   490 Bricks                 
      10          12    85 Technic Connectors     
      # … with 54 more rows
      ```
  * full join :
    * 📝 **example 1** : 
      ```
      # Count the part number and color id, weight by quantity
      batman_parts <- batman %>%
          count(part_num, color_id, wt = quantity)

      # Print out batman_parts
      batman_parts

      # Count the part number and color id, weight by quantity
      star_wars_parts <- star_wars %>%
          count(part_num, color_id, wt = quantity)

      # Print out star_wars_parts
      star_wars_parts

      # Combine the star_wars_parts table 
      # Replace NAs with 0s in the n_batman and n_star_wars columns 
      batman_parts %>%
          full_join(star_wars_parts, by = c("part_num", "color_id"), suffix = c("_batman", "_star_wars")) %>%
          replace_na(list(n_batman = 0, n_star_wars = 0))
      ```   
    
    * 🔎 **result 1** :
      ```
      # batman_parts
      # A tibble: 2,071 × 3
         part_num color_id     n
         <chr>       <dbl> <dbl>
       1 10113           0    11
       2 10113         272     1
       3 10113         320     1
       4 10183          57     1
       5 10190           0     2
       6 10201           0     1
       7 10201           4     3
       8 10201          14     1
       9 10201          15     6
      10 10201          71     4
      # … with 2,061 more rows

      # star_wars_parts
      # A tibble: 2,413 × 3
         part_num color_id     n
         <chr>       <dbl> <dbl>
       1 10169           4     1
       2 10197           0     2
       3 10197          72     3
       4 10201           0    21
       5 10201          71     5
       6 10247           0     9
       7 10247          71    16
       8 10247          72    12
       9 10884          28     1
      10 10928          72     6
      # … with 2,403 more rows

      # full join
      # A tibble: 3,628 × 4
         part_num color_id n_batman n_star_wars
         <chr>       <dbl>    <dbl>       <dbl>
       1 10113           0       11           0
       2 10113         272        1           0
       3 10113         320        1           0
       4 10183          57        1           0
       5 10190           0        2           0
       6 10201           0        1          21
       7 10201           4        3           0
       8 10201          14        1           0
       9 10201          15        6           0
      10 10201          71        4           5
      # … with 3,618 more rows
      ```
      
  * semi join :
    * 📝 **example 1** : 
      ```
      batmobile <- inventory_parts_joined %>%
          filter(set_num == "7784-1") %>%
          select(-set_num)

      # Print out batmobile
      batmobile

      # Filter the batwing set for parts that are also in the batmobile set
      batwing %>%
          semi_join(batmobile, by = "part_num")
      ```   

    * 🔎 **result 1** :
      ```
      # batmobile
      # A tibble: 173 × 3
         part_num color_id quantity
         <chr>       <dbl>    <dbl>
       1 3023           72       62
       2 2780            0       28
       3 50950           0       28
       4 3004           71       26
       5 43093           1       25
       6 3004            0       23
       7 3010            0       21
       8 30363           0       21
       9 32123b         14       19
      10 3622            0       18
      # … with 163 more rows

      # semi join
      # A tibble: 126 × 3
         part_num color_id quantity
         <chr>       <dbl>    <dbl>
       1 3023            0       22
       2 3024            0       22
       3 3623            0       20
       4 2780            0       17
       5 3666            0       16
       6 3710            0       14
       7 6141            4       12
       8 2412b          71       10
       9 6141           72       10
      10 6558            1        9
      # … with 116 more rows
      ```
      
  * anti join :
    * 📝 **example 1** : 
      ```
      batwing <- inventory_parts_joined %>%
          filter(set_num == "70916-1") %>%
          select(-set_num)

      # Print out batmobile
      batwing

      # Filter the batwing set for parts that aren't in the batmobile set
      batwing %>%
          anti_join(batmobile, by = "part_num")
      ```   

    * 🔎 **result 1** :
      ```
      # batwing
      # A tibble: 309 × 3
         part_num color_id quantity
         <chr>       <dbl>    <dbl>
       1 3023            0       22
       2 3024            0       22
       3 3623            0       20
       4 11477           0       18
       5 99207          71       18
       6 2780            0       17
       7 3666            0       16
       8 22385           0       14
       9 3710            0       14
      10 99563           0       13
      # … with 299 more rows

      # anti join
      # A tibble: 183 × 3
         part_num color_id quantity
         <chr>       <dbl>    <dbl>
       1 11477           0       18
       2 99207          71       18
       3 22385           0       14
       4 99563           0       13
       5 10247          72       12
       6 2877           72       12
       7 61409          72       12
       8 11153           0       10
       9 98138          46       10
      10 2419           72        9
      # … with 173 more rows
      ```
