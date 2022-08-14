# Lesson 1 : Introduction to R

## 1-5. Dataframe

* __create data frame__ :
  * ✒ use **`data.frame()`** :
  * 📝 **example** :
    ```
    # Definition of vectors
    name <- c("Mercury", "Venus", "Earth", "Mars", "Jupiter", "Saturn", "Uranus", "Neptune")
    type <- c("Terrestrial planet", "Terrestrial planet", "Terrestrial planet", "Terrestrial planet", "Gas giant", "Gas giant", "Gas giant", "Gas giant")
    diameter <- c(0.382, 0.949, 1, 0.532, 11.209, 9.449, 4.007, 3.883)
    rotation <- c(58.64, -243.02, 1, 1.03, 0.41, 0.43, -0.72, 0.67)
    rings <- c(FALSE, FALSE, FALSE, FALSE, TRUE, TRUE, TRUE, TRUE)
    
    # Create a data frame from the vectors
    planets_df <- data.frame(name, type, diameter, rotation, rings)
    
    # Print out data frame
    planets_df
    ```
  * 🔎 **result** :
    ```
         name                type   diameter rotation   rings
    1 Mercury  Terrestrial planet    0.382      58.64   FALSE
    2   Venus  Terrestrial planet    0.949    -243.02   FALSE
    3   Earth  Terrestrial planet    1.000       1.00   FALSE
    4    Mars  Terrestrial planet    0.532       1.03   FALSE
    5 Jupiter           Gas giant   11.209       0.41   TRUE
    6  Saturn           Gas giant    9.449       0.43   TRUE
    7  Uranus           Gas giant    4.007      -0.72   TRUE
    8 Neptune           Gas giant    3.883       0.67   TRUE
    ```

* __show first or last row on data frame__ :
  * ✒ use **`head()`** : 
    * show **first row** on data frame.
    * **default show 6 rows**, you can set the number of row counts, like **`head(dataframe_name, row_counts)`**.
    * 📝 **example** :
      ```
      # show default frist 6 row
      head(planets_df)

      # show frist 4 row
      head(planets_df, 4)
      ```
    * 🔎 **result** :
      ```
           name                type   diameter rotation   rings
      1 Mercury  Terrestrial planet    0.382      58.64   FALSE
      2   Venus  Terrestrial planet    0.949    -243.02   FALSE
      3   Earth  Terrestrial planet    1.000       1.00   FALSE
      4    Mars  Terrestrial planet    0.532       1.03   FALSE
      5 Jupiter           Gas giant   11.209       0.41   TRUE
      6  Saturn           Gas giant    9.449       0.43   TRUE

           name                type   diameter rotation   rings
      1 Mercury  Terrestrial planet    0.382      58.64   FALSE
      2   Venus  Terrestrial planet    0.949    -243.02   FALSE
      3   Earth  Terrestrial planet    1.000       1.00   FALSE
      4    Mars  Terrestrial planet    0.532       1.03   FALSE
      ```
  
  * ✒ use **`tail()`** : show last row on data frame
    * show **last row** on data frame.
    * **default show 6 rows**, you can set the number of row counts, like **`tail(dataframe_name, row_counts)`**.
    * 📝 **example** :
      ```
      # show default last 6 row
      tail(planets_df)

      # show last 4 row
      tail(planets_df, 4)
      ```
    * 🔎 **result** :
      ```
           name                type   diameter rotation   rings
      3   Earth  Terrestrial planet    1.000       1.00   FALSE
      4    Mars  Terrestrial planet    0.532       1.03   FALSE
      5 Jupiter           Gas giant   11.209       0.41   TRUE
      6  Saturn           Gas giant    9.449       0.43   TRUE
      7  Uranus           Gas giant    4.007      -0.72   TRUE
      8 Neptune           Gas giant    3.883       0.67   TRUE   

           name                type   diameter rotation   rings
      5 Jupiter           Gas giant   11.209       0.41   TRUE
      6  Saturn           Gas giant    9.449       0.43   TRUE
      7  Uranus           Gas giant    4.007      -0.72   TRUE
      8 Neptune           Gas giant    3.883       0.67   TRUE  
      ```   

