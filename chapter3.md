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
