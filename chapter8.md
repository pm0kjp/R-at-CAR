---
title       : "Common Use Cases: Merging Ambiguous Data"
description : Here we'll go over another common use case, that of merging ambiguous data.


--- type:NormalExercise lang:r xp:100 skills:1 key:c189a1a399
## Describing the Problem

Let's say you're merging two data frames, from two different studies.  Jane's study and Bill's study collect very different kinds of data, but they have some overlap.  For example, both collected SRS total T scores on some (maybe not all) of their subjects. So, when you merge the two dataframes into a combined dataset, you have SRS\_Total\_T.x and SRS\_Total\_T.y -- two columns which each contain SRS total T scores.  

* Some rows have values in neither column -- the subject doesn't have an SRS in either study.
* Others have the value in SRS\_Total\_T.x and nothing (NA) in SRS\_Total\_T.y.
* Others have it the other way around -- a value in y but not in x.
* Finally, some may have values in both -- either matching scores (maybe data was shared between the two studies) or non-matching scores (two administrations arrived at different conclusions).  

How can you resolve this conundrum?  Let's start by creating a data frame that illustrates the problem.

*** =instructions

Create a data frame called studyData that has three columns:

study\_id: CAR-Q23, CAR-48A, CAR-2FD, CAR-SNZ, CAR-R42, CAR-33D, CAR-VC8

SRS\_Total\_T.x:  NA, NA, 50, 75, 95, NA, 100

SRS\_Total\_T.y: 100, 80, NA, 80, NA, NA, 100

*** =hint
Don't forget to quote your strings, and use the concatenation operator, `c()`, to combine several values in a single variable.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
studyData <- data.frame(study_id = ...,
                        SRS_Total_T.x=...,
                        SRS_Total_T.y=...)
```

*** =solution
```{r}
studyData <- data.frame(study_id = c('CAR-Q23', 'CAR-48A', 'CAR-2FD', 'CAR-SNZ', 'CAR-R42', 'CAR-33D', 'CAR-VC8'),
                        SRS_Total_T.x=c(NA, NA, 50, 75, 95, NA, 100),
                        SRS_Total_T.y=c(100, 80, NA, 80, NA, NA, 100))
