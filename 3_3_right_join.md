# Lesson 3 : Joining Data with dplyr

## 3-3. Right Join

* right join table :
  * ✒ use verb **`right_join()`** function.
    * ✒ can match to use **`replace_na()`** function to replace missing values. (e.g. example 1)
      * For example :
        ```
        replace_na(list(column_name1 = value1))
        ```
    * ✒ or use **`is.na()`** funciton to get contain missing data. (e.g. example 1)
      * For example :
        ```
        is.na(column_name1)
        ```
  * what's different with others join method : only change verb function right_join(), other argument usage same as other join method.
  * result table will contain blue square.
  
    ![image](https://user-images.githubusercontent.com/15766139/186334292-61ca2865-4c1c-4eb0-a62a-8391fac88dbd.png)
  
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
