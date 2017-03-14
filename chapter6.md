---
title       : Understanding Psychometric Instruments at CAR
description : CAR has a ton of instruments that we use to measure all sorts of things!  You'll want to be familiar with many of these.


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:03418b5e2c
## Access to CAR's form library

Hopefully, if you were assigned this training, your PI (or Joy) has added you to the following database.  See if you can access it:
https://redcap.research.chop.edu/redcap_v7.1.2/index.php?pid=12524.  You can only advance in this chapter once you have access.  If you don't, [email Joy](mailto:paytonk@email.chop.edu)!

Ready to move on?

*** =instructions
- Yep, I have access!
- Nope, still waiting!

*** =hint
No real hint.  Just ask Joy to add you!

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Oops, you have to get that access before you can continue!"
msg_good <- "Alright, let's keep going!"
test_mc(correct = 1, feedback_msgs = c(msg_good, msg_bad))
```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:156c554b4d
## Looking at a Record

In this REDCap database, each record is a form or instrument in our library of psychometric measures.  Normally, in a REDCap database, each record represents a human research subject.  By working in this project, you'll not only learn about psychometric instruments we use, you'll also learn about how to use REDCap to collect and manage study data.

See if you can find the "Instrument Profile" for the BRIEF Parent Form.  Once you find it, download the scanned image associated with the form.  How many questions are there?

*** =instructions
- 46
- 86
- 26
- 100

*** =hint
Having a hard time finding the BRIEF Parent? Try Add / Edit Records.  

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Nope, that's not quite right!"
msg_good <- "Yep, you got it!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_good, msg_bad, msg_bad))
```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:25ea344b18
## Checking out Existing Reports

Not all of the forms listed in our library have scanned paper forms associated with them.  Let's say your job is to track down which forms still need to have .pdfs uploaded.  Go to the Data Exports, Reports, and Stats link on the left side of the page and find Records without PDF.  Click on the button to view report.

What's the best description of what you see?
*** =instructions
- a five-column table, with striped rows, each column with both a human-readable and machine name for the data
- an executive report, in the form of a printable document with CHOP-branded headers and footers and a watermark
- a color-coded grid with red, green, yellow, and grey dots representing incomplete, complete, unclear, and absent data, respectively

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Nope, that's not quite right!"
msg_good <- "Yep, you got it!"
test_mc(correct = 1, feedback_msgs = c(msg_good, msg_bad, msg_bad))
