# Lesson 1 : Introduction to R

## 1-6. Lists
* like a to do list on work.
* __create a list__ :
  * ✒ use **`list()`** function :
  * For example :
    * The arguments to the list function are the list components. 
    * These components can be **matrix, vectors, dataframe, variable, other lists**.
    ```
    # create a list, not named.
    my_list <- list(comp1, comp2 ...)
    
    # create a list, have named.
    my_list <- list(name1 = comp1, name2 = comp2 ...)
    ```
  * 📝 **example** :
    ```
    # create a vector - Vector with numerics from 1 up to 10
    my_vector <- 1:10
    
    # create a matrix - Matrix with numerics from 1 up to 9
    my_matrix <- matrix(1:9, ncol = 3)
    
    # create a dataframe - use scores and comments vectors
    scores <- c(4.6, 5, 4.8, 5, 4.2)
    comments <- c("I would watch it again", "Amazing!", "I liked it", "One of the best movies", "Fascinating plot") 
    
    my_df <- data.frame(scores, comments)
    
    # create a variable - calculate my_vector avarage
    my_avg <- mean(scores)
    
    # create a list - use my_vector and my_matrix
    my_sublist <- list(my_vector, my_matrix)
    
    # Construct list with these different elements (not named)
    my_list <- list(my_vector, my_matrix, my_df, my_avg, my_sublist)
    
    # Construct list with these different elements (have named)
    ## method 1:
    my_list2 <- list(vec = my_vector, mat = my_matrix, df = my_df, avg = my_avg, sublist = my_sublist)
    
    ## method 2:
    my_list2 <- list(my_vector, my_matrix, my_df, my_avg, my_sublist)
    names(my_list2) <- c('vec', 'mat', 'df', 'avg', 'sublist')
    ```
  * 🔎 **result** :
    ```
    my_vector
    1  2  3  4  5  6  7  8  9 10
    
    my_matrix
         [,1] [,2] [,3]
    [1,]    1    4    7
    [2,]    2    5    8
    [3,]    3    6    9
    
    my_df
      scores               comments
    1    4.6 I would watch it again
    2    5.0               Amazing!
    3    4.8             I liked it
    4    5.0 One of the best movies
    5    4.2       Fascinating plot
    
    my_avg
    4.72
    
    my_list
    [[1]]
     [1]  1  2  3  4  5  6  7  8  9 10

    [[2]]
         [,1] [,2] [,3]
    [1,]    1    4    7
    [2,]    2    5    8
    [3,]    3    6    9

    [[3]]
      scores                 comments
    1    4.6   I would watch it again
    2    5.0                 Amazing!
    3    4.8               I liked it
    4    5.0   One of the best movies
    5    4.2         Fascinating plot

    [[4]]
    [1] 4.72
    
    [[5]]
    [[5]][[1]]
     [1]  1  2  3  4  5  6  7  8  9 10

    [[5]][[2]]
         [,1] [,2] [,3]
    [1,]    1    4    7
    [2,]    2    5    8
    [3,]    3    6    9
    
    my_list2
    $vec
     [1]  1  2  3  4  5  6  7  8  9 10

    $mat
         [,1] [,2] [,3]
    [1,]    1    4    7
    [2,]    2    5    8
    [3,]    3    6    9

    $df
      scores               comments
    1    4.6 I would watch it again
    2    5.0               Amazing!
    3    4.8             I liked it
    4    5.0 One of the best movies
    5    4.2       Fascinating plot
    
    $avg
    4.72
    
    $sublist
    $sublist[[1]]
     [1]  1  2  3  4  5  6  7  8  9 10

    $sublist[[2]]
         [,1] [,2] [,3]
    [1,]    1    4    7
    [2,]    2    5    8
    [3,]    3    6    9
    ```
 
* Selecting elements from a list :
  * ✒ use **`[[]]`** or use **`$`** select components, then you can use **`[]`** to get elements of components.
  * 🌟 Note : select elements from vectors, you use single square brackets (i.e. []), Don't mix them up!
  * 📝 **example** :
    ```
    # build shining_list
    shining_list <- list(moviename = mov, actors = act, reviews = rev)
    
    # Print out the list
    shining_list
    
    # Print out all actors 
    ## method 1 :
    shining_list$actors
    
    ## method 2 :
    shining_list[["actors"]]
    
    # Print the second element of the actors
    ## method 1:
    shining_list$actors[2]
    
    ## method 2:
    shining_list[[2]][2]
    ```
  * 🔎 **result** :
    ```
    shining_list
    $moviename
    [1] "The Shining"

    $actors
    [1] "Jack Nicholson"   "Shelley Duvall"   "Danny Lloyd"      "Scatman Crothers"
    [5] "Barry Nelson"    

    $reviews
      scores sources                                              comments
    1    4.5   IMDb1                     Best Horror Film I Have Ever Seen
    2    4.0   IMDb2 A truly brilliant and scary film from Stanley Kubrick
    3    5.0   IMDb3                 A masterpiece of psychological horror
    
    shining_list$actors
    [1] "Jack Nicholson"   "Shelley Duvall"   "Danny Lloyd"      "Scatman Crothers"
    [5] "Barry Nelson"
    
    shining_list[["actors"]]
    [1] "Jack Nicholson"   "Shelley Duvall"   "Danny Lloyd"      "Scatman Crothers"
    [5] "Barry Nelson"
    
    shining_list$actors[2]
    "Shelley Duvall"
    
    shining_list[[2]][2]
    "Shelley Duvall"
    ```
