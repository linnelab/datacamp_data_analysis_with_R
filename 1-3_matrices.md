# Lesson 1 : Introduction to R

## 1-3. Matrices
* Matrics like two dimention array or dataframe
* __create a matrix__ :
  * ✒ use **`matrix()`** function
    * the first argument : 1:9, 
                           <br>is the collection of elements will arrange into the rows and columns of the matrix. 
                           <br>Here, we use 1:9 which is a shortcut for c(1, 2, 3, 4, 5, 6, 7, 8, 9).</br>
    * the second argument : <br>byrow = **`TRUE`**, indicates that the matrix is **filled by the `rows`**.
                            <br>byrow = **`FALSE`**, indicates that the matrix is **filled by the `columns`**.</br>
  * 📝 **example** :
    ```
    # Construct a matrix with 3 rows that contain the numbers 1 up to 9
    matrix(1:9, byrow = TRUE, nrow = 3)
    matrix(1:9, byrow = FALSE, nrow = 3)
    ```
  * 🔎 **result** :
    ```
         [,1] [,2] [,3]
    [1,]    1    2    3
    [2,]    4    5    6
    [3,]    7    8    9
    
          [,1] [,2] [,3]
    [1,]    1    4    7
    [2,]    2    5    8
    [3,]    3    6    9   
    ```

* __vectors convert to matrix__ :
  * 📝 **example** :
    ```
    # Box office Star Wars (in millions!)
    new_hope <- c(460.998, 314.4)
    empire_strikes <- c(290.475, 247.900)
    return_jedi <- c(309.306, 165.8)
    
    # Create box_office
    box_office <- c(new_hope, empire_strikes, return_jedi)
    
    # Print out the value of the variable box_office
    box_office
    
    # Construct star_wars_matrix
    star_wars_matrix <- matrix(box_office, byrow = TRUE, nrow = 3)
    
    # Print out the value of the variable star_wars_matrix
    star_wars_matrix
    ```
  * 🔎 **result** :
    ```
    box_office 
    460.998 314.400 290.475 247.900 309.306 165.800
    
    star_wars_matrix
            [,1]  [,2]
    [1,] 460.998 314.4
    [2,] 290.475 247.9
    [3,] 309.306 165.8
    ```

* __Naming a matrix__ :
  * ✒ name the columns : use **`colnames()`** function
  * ✒ name the rows : use **`rownames()`** function
  * 📝 **example** :
    ```
    # Box office Star Wars (in millions!)
    new_hope <- c(460.998, 314.4)
    empire_strikes <- c(290.475, 247.900)
    return_jedi <- c(309.306, 165.8)
    
    # Construct matrix
    star_wars_matrix <- matrix(c(new_hope, empire_strikes, return_jedi), byrow = TRUE, nrow = 3)
    
    # Vectors region and titles, used for naming
    region <- c("US", "non-US")
    titles <- c("A New Hope", "The Empire Strikes Back", "Return of the Jedi")
    
    # Name the columns with region
    colnames(star_wars_matrix) <- region
    
    # Name the rows with region
    rownames(star_wars_matrix) <- titles
    
    # Print out star_wars_matrix
    star_wars_matrix
    ```
  * 🔎 **result** :
    ```
                            US       non-US
    A New Hope              460.998  314.4
    The Empire Strikes Back 290.475  247.9
    Return of the Jedi      309.306  165.8
    ```

* __calculates matrix__ :
  * calculates the totals for each **`row`** : use **`rowSums()`**
    * 📝 **example** :
      ```
      # Construct star_wars_matrix
      box_office <- c(460.998, 314.4, 290.475, 247.900, 309.306, 165.8)

      # row name
      region <- c("US", "non-US")

      # column name
      titles <- c("A New Hope", "The Empire Strikes Back", "Return of the Jedi")

      # Construct star_wars_matrix 
      star_wars_matrix <- matrix(box_office, byrow = TRUE, nrow = 3, dimnames = list(region, titles))

      # Print out star_wars_matrix
      star_wars_matrix

      # Calculate worldwide box office figures
      worldwide_vector <- rowSums(star_wars_matrix)

      # Print out star_wars_matrix
      worldwide_vector
      ```
    * 🔎 **result** :
      ``` 
      star_wars_matrix
                              US       non-US
      A New Hope              460.998  314.4
      The Empire Strikes Back 290.475  247.9
      Return of the Jedi      309.306  165.8
      
      worldwide_vector
      A New Hope     The Empire Strikes Back      Return of the Jedi 
      775.398        538.375                      475.106 
      ```
      
  * calculates the totals for each **`column`** : use **`colSums()`**
    * 📝 **example** :
      ```
      # Print out star_wars_matrix
      star_wars_matrix
      
      # calculate region total
      region_vector <- colSums(star_wars_matrix)
      
      # Print out region_vector
      region_vector
      ```
    * 🔎 **result** :
      ```  
      star_wars_matrix
                              US       non-US
      A New Hope              460.998  314.4
      The Empire Strikes Back 290.475  247.9
      Return of the Jedi      309.306  165.8
      
      region_vector
      US        non-US 
      1060.779  728.100 
      ```
    
