# Lesson 1 : Introduction to R

## 1-4. Factors
* create factors :
  * ✒ use **`factor()`** function : can get categories on vector, at work here: "Male" and "Female".
  * 📝 **example** :
    * It is clear that there are two categories, or in R-terms called **'factor levels'**.
    ```
    # Sex vector
    sex_vector <- c("Male", "Female", "Female", "Male", "Male")
    
    # Convert sex_vector to a factor
    factor_sex_vector <- factor(sex_vector)
    
    # Print out factor_sex_vector
    factor_sex_vector
    ```
  * 🔎 **result** :
    ```
    [1] Male   Female Female Male   Male  
    Levels: Female Male
    ```

* create an ordered factor :
  * ✒ use **`factor()`** function and add two additional arguments: **`ordered`** and **`levels`**.
  * For example :
    ```
    factor(vector_name, ordered = TRUE, levels = c("lev1", "lev2", "lev3", ...))
    ```
  * 📝 **example** :
    ```
    # Temperature
    temperature_vector <- c("High", "Low", "High", "Low", "Medium")
    
    # Ordered temparature vector
    factor_temperature_vector <- factor(temparature_vector, ordered = TRUE, levels = c("Low", "Medium", "High"))
    
    # Print out factor_temperature_vector
    factor_temperature_vector
    ```
  * 🔎 **result** :
    ```
    [1] High   Low    High   Low    Medium
    Levels: Low < Medium < High
    ```   
    
* change levels name : 
  * ✒ use **`levels()`** function :
  * For example :
    ```
    levels(factor_vector_name) <- c("level_name1", "level_name2",...)
    ```
  * 📝 **example** :
    ```
    # Create survey_vector
    survey_vector <- c("M", "F", "F", "M", "M")
    
    # Change vector to factor
    factor_survey_vector <- factor(survey_vector)
    
    # Print out factor_survey_vector
    factor_survey_vector
    
    # Specify the levels of factor_survey_vector
    levels(factor_survey_vector) <- c("Female", "Male")
    
    # Print out factor_survey_vector
    factor_survey_vector
    ```
  * 🔎 **result** :
    ```
    factor_survey_vector
    [1] M F F M M
    Levels: F M
    
    factor_survey_vector 
    [1] Male   Female Female Male   Male  
    Levels: Female Male
    ```
    
* get factor information :
  * ✒ use **`summary()`** function : quick overview of the contents of a variable, vector or factor.
  * For example :
    ```
    summary(variable_name)
    summary(vector_name)
    ```
  * 📝 **example** :
    ```
    # create survey vector
    survey_vector <- c("M", "F", "F", "M", "M")
    
    # convert vector to factor
    factor_survey_vector <- factor(survey_vector)
    
    # change levels name
    levels(factor_survey_vector) <- c("Female", "Male")
    
    # Get survey_vector info
    summary(survey_vector)
    
    # Get factor_survey_vector info
    summary(factor_survey_vector)
    ```
  * 🔎 **result** :
    * summary(vector_name) : will get vector length and data type.
    * summary(factor_name) : will get the number of each category.
    ```
    summary(survey_vector)
    Length     Class      Mode 
      5        character  character 
      
    summary(factor_survey_vector)
    Female     Male 
         2        3 
    ```
    
* Comparing ordered factors :
  * use **`comparison operators`**
  * can use the **`>`** operator to check whether one element is larger than the other.
  * if you want to **compare elements of a factor**, it need to create a **ordered factor**.
    <br>if you **not ordered factor**, R will **returns a warning message**, telling you that **the greater than operator is not meaningful** and get **NA** value.
    <br>(factor default is not ordered)</br>
  * 📝 **example** :
    ```
    # Create factor_speed_vector
    speed_vector <- c("medium", "slow", "slow", "medium", "fast")
    
    # create ordered factor
    factor_speed_vector <- factor(speed_vector, ordered = TRUE, levels = c("slow", "medium", "fast"))
    
    # get factor value for second data analyst
    da2 <- factor_speed_vector[2]
    
    # get factor value for second data analyst
    da5 <- factor_speed_vector[5]
    
    # compare data analyst 2 faster than data analyst 5? 
    da2 > da5
    ```
  * 🔎 **result** :   
    ```
    FALSE
    ```  
