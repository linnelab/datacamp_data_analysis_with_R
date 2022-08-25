# Lesson 3 : Joining Data with dplyr

## 3-5. Full Join

* full join table :
  * ✒ use verb **`full_join()`** function.

    ![image](https://user-images.githubusercontent.com/15766139/186569630-f2525d85-04da-4c81-9a45-a49389fc940e.png) 

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