* __get data frame structure__ :
  * when you receive a new dataset or data frame., you can use this function to check data structure.
  * ✒ use **`str()`** function
  * 📝 **example** :
    ```
    # show the structure of planets_df
    str(planets_df)
    ```
  * 🔎 **result** :
    * 8 obs => means **8 rows**.
    * 5 variables => means **5 columns**.
    * $ name, $ type, $ diameter, $ rotation, $ rings => means **column name**.
    * chr, num, logi => means **column data type**.
    * "Mercury"... => means **values**.
    ```
    'data.frame':	8 obs. of  5 variables:
     $ name    : chr  "Mercury" "Venus" "Earth" "Mars" ...
     $ type    : chr  "Terrestrial planet" "Terrestrial planet" "Terrestrial planet" "Terrestrial planet" ...
     $ diameter: num  0.382 0.949 1 0.532 11.209 ...
     $ rotation: num  58.64 -243.02 1 1.03 0.41 ...
     $ rings   : logi  FALSE FALSE FALSE FALSE TRUE TRUE ...
    ```
 
* __Selection of data frame elements or subset__ :
  * ✒ method 1 - use **`[row, column]`** : row and column set **index**.
  * ✒ method 2 - use **`[row, column]`** : row set **index** and column set **column name**. Can not set row name, will get NA result.
  * ✒ method 3 - use **`$`** : use **<data_frame_name>$<column_name>** to get all row data for special column.
  * 🌟 index start from 1.
    * 📝 **example** :
      ```
      # Show planets_df 
      planets_df

      # Method 1 - print out diameter of Mercury (row 1, column 3)
      planets_df[1, 3]

      # Method 1 - print out data for Mars (entire fourth row)
      planets_df[4, ]

      # Method1 - select first 3 values of 2 to 4 column. 
      planets_df[1:3, 2:4]

      # Method 2 - select first 5 values of diameter column 
      planets_df[1:5, "diameter"]

      # Method 3 - select the rings variable from planets_df
      rings_vector <- planets_df$rings
      ## equal method :
      #planets_df[, 5]                  
      #planets_df[, "rings"]
      ```
    * 🔎 **result** :
      ```
      planets_df
           name                type   diameter rotation   rings
      1 Mercury  Terrestrial planet    0.382      58.64   FALSE
      2   Venus  Terrestrial planet    0.949    -243.02   FALSE
      3   Earth  Terrestrial planet    1.000       1.00   FALSE
      4    Mars  Terrestrial planet    0.532       1.03   FALSE
      5 Jupiter           Gas giant   11.209       0.41   TRUE
      6  Saturn           Gas giant    9.449       0.43   TRUE
      7  Uranus           Gas giant    4.007      -0.72   TRUE
      8 Neptune           Gas giant    3.883       0.67   TRUE   

      planets_df[1,3]
      0.382

      planets_df[4,]
        name                 type   diameter  rotation  rings
      4 Mars   Terrestrial planet    0.532     1.03     FALSE

      planets_df[1:3, 2:4]
                      type   diameter  rotation
      1 Terrestrial planet    0.382    58.64
      2 Terrestrial planet    0.949    -243.02
      3 Terrestrial planet    1.000    1.00

      planets_df[1:5, "diameter"]
      0.382  0.949  1.000  0.532 11.209 
      ```
  * ✒ method 4 - use boolean column to get sepcial row data on dataframe.
    * 📝 **example** :
      ```
      # planets_df is pre-loaded in your workspace
      planets_df

      # Select the rings variable from planets_df
      rings_vector <- planets_df$rings

      # Print out rings_vector
      rings_vector

      # Select all columns for planets with rings (i.e. rings = TRUE data)
      planets_df[rings_vector, ]
      ```
    * 🔎 **result** :
      ```
      planets_df
           name                type   diameter rotation   rings
      1 Mercury  Terrestrial planet    0.382      58.64   FALSE
      2   Venus  Terrestrial planet    0.949    -243.02   FALSE
      3   Earth  Terrestrial planet    1.000       1.00   FALSE
      4    Mars  Terrestrial planet    0.532       1.03   FALSE
      5 Jupiter           Gas giant   11.209       0.41   TRUE
      6  Saturn           Gas giant    9.449       0.43   TRUE
      7  Uranus           Gas giant    4.007      -0.72   TRUE
      8 Neptune           Gas giant    3.883       0.67   TRUE     

      rings_vector
      FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE

      planets_df[rings_vector, ]
           name         type   diameter  rotation  rings
      5 Jupiter    Gas giant   11.209     0.41     TRUE
      6  Saturn    Gas giant    9.449     0.43     TRUE
      7  Uranus    Gas giant    4.007    -0.72     TRUE
      8 Neptune    Gas giant    3.883     0.67     TRUE
      ```
  * ✒ method 5 - use **`subset()`** function : 
    * For example :
      ```
      subset(data_frame_name, subset = some_condition)
      ```
    * 📝 **example** :
      ``` 
      # planets_df is pre-loaded in your workspace
      planets_df

      # In the previous exercise, the code below will give same result, but this time, you didn't need the rings_vector.
      subset(planets_df, subset = rings)
      # same as 
      planets_df[rings_vector, ]
      
      # Select planets with diameter < 1
      subset(planets_df, subset = diameter < 1)
      ```
    * 🔎 **result** :
      ```
      planets_df
           name                type   diameter rotation   rings
      1 Mercury  Terrestrial planet    0.382      58.64   FALSE
      2   Venus  Terrestrial planet    0.949    -243.02   FALSE
      3   Earth  Terrestrial planet    1.000       1.00   FALSE
      4    Mars  Terrestrial planet    0.532       1.03   FALSE
      5 Jupiter           Gas giant   11.209       0.41   TRUE
      6  Saturn           Gas giant    9.449       0.43   TRUE
      7  Uranus           Gas giant    4.007      -0.72   TRUE
      8 Neptune           Gas giant    3.883       0.67   TRUE   

      subset(planets_df, subset = rings)
           name         type   diameter  rotation  rings
      5 Jupiter    Gas giant   11.209     0.41     TRUE
      6  Saturn    Gas giant    9.449     0.43     TRUE
      7  Uranus    Gas giant    4.007    -0.72     TRUE
      8 Neptune    Gas giant    3.883     0.67     TRUE
      
      subset(planets_df, subset = diameter < 1)
           name                type  diameter  rotation   rings
      1 Mercury  Terrestrial planet    0.382      58.64   FALSE
      2   Venus  Terrestrial planet    0.949    -243.02   FALSE
      4    Mars  Terrestrial planet    0.532       1.03   FALSE
      ```

