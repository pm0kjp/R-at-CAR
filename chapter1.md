---
title       : Intro to Tabular Data
description : Tabular Data in R
attachments :


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:852d4b84bb
## What is tabular data?

Tabular data is data that can easily be displayed in a table.  If you can imagine putting the data into a spreadsheet or other kind of table, it's probably tabular data.  CAR has lots of tabular data -- things like answers to questionnaires, performance data on a task, measurements of someone's body, medical and diagnostic histories, and other data types can be organized into rows (one row per research subject) and columns (with names like "height", "question1", "IQ", "number_correct", etc.).

Which of the following kinds of data are tabular?
*** =instructions
- Transcripts of conversations between children and psychologists
- Parent responses to a survey that asks 40 questions about child behavior
- Voice recordings
- Three-dimensional (X,Y,Z coordinate) movement data over the course of five minutes

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
msg_3d <- "No.  This is a bit of a trick question, because the problem is well-parameterized, with 3 variables, X, Y, and Z, and a fixed time of five minutes.  You could perhaps imagine a table with X,Y, and Z columns and a row for each frame, but at a recording speed of 60 (or more!) frames per second, each subject would have a very, very long table.  While you could force this to be in a tabular format, it's more likely to be set up as a stream of data."
test_mc(correct = 2, feedback_msgs = c(msg_transcript, msg_survey, msg_voice,  msg_3d))
```

--- type:NormalExercise lang:r xp:100 skills:1 key:1f948a1bd2
## Creating Tabular Data in R

In the previous question, you learned that a parent survey could be easily made into a tabular structure.  Here, let's create some tabular data for a parent questionnaire with five questions.  We'll call it the Particular Interests Inventory, or PII.

In R, we'll use a data frame to create a six column data structure.  The first column will be titled "ID", and the other columns will be titled "Question1", "Question2",... "Question5".  


*** =instructions
- Create a data frame with just one row, using this code: `pii <- data.frame("ID" = "CAR-123", "Question1" = "Y", "Question2" = "N", "Question3"= "Y", "Question4" = "Y", "Question5" = "N")`

*** =hint
- Make sure your quotes are correct -- do they have opening and closing quotes?

*** =pre_exercise_code
```{r}
# None
```

*** =sample_code
```{r}
# Create a data frame with one row
pii <- data.frame("ID" = "CAR-123", "Question1" = "Y", "Question2" = "N", "Question3"= "Y", "Question4" = "Y", "Question5" = "N")
```

*** =solution
```{r}
# Create a data frame with one row, using data.frame.
pii <- data.frame # Add your code here!
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("data.frame",
              not_called_msg = "You didn't call `data.frame()`!",
              incorrect_msg = "You didn't call `data.frame()` with the correct arguments.")

test_object("pii")

test_error()

success_msg("Good work!")
```
