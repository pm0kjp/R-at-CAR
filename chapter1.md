---
title       : Quick Refresher on Tabular Data
description : Tabular Data -- What is it?  How do we work with it?


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:852d4b84bb
## What is tabular data?

Tabular data is data that can easily be displayed in a table.  If you can imagine putting the data into a spreadsheet or other kind of table, it's probably tabular data.  CAR has lots of tabular data -- things like answers to questionnaires, performance data on a task, measurements of someone's body, medical and diagnostic histories, and other data types can be organized into rows (one row per research subject) and columns (with names like "height", "question1", "IQ", "number_correct", etc.).

Which of the following kinds of data are tabular?
*** =instructions
- Transcripts of conversations between children and psychologists
- Parent responses to a survey that asks 40 questions about child behavior
- Voice recordings
- Genomic data 

*** =hint
Imagine trying to fit the data into a table with rows and columns.  Which one fits that kind of schema?

*** =pre_exercise_code
```{r}
# None
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
msg_transcript <- "Not really.  Transcript data is hard to put into columns and rows.  Rather, it's a free-form sort of data that can be short or long, have different turn-taking, have pauses that need to be noted, overlapping speaking, and different vocabulary.  This kind of data might be better in a document store, not in tabular format!"
msg_survey <- "You got it.  The fact that the structure is set -- 40 questions -- is a good hint that this could be imagined as a 40-column table.  The 3D movement data is sort of a trick question:  You could perhaps imagine a table with X,Y, and Z columns and a row for each frame, but at a recording speed of 60 (or more!) frames per second, each subject would have a very, very long table.  While you could force this to be in a tabular format, it's more likely to be set up as a stream of data."
msg_voice <- "Not really.  While we could extract some features to put into columns, like 'fundamental frequency', 'recording length', 'audio quality', the sound recording itself is so rich and varied that it wouldn't do well in a tabular format."
msg_genomic <- "No.  Genomic data is frequently a sequence of letters that is more of a data stream than a tabular data format."
test_mc(correct = 2, feedback_msgs = c(msg_transcript, msg_survey, msg_voice,  msg_genomic))
```

--- type:NormalExercise lang:r xp:100 skills:1 key:1f948a1bd2
## Creating Tabular Data in R

In the previous question, you learned that a parent survey could be easily made into a tabular structure.  Here, let's create some tabular data for a parent questionnaire with five questions.  We'll call it the Particular Interests Inventory, or PII.

In R, we'll use a data frame to create a six column data structure.  The first column will be titled "ID", and the other columns will be titled "Question1", "Question2",... "Question5".  This should be review for you.  If not, you may want to consider the [DataCamp Introduction to R Course](https://www.datacamp.com/courses/free-introduction-to-r).


*** =instructions
- Create a data frame named "pii" with just one row, using these parameters: "ID" = "CAR-123";  "Question1" = "Y"; "Question2" = "N"; "Question3"= "Y"; "Question4" = "Y"; "Question5" = "N")

*** =hint
- `?data.frame()` might help you!  Type it into the console.
- Make sure your quotes are correct -- do you use opening and closing quotes?

*** =pre_exercise_code
```{r}
# None
```

*** =sample_code
```{r}
# Create a data frame with one row
pii <-  # Add your code here!
```

*** =solution
```{r}
# Create a data frame with one row, using data.frame.
pii <- data.frame("ID" = "CAR-123", "Question1" = "Y", "Question2" = "N", "Question3"= "Y", "Question4" = "Y", "Question5" = "N")
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("data.frame", args = c("ID", "Question1", "Question2", "Question3", "Question4", "Question5"),
              not_called_msg = "You didn't call `data.frame()`!",
              incorrect_msg = "You didn't call `data.frame()` with the correct arguments.")

test_object("pii")

test_error()

success_msg("Good work! You created a data frame!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:ab1e3a396a
## Creating a Data Frame from a CSV

In the previous question, you created a data frame that held answers from a parent survey.  Here, let's create a data frame from a csv using read.csv()  This should be review for you.  If not, you may want to consider the [DataCamp Introduction to R Course](https://www.datacamp.com/courses/free-introduction-to-r).

We're going to use data found at
https://raw.githubusercontent.com/pm0kjp/datastore/master/pii.csv

*** =instructions
- Create a data frame named "pii" that contains the data found in [the URL above](https://raw.githubusercontent.com/pm0kjp/datastore/master/pii.csv).  Hint: right click on the link and copy the link address, since the URL is long.


*** =hint
- `?read.csv()` might help you!  Type it into the console.
- Did you quote the URL?

*** =pre_exercise_code
```{r}
# None
```

*** =sample_code
```{r}
# Create a data frame with one row
pii <- read.csv # Add your code here!
```

*** =solution
```{r}
# Create a data frame with one row, using data.frame.
pii <- read.csv("https://raw.githubusercontent.com/pm0kjp/datastore/master/pii.csv")
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("read.csv",
              not_called_msg = "You didn't call `read.csv()`!",
              incorrect_msg = "You didn't call `read.csv()` with the correct arguments.")

test_object("pii")

test_error()