* __Sorting data frame__ :
  * use **`order()`** function :  the ranked position of each element.
  * sorting method : ascending.
  * 📝 **example** :
    ```
    # Show planets_df
    planets_df
    
    # Use order() to rank diameter
    positions <- order(planets_df$diameter)
    
    # Show positions
    positions
    
    # Use positions to sort planets_df
    planets_df[order(planets_df$diameter), ]
    ```
  * 🔎 **result** :
    ```
    planets_df
         name               type   diameter rotation  rings
    1 Mercury  Terrestrial planet    0.382    58.64   FALSE
    2   Venus  Terrestrial planet    0.949  -243.02   FALSE
    3   Earth  Terrestrial planet    1.000     1.00   FALSE
    4    Mars  Terrestrial planet    0.532     1.03   FALSE
    5 Jupiter           Gas giant   11.209     0.41   TRUE
    6  Saturn           Gas giant    9.449     0.43   TRUE
    7  Uranus           Gas giant    4.007    -0.72   TRUE
    8 Neptune           Gas giant    3.883     0.67   TRUE
    
    positions
    1 4 2 3 8 7 6 5
    
    planets_df[order(planets_df$diameter),]
         name               type   diameter  rotation  rings
    1 Mercury  Terrestrial planet    0.382      58.64  FALSE
    4    Mars  Terrestrial planet    0.532       1.03  FALSE
    2   Venus  Terrestrial planet    0.949    -243.02  FALSE
    3   Earth  Terrestrial planet    1.000       1.00  FALSE
    8 Neptune           Gas giant    3.883       0.67  TRUE
    7  Uranus           Gas giant    4.007      -0.72  TRUE
    6  Saturn           Gas giant    9.449       0.43  TRUE
    5 Jupiter           Gas giant   11.209       0.41  TRUE
    ```
