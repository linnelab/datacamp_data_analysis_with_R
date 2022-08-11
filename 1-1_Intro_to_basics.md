# Lesson 1 : Introduction to R

## 1-1. Intro to basics

* R language is **`case sensitive`**.

* program comment : use **`#`**

* __arithmetic operation__ : 
  
  |operator|description      |example       |result |
  |--------|-----------------|--------------|-------|
  |+       |Addition         |5 + 5         |10     |
  |-       |Subtraction      |5 - 5         |0      |
  |*       |Multiplication   |3 * 5         |15     |
  |/       |Division         |(5 + 5) / 2   |5      |
  |^       |Exponentiation   |2^5           |32     |
  |%%      |Modulo           |5 %% 2        |1      |
  
* __variable assignment__ : 
  * ✒ use **`<-`**
  * 📝 **example** :
    ```
    # Assign a value to the variables my_apples and my_oranges
    my_apple <- 5
    my_orange <- 6
    
    # Assign a string to the variables my_character
    my_character <- "universe"
    
    # Assign a boolean to the variables my_character
    my_logical <- FALSE
    
    # Print out the value of the variable my_apples and my_oranges
    my_apple
    my_orange
    ```
  * 🔎 **result** :
    ```
    5
    6
    ```
    
* __variables operation__ : 
  * 🌟 variables need same data type (e.g. my_apples and my_oranges are numeric).
  * 📝 **example** :
    ```
    # Assign a value to the variables my_apples and my_oranges
    my_apples <- 5
    my_oranges <- 6

    # Add these two variables together
    my_apples + my_oranges

    # Create the variable my_fruit
    my_fruit <- my_apples + my_oranges
    
    # Print out the value of the variable my_fruit
    my_fruit
    ```
  * 🔎 **result** :
    ```
    12
    ```

* __basic data types__ : 
  
  |name        |description                   |example       |ps                         |
  |------------|------------------------------|--------------|---------------------------|
  |numerics    |decimal values, whole numbers |4.5           |                           |
  |integers    |whole numbers                 |4             |integers are also numerics |
  |logical     |Boolean                       |TRUE, FALSE   |                           |
  |characters  |Text, string                  |"universe"    |                           |

* __check variable data type__ :
  * ✒ use **`class()`** function
  * 📝 **example** :
    ```
    # Declare variables of different types
    my_numeric <- 42
    my_character <- "universe"
    my_logical <- FALSE 

    # Check class of my_numeric
    class(my_numeric)

    # Check class of my_character
    class(my_character)

    # Check class of my_logical
    class(my_logical)
    ```
  * 🔎 **result** :
    ```
    "numeric"
    "character"
    "logical"
    ```
