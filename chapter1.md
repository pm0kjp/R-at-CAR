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
## More movies

In the previous exercise, you saw a dataset about movies. In this exercise, we'll have a look at yet another dataset about movies!

A dataset with a selection of movies, `movie_selection`, is available in the workspace.

*** =instructions
- Check out the structure of `movie_selection`.
- Select movies with a rating of 5 or higher. Assign the result to `good_movies`.
- Use `plot()` to  plot `good_movies$Run` on the x-axis, `good_movies$Rating` on the y-axis and set `col` to `good_movies$Genre`.

*** =hint
- Use `str()` for the first instruction.
- For the second instruction, you should use `...[movie_selection$Rating >= 5, ]`.
- For the plot, use `plot(x = ..., y = ..., col = ...)`.

*** =pre_exercise_code
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code

library(MindOnStats)
data(Movies)
movie_selection <- Movies[Movies$Genre %in% c("action", "animated", "comedy"),c("Genre", "Rating", "Run")]

# Clean up the environment
rm(Movies)
```

*** =sample_code
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection


# Select movies that have a rating of 5 or higher: good_movies


# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre

```

*** =solution
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection
str(movie_selection)

# Select movies that have a rating of 5 or higher: good_movies
good_movies <- movie_selection[movie_selection$Rating >= 5, ]

# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre
plot(good_movies$Run, good_movies$Rating, col = good_movies$Genre)
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("good_movies")

test_function("plot", args = "x")
test_function("plot", args = "y")
test_function("plot", args = "col")

test_error()

success_msg("Good work!")
```