success_msg("Good work! You created a data frame from a CSV!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:72cb3bbfc0
## Analyzing Tabular Data

We've loaded pii with all the data from that .csv you saw in the last question.  You can access it in your console or R script on the right.

*** =instructions
There are lots of ways to do this, but see if you can figure out how many "Y" values are given as the response to Question 3 in the pii data frame.  Assign that value to the variable numYes.

*** =hint
- Try using `pii$Question3 == "Y"` as your condition.
- `?which()` might help you!
- `?length()` might help you!

*** =pre_exercise_code
```{r}
pii <- read.csv("https://raw.githubusercontent.com/pm0kjp/datastore/master/pii.csv")
```

*** =sample_code
```{r}
# Whatever code you want to use to get the number of Y answers given to Q3
numYes <- # Finish this line
```

*** =solution
```{r}
numYes <- length(which(pii$Question3 == "Y"))
```

*** =sct
```{r}
test_object("numYes")
success_msg("Fantastic work! You counted the number of Y perfectly.  You may want to play around a bit with the fake pii data on Joy's GitHub, just to remind yourself how to work with data frames.  If you need some basic R refreshers, check out DataCamp's free introduction to R!")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:7fe9a05798
## A Brief Overview of Research Tabular Data

Most of our researchers collect a *lot* of tabular data.  Terms like "SRS", "ADOS", "Vineland", and "WASI" will become second nature to you.  We generate tabular data through things like:

- Questionnaires given to research subjects or people who can describe subject behavior well (things like the Social Communication Questionnaire, or SCQ, or the ADHD questionnaire for teachers)
- Asking subjects to perform a task and having a researcher record the results (things like the Purdue Pegboard task, or the Benton facial recognition task)
- Conducting an interview that allows psychologists to record subject development or abilities (things like the Autism Diagostic Interview Revised, the ADI-R, or the Weschler Intelligence Scale for Children, 4th Edition, the WISC-4)
- Asking demographic information like date of birth and medical history

This research data has been collected in a "siloed" manner -- each study (and there are many) has its own data collection and storage methods, usually in a system called REDCap, which you'll learn about in the next chapter.  This is convenient for researchers, as they need to be able to both protect access to their data (only certain people, cleared by CHOP's Institutional Review Board, or IRB, should be able to view the data) and analyze it quickly, without having to filter out data that belongs to other studies or making a data pull request from a database manager.

But this can cause problems, too, because there was historically no easy way to answer questions like

- Across all of CAR's studies, how many black, white, and Asian participants are there?
- For a grant, I need to know if we can identify 500 boys with autism between the ages of 6-15.  Do we have that many among our subjects?
- I'd like to understand which questions in the ADOS are the most useful (do a factor analysis).  Please give me all the ADOS question data and scores for everyone for whom we have an ADOS.

Needs like these are why CAR's data team was formed.  Our first task, which is ongoing, was to create a SQL data warehouse of all of our tabular data, from across the various studies.  

After reading the above, which of the following is NOT true?

*** =instructions
- Tabular data at CAR includes things like intelligence tests administered by psychologists.
- In REDCap, access is open at the department level -- all CAR researchers can see all REDCap projects created by other CAR researchers
- Data integration of our tabular data takes place using a SQL data warehouse
- We give questionnaires not only to subjects, but to others who can report or inform on the behavior of subjects

*** =hint
Re-read the paragraph that begins with "This research data has been collected in a "siloed" manner...".

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
msg_iq <- "No.  IQ tests like the WISC-4 are included in our tabular data!"
msg_redcap <- "Yep.  REDCap databases are controlled by whoever created it.  There's no automatic way for us to see into each other's projects without being added manually by the database owner or administrator.  Additionally, users who can access any REDCap database need to be listed in the IRB protocol for the study."
msg_sql <- "Nope, we do in fact use SQL.  Currently we have a MySQL database, and we're hoping to migrate to Oracle soon!"
msg_reporter <- "No. Informant or reporter questionnaires are very important -- we ask parents, teachers, and others to fill out questionnaires about our subjects."
test_mc(correct = 2, feedback_msgs = c(msg_iq, msg_redcap, msg_sql,  msg_reporter))
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:3b4180306f
## A Tidy Approach

We try to do "tidy" data collection, integration, and analysis as much as possible.  To understand this concept, check out a brief article I wrote about this on CAR's data blog: [http://data.centerforautismresearch.org/tidyverse](http://data.centerforautismresearch.org/tidyverse) and read (scan, mostly, but pay special attention to parts 2 and 3) of [Hadley's Classic](http://vita.had.co.nz/papers/tidy-data.pdf).

What defines tidy data?

- (A) Each row consitutes a single observation
- (B) The number of columns is generally less than 25
- (C) Units are the same in all columns of the same metric type (you can't have grams in one column and pounds in another)
- (D) Each column gives a measurement of one thing only
- (E) The number of cells (row / column combinations) is minimized as much as possible

*** =instructions
- (A), (D), and (E)
- (A) through (D)
- (A) and (D) only
- (A) through (C)
- (A) through (E)

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_1 <- "You're partially right, but only partially right!"
msg_2_4 <- "No, there's no limit on columns in the 'tidyverse', and as long as you're consistent within each column, units between columns can vary as needed."
msg_3 <- "That's exactly right.  Avoid the temptation to combine measures or observations!"
msg_5 <- "On the contrary, tidy data often has many more cells than untidy data.  And that's not the only thing you missed!"
test_mc(correct = 3, feedback_msgs = c(msg_1, msg_2_4, msg_3, msg_2_4, msg_5))
```
