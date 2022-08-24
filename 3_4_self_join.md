# Lesson 3 : Joining Data with dplyr

## 3-4. Self Join

* self join table :
  * ✒ use verb **`inner_join()`** function.
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
  * diff with others join : usage same as inner_join(), but it use self table join itself.
  
  * 📝 **example 1** : 
    ```
    # 
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
