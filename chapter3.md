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
