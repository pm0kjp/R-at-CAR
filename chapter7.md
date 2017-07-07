---
title       : Common Use Cases
description : Here we'll take a look at some things you'll often have to do with CAR's tabular data.
--- type:NormalExercise lang:r xp:100 skills:1 key:6f8860ff3e
## Get some Data

Let's take the example of "date matching."  Let's get two datasets, one that has language achievement data and one that has math achievement data (both fake!).


*** =instructions
Create two dataframes, fakeMath and fakeLang, which contain simulated data.  Use read.csv() to get the data from https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeMath.csv and https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeLang.csv.  It's almost always a good idea to use stringsAsFactors = FALSE when using read.csv()!

*** =hint
Try fakeMath <- read.csv(".....", stringsAsFactors = FALSE) and fakeLang <- read.csv(".....", stringsAsFactors = FALSE)


*** =pre_exercise_code
```{r}
```

*** =sample_code
```{r}
fakeMath <- read.csv # finish this!
fakeLang <- read.csv # finish this!
```

*** =solution
```{r}
fakeMath <- read.csv("https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeMath.csv", stringsAsFactors = FALSE)
fakeLang <- read.csv("https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeLang.csv", stringsAsFactors = FALSE)
```

*** =sct
```{r}
test_error()
test_object("fakeMath")
test_object("fakeLang")
success_msg("Good work! You pulled in the two objects!")
```




--- type:NormalExercise lang:r xp:100 skills:1 key:3b771fcd2a
## Check out the data and correct data type problems

Now that you've got fakeMath and fakeLang, take a look at the data and correct any type problems.  There are several ways to check out data types.  We'll use str(), which will show you the structure of your data frames.  We can also use head() and tail() to look at the data frames.  In the console, use str(fakeMath) to check out the structure of fakeMath.  You'll see that the second variable is a chr, or character variable, but it would be better to have its data type be date.  That way we could do things like date arithmetic!  You can use as.Date() to transform dates that are in character format and make them dates.

*** =instructions
Use str() to look at fakeMath and fakeLang, then use as.Date to make any date fields that are in character format true date-formatted variable types.
*** =hint

*** =pre_exercise_code
```{r}
fakeMath <- read.csv("https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeMath.csv", stringsAsFactors = FALSE)
fakeLang <- read.csv("https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeLang.csv", stringsAsFactors = FALSE)
```

*** =sample_code
```{r}
# Do the fakeMath fix
str(...)  # replace the dots!
.... <- as.Date(...) # replace the dots!

# Do the fakeLang fix
str(...)  # replace the dots!
.... <- as.Date(...) # replace the dots!
```

*** =solution
```{r}
# Do the fakeMath fix
str(fakeMath)  
fakeMath$testDate <- as.Date(fakeMath$testDate) 

# Do the fakeLang fix
str(fakeLang)  
fakeLang$testDate <- as.Date(fakeLang$testDate) 
```

*** =sct
```{r}
test_error()
test_object("fakeLang")
test_object("fakeMath")
test_function("str",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str()` with the correct arguments.")
success_msg("The dates were transformed accurately, great job!")

```
