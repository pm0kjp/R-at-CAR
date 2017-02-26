---
title       : Accessing REDCap from R
description : How to use the REDCap API


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:38b763d26a
## Setup

Log into CHOP's REDCap instance and go to your first REDCap project, the one you built in the previous chapter of this training.  Click on the "API" application and then click on the button to "Request API Token."  This is handled by an actual human, so it'll take a few minutes (or, in rare cases, a few hours) to get processed.

In the meantime, add a bunch of fake data to your database.  Think about the possibilities for missing, incomplete, or badly formatted data.  Are there any changes you want to make to your instruments (data entry forms)?  Maybe you'll want to make some fields required, or add some Field Notes to make it easier to understand what range of data is expected.  Feel free to delete some questions and add your own new ones.  Really practice some of the things you learned in the Detailed Overview Video.

This is also a good time to consider watching the Data Entry Overview video, the third in the "Just Getting Started" section. It's not required, but it goes over a couple of things you haven't seen yet.

Forget where to look for these videos? Try [https://redcap.chop.edu/index.php?action=training](https://redcap.chop.edu/index.php?action=training)

What are you working on right now?
*** =instructions
- I requested an API token for my database and I'm entering, or have entered, a bunch of fake data into my database.
- Nothing, or not what I was asked.

*** =hint
Seriously, just do this, it'll make sense for future questions!

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "C'mon, work with me here!"
msg_good <- "Thanks!  Please wait to move on in this chapter until you get an email saying your API token was granted.  You can continue work in other chapters."
test_mc(correct = 1, feedback_msgs = c(msg_good, msg_bad))
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:af45bb806b
## Your Token

Hopefully by now you've gotten an email that tells you your request for an API token has been approved.  To check, go into your REDCap database and click on the API link in the Applications section.  You should see a character string.  How many characters long is it?

*** =instructions
- 8
- 16
- 32
- 64
- 128

*** =hint

You shouldn't have to count, just kind of estimate.  It'll be clear when you see the token!

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Nope, take another look!"
msg_good <- "Right on!  Congratulations on getting your REDCap API token!"
test_mc(correct = 3, feedback_msgs = c(msg_bad, msg_bad, msg_good, msg_bad, msg_bad))
```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:9de061edcb
## API Playground

OK, time to head over to the API Playground -- click on that phrase in the Applications pane on the left.  At the top, you'll see an easy-to-navigate box with several drop-down menus.  The first selection you have to make is API Method.  Choose "Export Project Info", and in the next two menus, choose "CSV".  The "Raw Request Parameters" box below your selection will change to reflect whatever you chose! 

Look further down the page and click on the button that says "Execute Request".  You'll get a "waiting" spinner (maybe for awhile, as CHOP REDCap is slow!) and then a box will appear below the button with the data that REDCap returned from your request.  Below that box, you'll see an HTTP status.  You want that to be 200, which means no errors occurred.

How does the first line in the data begin?
*** =instructions
- `project_id,project_title,creation_time`,
- `csv_table:`
- `API_token: [your token], project_notes:`
- None of these

*** =hint

Getting an http status code other than 200?  This is a problem outside your control -- skip ahead to the next chapter and let Joy know what's up!

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Nope, that's not how the data starts."
msg_good <- "Yes, you just made your first API call!  Congrats!"
test_mc(correct = 1, feedback_msgs = c(msg_good, msg_bad, msg_bad, msg_bad))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:7d7d01cba9
## API tokens

Important note: Normally it is a TERRIBLE idea to post or use your API key in the cloud (like here on DataCamp), where it might be copied and used without your consent.  But we can make an exception here because:

- The API key is unique to the combination of user and project.  So this key is unique to your practice project, which will hold just practice data.  There's no way to get to real subject data with your key.  You didn't add real subject data, did you?
- DataCamp is probably not evil and probably isn't interested in your REDCap data anyway
- DataCamp runs over https, so we eliminate the man-in-the-middle risk
- You're going to re-issue or discard your API key at the end of this course, so exposure is limited.

The important thing to remember is that exposing your API key to a place where it could be seen or picked off (say, hotel wi-fi) is a Very Bad Idea, and we're taking a calculated very minimal risk here.

Should you throw around your API keys and share them?

*** =instructions
- Absolutely, I believe in the sharing economy!  Freedom!
- No way, API tokens are like the keys to my house, and I keep them close at all times.
*** =hint
Really?

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "You're killing me, Smalls."
msg_good <- "Yes!  Make good choices!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_good))
```



--- type:NormalExercise lang:r xp:100 skills:1 key:0e20eaee75
## Getting REDCap data into R

We can access REDCap data using the API and bring it directly into R for analysis.  This is often more convenient than downloading a CSV, because you can specify specific data you want, including data that isn't easily downloadable in the REDCap website download area.  

*** =instructions
- Log into your practice REDCap database and go to the API Playground.  
- Choose "Export Project Info", and in the next two menus, choose "CSV".   
- Then look down in the bottom part of the page and look for a bunch of tabs with different programming languages.  
- Click on the R tab, and paste that code into your code editor at the right.  
- Then click "Submit".

*** =hint
If you don't have the API Playground, check to make sure you've given yourself API rights in the User Rights application, and that you've requested an API token in the API section of Applications

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Your code should look something like this:
#!/usr/bin/env Rscript
# library(RCurl)
# result <- postForm(
#   uri='https://redcap.chop.edu/api/',
#   token='SOME TEXT HERE',
#   content='project',
#   format='csv',
#   returnFormat='csv'
#)
#print(result)


```

*** =solution
```{r}
result <- ""
```

*** =sct
```{r}
test_object("result", eval = FALSE)
success_msg("You created the object 'result'!  It's not very pretty, but we'll fix that in our next section.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:cc490e7798
## Formatting REDCap Data

So, the "result" object you created is a raw CSV, but you want to make it into a data frame.  While you might think that `read.csv()` is a good option, you can't do `read.csv(result)`, because `read.csv()` expects a *file name*, not the actual text that constitutes a .csv.  What to do?  We'll make a text connection.

We'll create a "text connection" and when we use that connection variable type, read.csv will realize that it's not going to use a file as its source csv, but a text stream. 

*** =instructions
- Copy the same R code that you did for the last question -- Export Project Info with Format and Errors both set to CSV.
- Remove the line that reads print(result).
- Replace it with these two lines: 
- `con <- textConnection(result)`
- `myDF <- read.csv(con)`
- Add a final line to look just at the first few columns:
- `myDF[,1:3]`
- Submit your answer!
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Your code should look something like this:
#!/usr/bin/env Rscript
# library(RCurl)
# result <- postForm(
#   uri='https://redcap.chop.edu/api/',
#   token='SOME TEXT HERE',
#   content='project',
#   format='csv',
#   returnFormat='csv'
#)
con <- # Add code here
myDF <- # Add code here
```

*** =solution
```{r}
result <- ""
con <- textConnection(result)
myDF <- ""
```

*** =sct
```{r}
test_function("textConnection",
              not_called_msg = "You didn't call `textConnection()`!")
test_object("result", eval= FALSE)
test_object("con", eval=FALSE)
test_object("myDF", eval = FALSE)
success_msg("Fantastic.  You now know how to download a CSV from REDCap and create a data frame from it, all within R!")
```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:b7bbab8dbb
## Understanding Playground Rules

The API playground lets you try out a bunch of different API calls in your browser, so you can fine-tune your requests before plunking that code into your program or script.  This time, go into the API playground, and in the first drop-down menu, choose "Export Records".  Do *NOT* make any other selections.  Then hit "Execute Request".  Look at the output that REDCap returns.  

What do you see?


*** =instructions
- No output -- I didn't request anything specific, so REDCap gave me nothing.
- Output for every instrument and every subject -- I didn't request anything specific, so REDCap gave me everything.
- An error message -- I didn't complete a full request so REDCap didn't know what to do.
*** =hint

It will help if you add fake data to your database, if you haven't already!

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Nope, take a closer look!  It's complicated sometimes to make sense of encoded data, but you can do it!"
msg_good <- "Yep.  If you don't limit your request (say by subject ID or by specific form/instrument), REDCap will just give you everything!  You're at the end of this chapter, so take what you've learned and play around a bit in the API playground and in your own RStudio at your computer!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_good, msg_bad))
```
