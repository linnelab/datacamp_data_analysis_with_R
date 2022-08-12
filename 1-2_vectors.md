# Lesson 1 : Introduction to R

## 1-2. Vectors
* vectors like one dimension array or list.
* __create a vector__ : 
  * ✒ use combine function **`c()`**
  * 📝 **example** :
    ```
    numeric_vector <- c(1, 10, 49)
    character_vector <- c("a", "b", "c")
    boolean_vector <- c(TRUE, FALSE, TRUE)
    ```
    
* __give names for the elements of the vector__ : 
  * ✒ use **`names()`** function
  * 📝 **example** :
    ```
    # Poker and roulette winnings from Monday to Friday:
    poker_vector <- c(140, -50, 20, -120, 240)
    roulette_vector <- c(-24, -50, 100, -350, 10)
    days_vector <- c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")
    
    # Assign days as names of poker_vector
    names(poker_vector) <- days_vector
    
    # Assign days as names of roulette_vector
    names(roulette_vector) <- days_vector

    # Print out the value of the variable poker_vector and roulette_vector
    poker_vector
    roulette_vector
    ```
  * 🔎 **result** :
    ```
    Monday   Tuesday Wednesday  Thursday    Friday 
    140       -50        20      -120       240 

    Monday   Tuesday Wednesday  Thursday    Friday 
    -24       -50       100      -350        10 
    ```

* __arithmetic with vectors__ :
  * ✒ use **`addition (+)`** :
    * calculates **`each elements`** of a vector
    * 📝 __example__ :
      ```
      # Assign to total_daily how much you won/lost on each day
      total_daily <- poker_vector + roulette_vector

      # Print out the value of the variable poker_vector and roulette_vector
      total_daily
      ```
    * 🔎 __result__ :
      ```
      Monday   Tuesday Wednesday  Thursday    Friday 
      116      -100       120      -470       250 
      ```
  * ✒ use **`sum()`** function :
    * calculates the sum of **`all elements`** of a vector
    * 📝 __example__ :
      ```      
      # Total winnings with poker
      total_poker <- sum(poker_vector)
      
      # Total winnings with roulette
      total_roulette <- sum(roulette_vector)
      
      # Total winnings overall
      total_week <- total_poker + total_roulette
      
      # Print out the value of the variable total_week
      total_week
      ```
    * 🔎 __result__ :
      ```
      -84
      ```
 
 * __comparison with vectors__ :
   * ✒ use **`logical comparison operators`**
   
     |operators|description              |
     |---------|-------------------------|
     |<        |less than                |
     |>        |greater than             |
     |<=       |less than or equal to    |
     |>=       |greater than or equal to |
     |==       |equal to each other      |
     |!=       |not equal to each other  |
        
   * 📝 __example__ :
     ```
     # Poker and roulette winnings from Monday to Friday:
     poker_vector <- c(140, -50, 20, -120, 240)
     days_vector <- c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")
     names(poker_vector) <- days_vector

     # Which days did you make money on poker?
     selection_vector <- poker_vector > 0

     # Print out selection_vector
     selection_vector
     
     # Select from poker_vector these days
     poker_winning_days <- poker_vector[selection_vector]
     poker_winning_days
     ```
   * 🔎 __result__ :
     ```
     Monday   Tuesday Wednesday  Thursday    Friday 
     TRUE     FALSE      TRUE     FALSE      TRUE 
     
     Monday Wednesday    Friday 
     140        20       240
     ```
  * __select the single element of the vector__ :
    * 🌟 the **`first element`** in a vector has **`index 1`**, __not 0__.
    * ✒ use **`[]`**
    * 📝 __example__ :
      ```
      poker_vector <- c(140, -50, 20, -120, 240)
      
      # Define a new variable based on a selection
      poker_wednesday <- poker_vector[3]
      
      # Print out the value of the variable poker_wednesday
      poker_wednesday
      ```
    * 🔎 __result__ :
      ```
      20
      ```
  * __select multiple element of the vector__ :
    * 🚩 method 1 : **`use [c(,)]`**
      * 📝 __example__ :
        ```
        poker_vector <- c(140, -50, 20, -120, 240)
        days_vector <- c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")
        names(poker_vector) <- days_vector

        # Define a new variable based on a selection
        poker_midweek <- poker_vector[c(2, 3, 4)]
        poker_odd_day <- poker_vector[c(1, 3, 5)]

        # Print out the value of the variable poker_midweek
        poker_midweek
        poker_odd_day
        ```
      * 🔎 __result__ :
        ```
        Tuesday Wednesday  Thursday 
        -50        20      -120 

        Monday Wednesday    Friday 
        140        20       240 
        ```
      
    * 🚩 method 2 : **`use [:]`**  (select consecutive elements of the vector)
      * 📝 __example__ :
         ```
         poker_vector <- c(140, -50, 20, -120, 240)
         days_vector <- c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")
         names(poker_vector) <- days_vector

         # Define a new variable based on a selection
         poker_selection_vector <- poker_vector[2:5]

         # Print out the value of the variable roulette_selection_vector
         poker_selection_vector
         ```
      * 🔎 __result__ :
         ```
         Tuesday   Wednesday  Thursday   Friday 
         -50       20         -120       240 
         ```

    * 🚩 method 3 : use **`element names`**
      * 📝 __example__ :
        ```
        # Poker and roulette winnings from Monday to Friday:
        poker_vector <- c(140, -50, 20, -120, 240)
        days_vector <- c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")
        names(poker_vector) <- days_vector

        # Select poker results for Monday, Tuesday and Wednesday
        poker_start <- poker_vector[c("Monday", "Tuesday", "Wednesday")]
        poker_start
        ```
      * 🔎 __result__ :
        ```
        Monday   Tuesday Wednesday 
          140       -50        20 
        ```
* __Calculate the average of the values for the vector__ :
  * ✒ use **`mean()`** function
  * 📝 __example__ :
    ```
    # Calculate the average of the elements in poker_start
    mean(poker_start)
    ```
  * 🔎 __result__ :
    ```
    36.66667
    ```
