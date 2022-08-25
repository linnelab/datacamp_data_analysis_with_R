# Lesson 3 : Joining Data with dplyr

## 3-5. Semi and Anti Join

* Semi join table :
  * ✒ use verb **`semi_join()`** function.

    ![image](https://user-images.githubusercontent.com/15766139/186570647-9fd350ca-b3f3-41bf-b9b7-75f9872d8617.png)

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
    
* Anti join table :
  * ✒ use verb **`anti_join()`** function.

    ![image](https://user-images.githubusercontent.com/15766139/186570768-ce21f027-e737-4588-862d-cd7dae0165c5.png)

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
