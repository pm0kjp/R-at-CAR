---
title       : "Common Use Cases: Date Matching"
description : Here we'll take a look at some things you'll often have to do with CAR's tabular data.
--- type:NormalExercise lang:r xp:100 skills:1 key:6f8860ff3e
## Get some Data

Let's take the example of "date matching."  Let's get two datasets, one that has language achievement data and one that has math achievement data (both fake!).


*** =instructions
Create two dataframes, fakeMath and fakeLang, which contain simulated data.  Use `read.csv()` to get the data from https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeMath.csv and https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeLang.csv.  It's almost always a good idea to use `stringsAsFactors = FALSE` when using `read.csv()`!

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

Now that you've got fakeMath and fakeLang, take a look at the data and correct any type problems.  There are several ways to check out data types.  We'll use `str()`, which will show you the structure of your data frames.  We can also use `head()` and `tail()` to look at the data frames.  

In the *console*, use `str(fakeMath)` to check out the structure of fakeMath.  You'll see that the second variable is a chr, or character variable, but it would be better to have its data type be date.  That way we could do things like date arithmetic!  You can use `as.Date()` to transform dates that are in character format and make them dates.

*** =instructions
Use `str()` to look at fakeMath and fakeLang, then use `as.Date()` to make any date fields that are in character format true date-formatted variable types.

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

Use `duplicated()` to see if any subjectID values are repeated.  Put the duplicated ID's for `fakeMath` into an object called `multipleMathScores`, and similarly, create `multipleLangScores` with the duplicated subject ID's in `fakeLang`.  

Then take a look at each object you created, using `summary()`.  You'll see that there are TRUE and FALSE values, indicating, for each subjectID, whether it is a 2nd (or 3rd, or 4th...) occurrence of an ID. 

*** =hint
You'll want to make sure to run `duplicated()` *just* on the subjectID field, not the entire dataframe.  Don't forget to use `?` plus the command you want to learn more about, when you need a bit of extra help.

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



--- type:NormalExercise lang:r xp:100 skills:1 key:900542393a
## Using TRUE/FALSE vectors

In the last exercise, we were able to get TRUE/FALSE values showing if the ID's in our data frames were the 2nd-nth use of that ID.  How can we actually see the affected ID's?  We'll use R's indexing feature to get a list of the actual ID's that repeat.

### Quick indexing review

Often, when we index (get specific data from inside a larger object) in R, we do something like this:

`fakeMath[10:25,1:2]` -- this shows rows 10-25 and column 1-2.
`fakeLang$subjectID` -- this shows an entire column.
`fakeLang[1:10,]` -- this shows all columns for the first ten rows.

Try these methods in the console.

### Indexing using truth values

We can also use TRUE/FALSE vectors.  So, if I have a vector "truthValues" of TRUE/FALSE that is the same number of rows as my data frame, I could show just the rows that are marked as "TRUE".  So, if my logical vector is something like c(TRUE, TRUE, FALSE, FALSE, TRUE), I could use that vector to indicate that I want the first, second, and fifth values from something (data frame, for example) that has a length of five.