```

*** =sct
```{r}
test_error()
test_object("studyData")
success_msg("Great, now we have a data frame to work with!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:43f0b17863
## Visually Checking out the Data

Now that we have a dataset, let's look at it and see how many of each kind of situation we have.  

*** =instructions

Take a look at studyData (hint: `head()` will give you a default of 6 rows, but our data frame has 7 rows) and then create three objects:

`numZeroScores` should be a number that gives how many subjects don't have any SRS at all.
`numOneScore` should be the number of subjects that have just one score -- in either X or Y version.
`numTwoScores` should be the number of subjects that have two scores -- in both X and Y versions.

*** =hint

*** =pre_exercise_code
```{r}
studyData <- data.frame(study_id = c('CAR-Q23', 'CAR-48A', 'CAR-2FD', 'CAR-SNZ', 'CAR-R42', 'CAR-33D', 'CAR-VC8'),
                        SRS_Total_T.x=c(NA, NA, 50, 75, 95, NA, 100),
                        SRS_Total_T.y=c(100, 80, NA, 80, NA, NA, 100))
```

*** =sample_code
```{r}
# Look at the data frame


# Then populate these variables with numeric values:
numZeroScores <-
numOneScore <-
numTwoScores <-

```

*** =solution
```{r}
# Look at the data frame
studyData

# Then populate these variables with numeric values:
numZeroScores <- 1
numOneScore <- 4
numTwoScores <- 2
```

*** =sct
```{r}
test_error()
test_object("numZeroScores")
test_object("numOneScore")
test_object("numTwoScores")
success_msg("Great, you understand the scope of our problem better now!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:72e8292b7d
## Creating Subsets

There are many ways to go about this, but the easiest (in Joy's opinion) is to subset the data frame according to the different categories.  Let's consider an example.  We could get the row number for which there's a value in SRS\_Total\_T.x but no value in SRS\_Total\_T.y like this:

`xIsRight <- which(!is.na(studyData$SRS_Total_T.x) & is.na(studyData$SRS_Total_T.y))`


*** =instructions
Come up with five subsets:

* xIsRight
* yIsRight
* noValue
* twoValuesThatMach
* twoValuesNoMatch


*** =hint
Trying to use "AND" logic?  Use '&'.  "OR" logic? '|'.

*** =pre_exercise_code
```{r}
studyData <- data.frame(study_id = c('CAR-Q23', 'CAR-48A', 'CAR-2FD', 'CAR-SNZ', 'CAR-R42', 'CAR-33D', 'CAR-VC8'),
                        SRS_Total_T.x=c(NA, NA, 50, 75, 95, NA, 100),
                        SRS_Total_T.y=c(100, 80, NA, 80, NA, NA, 100))
```

*** =sample_code
```{r}
# The score is in X, not  in Y
xIsRight<-which(...)

# The score is in Y,  not in X
yIsRight<-which(...)

# We don't have scores in either.
noValue<-which(...)

# Both have a score, but they match, so no worries.
twoValuesThatMatch<-which(...)

# Both have a score, but they don't match!  Uh oh!
twoValuesNoMatch<-which(...)
```

*** =solution
```{r}
# The score is in X, not  in Y
xIsRight<-which(!is.na(studyData$SRS_Total_T.x) & is.na(studyData$SRS_Total_T.y))

# The score is in Y,  not in X
yIsRight<-which(!is.na(studyData$SRS_Total_T.y) & is.na(studyData$SRS_Total_T.x))

# We don't have scores in either.
noValue<-which(is.na(studyData$SRS_Total_T.x) & is.na(studyData$SRS_Total_T.y))

# Both have a score, but they match, so no worries.
twoValuesThatMatch<-which(!is.na(studyData$SRS_Total_T.x) & 
                          !is.na(studyData$SRS_Total_T.y) & 
                          studyData$SRS_Total_T.x == studyData$SRS_Total_T.y)

# Both have a score, but they don't match!  Uh oh!
twoValuesNoMatch<-which(!is.na(studyData$SRS_Total_T.x) & 
                        !is.na(studyData$SRS_Total_T.y) & 
                        studyData$SRS_Total_T.x != studyData$SRS_Total_T.y)
```

*** =sct
```{r}
test_error()
test_object("xIsRight")
test_object("yIsRight")
test_object("noValue")
test_object("twoValuesThatMatch")
test_object("twoValuesNoMatch")
success_msg("Great job, you've created subsets that cover every possibility!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:4272378922
## Understanding numerical subsets

The subsets you created are numerical vectors -- each one holds row numbers that tell which rows in the studyData data frame meet the various conditions you set.  Just as we did in a previous chapter using logical (TRUE/FALSE) vectors, we can use numerical vectors to index a data frame.  For example, `studyData[xIsRight,]` will show only the appropriate rows, and all columns, of the data frame.  Try it in the console!


*** =instructions

Take a look at the dataframe, using your subsets to tailor what you see.  You can use this format:

`studyData[subsetName,]`

Can't remember what you named all those subsets?  Use `ls()` to see all the objects in your environment! 
*** =hint

*** =pre_exercise_code
```{r}
studyData <- data.frame(study_id = c('CAR-Q23', 'CAR-48A', 'CAR-2FD', 'CAR-SNZ', 'CAR-R42', 'CAR-33D', 'CAR-VC8'),
                        SRS_Total_T.x=c(NA, NA, 50, 75, 95, NA, 100),
                        SRS_Total_T.y=c(100, 80, NA, 80, NA, NA, 100))
# The score is in X, not  in Y
xIsRight<-which(!is.na(studyData$SRS_Total_T.x) & is.na(studyData$SRS_Total_T.y))

# The score is in Y,  not in X
yIsRight<-which(!is.na(studyData$SRS_Total_T.y) & is.na(studyData$SRS_Total_T.x))

# We don't have scores in either.
noValue<-which(is.na(studyData$SRS_Total_T.x) & is.na(studyData$SRS_Total_T.y))

# Both have a score, but they match, so no worries.
twoValuesThatMatch<-which(!is.na(studyData$SRS_Total_T.x) & 
                          !is.na(studyData$SRS_Total_T.y) & 
                          studyData$SRS_Total_T.x == studyData$SRS_Total_T.y)

# Both have a score, but they don't match!  Uh oh!
twoValuesNoMatch<-which(!is.na(studyData$SRS_Total_T.x) & 
                        !is.na(studyData$SRS_Total_T.y) & 
                        studyData$SRS_Total_T.x != studyData$SRS_Total_T.y)
```

*** =sample_code
```{r}
# Show the rows where x is the correct score to use


# Show the rows where y is the correct score to use


# Show the rows where we don't have a score available at all


# Show the rows where we have two scores that agree


# Show the rows where we have two scores that disagree
```

*** =solution
```{r}
# Show the rows where x is the correct score to use
studyData[xIsRight,]

# Show the rows where y is the correct score to use
studyData[yIsRight,]

# Show the rows where we don't have a score available at all
studyData[noValue,]

# Show the rows where we have two scores that agree
studyData[twoValuesThatMatch,]

# Show the rows where we have two scores that disagree
studyData[twoValuesNoMatch,]

```

*** =sct
```{r}
test_error()
test_output_contains('studyData[xIsRight,]', 
            incorrect_msg = "Did you display the xIsRight rows?")
test_output_contains('studyData[yIsRight,]', 
            incorrect_msg = "Did you display the yIsRight rows?")
test_output_contains('studyData[noValue,]', 
            incorrect_msg = "Did you display the noValue rows?")
test_output_contains('studyData[twoValuesThatMatch,]', 
            incorrect_msg = "Did you display the twoValuesThatMatch rows?")
test_output_contains('studyData[twoValuesNoMatch,]', 
            incorrect_msg = "Did you display the twoValuesNoMatch rows?")
success_msg("Great job displaying the data!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:8f347c0c84
## Resolving the data conflicts

Now that we have our subsets defined, I can think about the logic for each case.  

* If x is right and there's no y (xIsRight), I want to hang on to x.
* Likewise, if y is right and x is blank, I want to hang on to y. (e.g. yIsRight).
* No value?  Leave SRS\_Total\_T blank.
* Matching x and y?  Just choose one, say, x.
* Two values that don't match?  I could choose the lower or higher one, or take the average, or flag it with a code like -999, which stands out and shows that these need a bit of manual resolution (maybe one of them is wrong?).  That last is what you'll do in this exercise.


*** =instructions
- Create a column in studyData called "SRS\_Total\_T\_resolved" and set it to be NA.
- Fill in the values of this field according to the common-sense rules discussed above.
- Then delete the obsolete SRS\_Total\_T.x and SRS\_Total\_T.y columns.

*** =hint

*** =pre_exercise_code
```{r}
studyData <- data.frame(study_id = c('CAR-Q23', 'CAR-48A', 'CAR-2FD', 'CAR-SNZ', 'CAR-R42', 'CAR-33D', 'CAR-VC8'),
                        SRS_Total_T.x=c(NA, NA, 50, 75, 95, NA, 100),
                        SRS_Total_T.y=c(100, 80, NA, 80, NA, NA, 100))
# The score is in X, not  in Y
xIsRight<-which(!is.na(studyData$SRS_Total_T.x) & is.na(studyData$SRS_Total_T.y))

# The score is in Y,  not in X
yIsRight<-which(!is.na(studyData$SRS_Total_T.y) & is.na(studyData$SRS_Total_T.x))

# We don't have scores in either.
noValue<-which(is.na(studyData$SRS_Total_T.x) & is.na(studyData$SRS_Total_T.y))

# Both have a score, but they match, so no worries.
twoValuesThatMatch<-which(!is.na(studyData$SRS_Total_T.x) & 
                          !is.na(studyData$SRS_Total_T.y) & 
                          studyData$SRS_Total_T.x == studyData$SRS_Total_T.y)

# Both have a score, but they don't match!  Uh oh!
twoValuesNoMatch<-which(!is.na(studyData$SRS_Total_T.x) & 
                        !is.na(studyData$SRS_Total_T.y) & 
                        studyData$SRS_Total_T.x != studyData$SRS_Total_T.y)
```

*** =sample_code
```{r}
# Create an all-NA column for our new variable
studyData$SRS_Total_T_resolved <-   # What should this be?

# And now I'll populate it!
studyData$SRS_Total_T_resolved[xIsRight] <-  # Make sure your right hand side is the same length vector!
studyData$SRS_Total_T_resolved[yIsRight] <-  # Make sure your right hand side is the same length vector!
studyData$SRS_Total_T_resolved[twoValuesThatMatch] <-  # Make sure your right hand side is the same length vector!
studyData$SRS_Total_T_resolved[twoValuesNoMatch] <- # Set this equal to our "uh-oh" value.

# I'll just leave the "no value" group NA, which is what I set my column 
# to initially.  No need to assign it anything!

# Remove useless columns.  Try using dplyr select() for this!
library(dplyr)
studyData <- studyData %>% select(-c(...))  # What cols am I removing (note the minus sign!)?

```

*** =solution
```{r}
# Create an all-NA column for our new variable
studyData$SRS_Total_T_resolved <- NA

# And now I'll populate it!
studyData$SRS_Total_T_resolved[xIsRight] <- studyData$SRS_Total_T.x[xIsRight]
studyData$SRS_Total_T_resolved[yIsRight] <- studyData$SRS_Total_T.y[yIsRight]
studyData$SRS_Total_T_resolved[twoValuesThatMatch] <- studyData$SRS_Total_T.x[twoValuesThatMatch]
studyData$SRS_Total_T_resolved[twoValuesNoMatch] <- -999

# I'll just leave the "no value" group NA, which is what I set my column 
# to initially.  No need to assign it anything!

# Remove useless columns.  Try using dplyr select() for this!
library(dplyr)
studyData <- studyData %>% select(-c(SRS_Total_T.x, SRS_Total_T.y))  # What cols am I removing (note the minus sign!)?
```

*** =sct
```{r}
test_error()
test_object("studyData")
success_msg("Fantastic job.  If you haven't already, take a look at your spruced-up data frame!")
```
