# Lesson 1 : Introduction to R

## 1-3. Matrices
* **(two dimensional array)** can hold numeric, character or logical values. The elements in a matrix all have the **same data type**.
* __create a matrix__ :
  * ✒ use **`matrix()`** function
    * the first argument : <br>is the collection of **elements** will arrange into the rows and columns of the matrix. 
                           <br>Here, we use 1:9 which is a shortcut for c(1, 2, 3, 4, 5, 6, 7, 8, 9).</br>
    * the second argument : <br>**byrow = `TRUE`**, indicates that the matrix is **filled by the `rows`**.
                            <br>**byrow = `FALSE`**, indicates that the matrix is **filled by the `columns`**.</br>
    * the third argument : <br>**`nrow` = 3**, indicates that the matrix should have **`row counts`**.
    * the fourth argument : <br>**`dimnames = list(row_vector1, column_vector2)`**, to set columns and rows name of matrix.
    
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
  * ✒ calculates the totals for each **`row`** : use **`rowSums()`**
  * ✒ also can use **`dimnames = list(row_vector1, column_vector2)`** argument to set columns and rows name.
    * 📝 **example** :
      ```
      # Construct star_wars_matrix
      box_office <- c(460.998, 314.4, 290.475, 247.900, 309.306, 165.8)

      # row name
      region <- c("US", "non-US")

      # column name
      titles <- c("A New Hope", "The Empire Strikes Back", "Return of the Jedi")

      # Construct star_wars_matrix 
      star_wars_matrix <- matrix(box_office, byrow = TRUE, nrow = 3, dimnames = list(titles, region))

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
      
  * ✒ calculates the totals for each **`column`** : use **`colSums()`**
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
 
* __add a column(row) or multiple columns(row) to a matrix__ :
  * ✒ use **`cbind()`** function : 
    * which merges matrices and/or vectors together by **`column`**. 
    * **`For example: big_matrix <- cbind(matrix1, matrix2, vector1 ...)`**
    * 📝 **example** :
      ```
      # Construct star_wars_matrix
      box_office <- c(460.998, 314.4, 290.475, 247.900, 309.306, 165.8)
      region <- c("US", "non-US")
      titles <- c("A New Hope", "The Empire Strikes Back", "Return of the Jedi")
      star_wars_matrix <- matrix(c(box_office), byrow = TRUE, nrow = 3, dimnames = list(titles, region))
      star_wars_matrix
      worldwide_vector <- rowSums(star_wars_matrix)
      worldwide_vector

      # Bind the new variable worldwide_vector as a column to star_wars_matrix
      all_wars_matrix <- cbind(star_wars_matrix, worldwide_vector)

      # Print out all_wars_matrix
      all_wars_matrix
      ```
     * 🔎 **result** :
       ```
       star_wars_matrix
                               US       non-US
       A New Hope              460.998  314.4
       The Empire Strikes Back 290.475  247.9
       Return of the Jedi      309.306  165.8

       worldwide_vector
       A New Hope The Empire   Strikes Back      Return of the Jedi 
       775.398                 538.375           475.106 

       all_wars_matrix
                               US       non-US     worldwide_vector
       A New Hope              460.998  314.4      775.398
       The Empire Strikes Back 290.475  247.9      538.375
       Return of the Jedi      309.306  165.8      475.106
       ```
  * ✒ use **`rbind()`** function : 
    * which combine matrices and/or vectors together by **`row`**. 
    * **`For example: big_matrix <- rbind(matrix1, matrix2, vector1 ...)`**
    * 📝 **example** :
      ```
      # star_wars_matrix and star_wars_matrix2 are available in your workspace
      star_wars_matrix  
      star_wars_matrix2 

      # Combine both Star Wars trilogies in one matrix
      all_wars_matrix <- rbind(star_wars_matrix, star_wars_matrix2)

      # Print out all_wars_matrix
      all_wars_matrix
      ```
     * 🔎 **result** :
       ```
       star_wars_matrix  
                               US     non-US
       A New Hope              461.0  314.4
       The Empire Strikes Back 290.5  247.9
       Return of the Jedi      309.3  165.8

       star_wars_matrix2 
                               US     non-US
       The Phantom Menace      474.5  552.5
       Attack of the Clones    310.7  338.7
       Revenge of the Sith     380.3  468.5

       all_wars_matrix
                               US     non-US
       A New Hope              461.0  314.4
       The Empire Strikes Back 290.5  247.9
       Return of the Jedi      309.3  165.8
       The Phantom Menace      474.5  552.5
       Attack of the Clones    310.7  338.7
       Revenge of the Sith     380.3  468.5
       ```
      
* Selection of matrix elements :
  * ✒ use **`[rows, columns]`**
  * **For example** :
    ```
    * my_matrix[1,2] : selects the element at the first row and second column.
    * my_matrix[1:3,2:4] : results return a matrix with the data on the rows 1, 2, 3 and columns 2, 3, 4.
    * my_matrix[,1] : selects all elements of the first column.
    * my_matrix[1,] : selects all elements of the first row.
    ```
  * 📝 **example** :
    ```
    # all_wars_matrix is available in your workspace
    all_wars_matrix

    # Select the non-US revenue for all movies
    non_us_all <- all_wars_matrix[, 2]

    # Print out non_us_all
    non_us_all

    # Average non-US revenue
    mean(non_us_all)

    # Select the non-US revenue for first two movies
    non_us_some <- all_wars_matrix[1:2, 2]

    # Print out non_us_some
    non_us_some

    # Average non-US revenue for first two movies
    mean(non_us_some)
    ```
  * 🔎 **result** :
    ``` 
    all_wars_matrix
                            US     non-US
    A New Hope              461.0  314.4
    The Empire Strikes Back 290.5  247.9
    Return of the Jedi      309.3  165.8
    The Phantom Menace      474.5  552.5
    Attack of the Clones    310.7  338.7
    Revenge of the Sith     380.3  468.5

    non_us_all
    A New Hope             The Empire Strikes Back      Return of the Jedi 
    314.4                  247.9                        165.8 
    The Phantom Menace     Attack of the Clones         Revenge of the Sith 
    552.5                  338.7                        468.5 

    mean(non_us_all)
    347.9667

    non_us_some
    A New Hope The Empire   Strikes Back 
    314.4                   247.9 

    mean(non_us_some)
    281.15
    ```    
 
 * arithmetic with matrix :
   * can use standard operators like +, -, /, * or matrixes between operation
   * 📝 **example 1** :
     ```
     # all_wars_matrix is available in your workspace
     all_wars_matrix
     
     # Estimate the visitors
     visitors <- all_wars_matrix / 5
     
     # Print out visitors
     visitors
     ```
   * 🔎 **result 1** :
     * visitors result show have 92 million people went to see "A New Hope" in US theaters, because each ticket price is 5 dollars.
     ```
     all_wars_matrix
                                US non-US
     A New Hope              461.0  314.4
     The Empire Strikes Back 290.5  247.9
     Return of the Jedi      309.3  165.8
     The Phantom Menace      474.5  552.5
     Attack of the Clones    310.7  338.7
     Revenge of the Sith     380.3  468.5

     visitors
                                US non-US
     A New Hope              92.20  62.88
     The Empire Strikes Back 58.10  49.58
     Return of the Jedi      61.86  33.16
     The Phantom Menace      94.90 110.50
     Attack of the Clones    62.14  67.74
     Revenge of the Sith     76.06  93.70
     ```
   * 📝 **example 2** :
     ```
     # all_wars_matrix and ticket_prices_matrix are available in your workspace
     all_wars_matrix
     ticket_prices_matrix
     
     # Estimated number of visitors
     visitors <- all_wars_matrix / ticket_prices_matrix
     
     # Print out visitors
     visitors
     ```
   * 🔎 **result 2** :
     ```
     all_wars_matrix
                             US     non-US
     A New Hope              461.0  314.4
     The Empire Strikes Back 290.5  247.9
     Return of the Jedi      309.3  165.8
     The Phantom Menace      474.5  552.5
     Attack of the Clones    310.7  338.7
     Revenge of the Sith     380.3  468.5

     ticket_prices_matrix
                             US     non-US
     A New Hope              5.0    5.0
     The Empire Strikes Back 6.0    6.0
     Return of the Jedi      7.0    7.0
     The Phantom Menace      4.0    4.0
     Attack of the Clones    4.5    4.5
     Revenge of the Sith     4.9    4.9
     
     visitors
                              US         non-US
     A New Hope               92.20000   62.88000
     The Empire Strikes Back  48.41667   41.31667
     Return of the Jedi       44.18571   23.68571
     The Phantom Menace       118.62500  138.12500
     Attack of the Clones     69.04444   75.26667
     Revenge of the Sith      77.61224   95.61224
     ```      
