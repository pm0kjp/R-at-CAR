---
title       : "Common Use Cases: Date Matching"
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
## Correct data type problems

Now that you've got fakeMath and fakeLang, take a look at the data and correct any type problems.  There are several ways to check out data types.  We'll use str(), which will show you the structure of your data frames.  We can also use head() and tail() to look at the data frames.  In the console, use str(fakeMath) to check out the structure of fakeMath.  You'll see that the second variable is a chr, or character variable, but it would be better to have its data type be date.  That way we could do things like date arithmetic!  You can use as.Date() to transform dates that are in character format and make them dates.

*** =instructions
Use str() to look at fakeMath and fakeLang, then use as.Date to make any date fields that are in character format true date-formatted variable types.
*** =hint
You can use `?str()` in the console for more information on how to use it, and likewise you can use `?as.Date` (note the capitalization!) to get more info about that command as well.

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

# Check the fix!
str(...)  # replace the dots!


# Do the fakeLang fix
str(...)  # replace the dots!
.... <- as.Date(...) # replace the dots!

# Check the fix!
str(...)  # replace the dots!

```

*** =solution
```{r}
# Do the fakeMath fix
str(fakeMath)  
fakeMath$testDate <- as.Date(fakeMath$testDate) 

# Check the fix! 
str(fakeMath)  

# Do the fakeLang fix
str(fakeLang)  
fakeLang$testDate <- as.Date(fakeLang$testDate) 

# Check the fix!
str(fakeLang) 
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

--- type:NormalExercise lang:r xp:100 skills:1 key:8aea089315
## Matching by date

Let's take a look at your fakeMath and fakeLang data frames, now with the date data type made into a real date.  Do we have any "repeated measures", where the same subject has multiple values at different time points?  


*** =instructions

Use duplicated() to see if any subjectID values are repeated.  Put the duplicated ID's for fakeMath into an object called multipleMathScores, and similarly, create multipleLangScores with the duplicated subject ID's in fakeLang.  Then take a look at each object you created, using summary().  You'll see that there are TRUE and FALSE values, indicating, for each subjectID, whether it is a 2nd (or 3rd, or 4th...) occurrence of an ID. 

*** =hint
You'll want to make sure to run duplicated() *just* on the subjectID field, not the entire dataframe.  Don't forget to use ? plus the command you want to learn more about, when you need a bit of extra help.

*** =pre_exercise_code
```{r}
fakeMath <- read.csv("https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeMath.csv", stringsAsFactors = FALSE)
fakeLang <- read.csv("https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeLang.csv", stringsAsFactors = FALSE)
fakeLang$testDate <- as.Date(fakeLang$testDate) 
fakeMath$testDate <- as.Date(fakeMath$testDate) 
```

*** =sample_code
```{r}
multipleLangScores <- duplicated(...) # Check subjectID in fakeLang
multipleMathScores <- duplicated(...) # Check subjectID in fakeMath
summary(...) # Are there multiples for Math?
summary(...) # Are there multiples for Lang?
```

*** =solution
```{r}
multipleLangScores <- duplicated(fakeLang$subjectID)
multipleMathScores <- duplicated(fakeMath$subjectID)
summary(multipleLangScores)
summary(multipleMathScores)
```

*** =sct
```{r}
test_error()
test_object("multipleLangScores")
test_object("multipleMathScores")
test_function("summary",
              not_called_msg = "You didn't call `summary()`!",
              incorrect_msg = "You didn't call `summary()` with the correct arguments.")
success_msg("Well done -- we have repeated measures in both fakeLang and fakeMath.")
```