So, I could do this to get entire rows (I'm selecting all columns here):

`fakeLang[truthValues,]  # Note -- sample code -- won't actually work!`

Or, I could choose just a single column to show, like subjectID:

`fakeLang$subjectID[truthValues]` or `fakeLang[truthValues, "subjectID"]`

*** =instructions

Using the vectors you created in the last exercise, multipleLangScores and multipleMathScores, extract just the duplicated ID's.  Don't get the whole row, just the subjectIDs.  Finally, wrap your whole command in `unique()` so that we only see each repeated ID one time (otherwise, if an ID occurred 4 times, we'd see it 3 times -- the 2nd, 3rd, and 4th uses).  Do this for both fakeLang (using multipleLangScores) and fakeMath (using multipleMathScores).  Put the repeated ID's for fakeMath into mathRepeaters, and the repeated ID's for fakeLang into langRepeaters.  Then take a look at each list of repeating ID's.

*** =hint
You'll want to do something like this: `unique(fakeMath....)` and `unique(fakeLang....)`

*** =pre_exercise_code
```{r}
fakeMath <- read.csv("https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeMath.csv", stringsAsFactors = FALSE)
fakeLang <- read.csv("https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeLang.csv", stringsAsFactors = FALSE)
fakeLang$testDate <- as.Date(fakeLang$testDate) 
fakeMath$testDate <- as.Date(fakeMath$testDate) 
multipleLangScores <- duplicated(fakeLang$subjectID)
multipleMathScores <- duplicated(fakeMath$subjectID)
```

*** =sample_code
```{r}
langRepeaters <- unique() # Which ID's are repeated in fakeLang?
mathRepeaters <- unique() # Which ID's are repeated in fakeMath?

# Check out the repeated values:
langRepeaters
mathRepeaters
```

*** =solution
```{r}
langRepeaters <- unique(fakeLang$subjectID[multipleLangScores])
mathRepeaters <- unique(fakeMath$subjectID[multipleMathScores])

langRepeaters
mathRepeaters
```

*** =sct
```{r}
test_error()
test_object("langRepeaters")
test_object("mathRepeaters")
success_msg("Great!  Now we're really close to doing some date matching!")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:16e55c13ac
## Checking out repeated data

So far, we've identified which subjectID's are duplicated and we've identified which ones they are.  Why are we doing this?  Because at CAR, we often have repeated measures.  A subject who was in two different studies might have two SRS-2 Parent questionnaires given 2 years apart and 2 different SCQ's.  When we do data pulls for scientists, how do we pick which value is the "right" value to return?  Or do we match both SCQ values to both SRS-2?  That would give us four rows for a single subject, which we hardly ever want.  Generally, scientists want a single row of data for each subject.

There are multiple ways to do "date matching."  The most common is that scientists will pick an "anchor" date, like the subject's ADOS administration date (or, in the case of multiple ADOS administrations, their most recent, or their earliest.  Then all other questionnaires will be selected by proximity to that anchor date.  Let's do the first step here, establishing our anchor date.  In our case, we'll say the date of the first Math test is the anchor date.  Let's get that!


*** =instructions

Load the dplyr library using `library(dplyr)`.

Then, use dplyr to limit the fakeMath dataframe to just those rows that represent each subject's *first* Math score (in time).  The simplest way to do this is:

* use group_by to create groups based on subjectID
* use filter to restrict the rows to be the earliest of the dates
* use slice to just take the first remaining row (only important if there's a date tie)
* ungroup.
* save the results in earliestMathScores.

Find out the number of rows in earliestMathScores.  How many unique Math test takers do we have?  Store that number in numMath.

*** =hint
Do you need to be reminded of the structure of fakeMath?  Try `str(fakeMath)`.

*** =pre_exercise_code
```{r}
fakeMath <- read.csv("https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeMath.csv", stringsAsFactors = FALSE)
fakeLang <- read.csv("https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeLang.csv", stringsAsFactors = FALSE)
fakeLang$testDate <- as.Date(fakeLang$testDate) 
fakeMath$testDate <- as.Date(fakeMath$testDate) 
```

*** =sample_code
```{r}
library(dplyr)
earliestMathScores <- fakeMath %>% 
                      group_by(...) %>%  # What are you grouping by?
                      filter( .... == min(...)) %>%  # What are you trying to find the min of?
                      slice(1) %>%  # Just get the first remaining row
                      ungroup()
numMath <- # number of rows in earliestMathScores
```

*** =solution
```{r}
library(dplyr)
earliestMathScores <- fakeMath %>% 
  group_by(subjectID) %>% 
  filter(testDate == min(testDate)) %>% 
  slice(1) %>% 
  ungroup()
numMath <- nrow(earliestMathScores)
```

*** =sct
```{r}
test_error()
test_object("earliestMathScores")
test_object("numMath")
success_msg("Great!  Now we're really close to doing some date matching!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:499f5b2f6b
## Merging by Date

As we've discussed previously, using dplyr will help a lot with date matching.  We have 411 unique subjects with Math scores (we narrowed them down by taking each subject's first administration).  The date of those math scores will be the "anchor" date for selecting a Language score to use in our merge.  It doesn't matter which happened first, language or math -- we just want the minimum difference (in other words, the absolute value of the testDate for math minus the testDate for language, or the other way around).


*** =instructions

First, merge earliestMathScores (what you created in the last question) and fakeLang.  Since the column names are the same in each data frame, `merge()` will apply suffixes, which you want to be crystal clear.  You'll use ".math" as the suffix for columns coming from earliestMathScores, and .lang for columns coming from fakeLang.  Also, keep rows where there are math scores but the subject doesn't have a language score.  Then, you'll use a similar dplyr technique to what you did last time:  

* group_by the subjectID
* filter by the smallest absolute value of the date difference 
* slice(1) to keep the first row of any "ties"
* ungroup

Store the combined data in mathLangScores.

*** =hint
Merge can be complicated!  Try `?merge()` for more info.


*** =pre_exercise_code
```{r}
fakeMath <- read.csv("https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeMath.csv", stringsAsFactors = FALSE)
fakeLang <- read.csv("https://raw.githubusercontent.com/pm0kjp/R-at-CAR/master/datasets/fakeLang.csv", stringsAsFactors = FALSE)
fakeLang$testDate <- as.Date(fakeLang$testDate) 
fakeMath$testDate <- as.Date(fakeMath$testDate) 
library(dplyr)
earliestMathScores <- fakeMath %>% 
  group_by(subjectID) %>% 
  filter(testDate == min(testDate)) %>% 
  slice(1) %>% 
  ungroup()
```

*** =sample_code
```{r}
unfilteredScores <- merge(x=earliestMathScores, y=fakeLang, by="...",  # What will you use to match?
                          all...., # which of x and y do you want to preserve all rows for?
                          suffixes = c('....','...'))   # what suffixes do you want?  Put in x, y order.
                          
mathLangScores <- unfilteredScores %>%
                  group_by(...) %>% # What is your grouping variable?
                  filter(abs(......) == min(abs(....))  %>%  # what are you trying to minimize?
                  slice(1) %>%
                  ungroup()
                          
```

*** =solution
```{r}
unfilteredScores <- merge(x=earliestMathScores, y=fakeLang, by="subjectID",  # What will you use to match?
                          all.x = TRUE, # which of x and y do you want to preserve all rows for?
                          suffixes = c('.math', '.lang'))  # what suffixes do you want?  Put in x, y order.
                                       
mathLangScores <- unfilteredScores %>%
                  group_by(subjectID) %>%
                  filter(abs(testDate.math - testDate.lang) == min(abs(testDate.math - testDate.lang)))  %>% 
                  slice(1) %>%
                  ungroup()
```

*** =sct
```{r}
test_error()
test_object("mathLangScores")
success_msg("Perfect, you've done date matching!")
```
