---
title       : "Common Use Cases: Filling in Prioritized Data"
description : Here we'll go over another common use case, that of merging prioritized data.

--- type:NormalExercise lang:r xp:100 skills:1 key:42b9d2f433
## What do you mean by Priority?

Sometimes, we want to create a data set that has a value that we'll fill in first using our best data, then we'll populate any missing values from a less-trusted, or less-complete set of data.  Two examples at CAR spring to mind:  Diagnosis and IQ.

Let's say you're working with a scientist who wants to get the SCQ and SRS-2 and Diagnosis values for certain subjects.  Getting the SCQ and SRS-2 values aren't that hard, but diagnosis can be tricky.  We have a "first recourse," our DSM-IV-TR Case Conceptualization database.  That database has diagnoses that were arrived at by practiced clinicians doing thorough chart reviews.  But if there are subjects that don't have a diagnosis there, we can go to the next level, which are study-based diagnoses.  These are pretty good, but may lack the rigor of the DSM-IV-TR Case Conceptualization database.  Note that we only want to add, not overwrite, diagnoses once we start resorting to our study-based diagnoses.

IQ is another example.  We have several different kinds of IQ tests we give to kiddos.  Maybe your scientist prefers DAS-II School-Aged, but if that's not available, has a priority list that allows you to fill in from other tests, like this:

* First: DAS-II School-Aged, then, if needed
* DAS-II Early Childhood, then, if needed
* WISC-IV, then, if needed
* WASI-II, then, if needed
* WASI, then, if needed
* PPVT

In this Chapter, we'll show how this happens!

*** =instructions
We'll start with a pretty easy task:  In your environment, you have three objects.  Use `ls()` to find out what they are, and look at each one using `head()`, but choose 20 rows.

*** =hint

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
unfilteredScores <- merge(x=earliestMathScores, y=fakeLang, by="subjectID",  # What will you use to match?
                          all.x = TRUE, # which of x and y do you want to preserve all rows for?
                          suffixes = c('.math', '.lang'))  # what suffixes do you want?  Put in x, y order.
                                       
mathLangScores <- unfilteredScores %>%
                  group_by(subjectID) %>%
                  filter(abs(testDate.math - testDate.lang) == min(abs(testDate.math - testDate.lang)))  %>% 
                  slice(1) %>%
                  ungroup()
                  

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}

```
---
title       : "Common Use Cases: Filling in Data by Priority"
description : Here we'll go over another common use case, that of merging ambiguous data.

