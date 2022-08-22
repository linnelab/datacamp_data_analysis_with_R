# Lesson 3 : Data Manipulation with dplyr

## 3-4. Windows Function

* __Compare consecutive steps__ :
  * use verb **`lag()`** function.
  * For example :
    ```
    # create a vector
    v <- c(1, 3, 6, 14)
    
    # print out these vector
    v
    
    # print out lag vector result
    lag(v)
    
    # get each value once we've subtracted the previous one
    v - lag(v)
    ```
  * Result :
    ```
    # v
    1   3  6  14
    
    # lag(v)
    NA  1  3  6
    
    # v - lag(v)
    NA  2  3  8
    ```
