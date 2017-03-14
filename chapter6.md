---
title       : Understanding Psychometric Instruments at CAR
description : CAR has a ton of instruments that we use to measure all sorts of things!  You'll want to be familiar with many of these.


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:03418b5e2c
## Access to CAR's form library

Hopefully, if you were assigned this training, your PI (or Joy) has added you to the following database.  See if you can access it:
[https://redcap.research.chop.edu/redcap_v7.1.2/index.php?pid=12524](https://redcap.research.chop.edu/redcap_v7.1.2/index.php?pid=12524).  You can only advance in this chapter once you have access.  If you don't, [email Joy](mailto:paytonk@email.chop.edu)!

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
```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:32fc67f1eb
## Reports Video

While still in the Reports screen, check out the video link at the top of the page.  Watch the brief intro into creating reports. 

What kind of data export is *not* explicitly provided for?
*** =instructions
- Stata
- JSON
- CSV
- SPSS
- SAS
*** =hint
You can also hit the Export button on any report to get a list of the export options available!

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Nope, you can download data in this format."
msg_good <- "You're right.  JSON download is not specifically mentioned in the export section.  That's because humans, who use the export functionality, seldom find JSON helpful.  But programs do, which is why JSON exporting is supported in the API!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_good, msg_bad, msg_bad, msg_bad))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:01ab5ec64f
## Create a Report!

Now's your chance to create your own report.  Create a report that has important copyright and intellectual property fields (like publisher info) for all instruments that are part of the ADOS or ADI-R families.  Make sure your report is visible only to you, not to all users of the database.  

Try doing things like changing the order of how fields appear, using "contains" logic, and adding your own touches to the report.  Were you successful?  There's no specific question for this one.
*** =instructions
- No, this report thing is way too tricky!
- I got it!  I played around with the reporting feature and can create reports based on data features.

*** =hint
Stuck?  Try watching the video again!

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Really, you should try to get this right before moving forward!"
msg_good <- "Fantastic, let's keep going!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_good))
```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:598b05a5b0
## Common Instruments

There are a few common instruments that are commonly used to characterize subjects at CAR.  Check out the following instruments and look at the scanned .pdf of the instrument, including the scoring section, if included.

- SCQ Lifetime
- ADI-R (only scoring is uploaded at this point)
- SRS (any variety will work, but SRS Parent is the most frequently used)
- ADOS (again, any variety)
- DAS (any variety, but DAS-II School is our most frequently used)
- DSM Checklist (any variety)

Which of the forms above seem to be adminstered by clinicians -- psychologists, in our case -- and filled out by them after an interview, test, observation, or interaction with the subject?

*** =instructions
- ADI-R, SRS, ADOS, and DAS
- SRS, ADOS, and DSM Checklist
- ADOS, ADI-R, DAS, and DSM Checklist
- SCQ, SRS, and DAS

*** =hint
You have incomplete information here, but you can use form instructions (do they assume a high level of psychological know-how, or just a family connection with a subject?), form name (is the word "interview" or other tell-tale phrase in the title of the instrument or form), or contents (does it seem like this is an IQ test with many parts, or a quick questionnaire anyone able to read and write would be able to do pretty well?).

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Sorry, take another look.  This is tricky!"
msg_good <- "You got it!  Only the SRS and the SCQ are questionnaires for family members of subjects.  The rest are sophisticated diagnostic tools used by trained clinicians."
test_mc(correct = 3, feedback_msgs = c(msg_bad, msg_bad, msg_good, msg_bad))
```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:788490d588
## Spotlight on the SCQ

Take look at the Lifetime SCQ .pdf, and locate the scoring located at the end.  You can tell that this scanned document had been "used", as there are light carbon marks that show a score.  How would you describe the scoring of the SCQ?  All of the below are real scoring methods used at CAR in our psychometric instruments.  Which one corresponds to the SCQ?

*** =instructions
- There's a lookup table that gives you a value for a given total, converting it to a standarized score.
- The scoring gives you a percentile -- comparing this subject to a population.
- It's a summary score -- you just add up the score for each question to get a value.
- There is a binary "cutoff" or "threshold" that if met indicates one diagnostic outcome, and if not, a lack of that diagnosis.

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "Scoring can be complicated. Try again!"
msg_good <- "Yep, the SCQ has a summary score -- just a raw total that doesn't tell you much more than that."
test_mc(correct = 3, feedback_msgs = c(msg_bad, msg_bad, msg_good, msg_bad))
```



--- type:MultipleChoiceExercise lang:r xp:100 skills:1 key:e280908668
## Types of scoring

In psychometric evaluations, there are many ways to provide scores, often used in tandem on the same measure.  These include methods like:

- raw summary score (score is not compared to any other subjects)
- Z-score (how many standard deviations away from the mean of the norm is this subject?)
- Transformed or T-score (*not* the same as Student's T statistic or T-score in statistics!)
- severity score or other specialized comparison score (the ADOS-2 has one)
- cutoff or threshold scoring that classifies subjects into groups (DSM checklists are one example)
- domain-specific scores (which calculate a score on only certain items in an instrument that measure the same thing)
- total scores (which include all domains)
- composite scores (combinations of scores from different domains, but not all items)
- percentiles (estimates of how subjects compare to the population at large)
- standardized scores (usually a method of re-shaping score data so that the mean is 100)
- consistency scores (how did subjects respond to questions asked in different ways?)
- imputation (how you handle missing scores -- the SRS is a good example of built-in imputation logic)

Understanding scoring is a huge part of working with human subject data at CAR.  Consider, for example, the ADOS-2 Module 3 (check it out by downloading the image from the REDCap library we've been working with!)

What kind of scoring do you see?

*** =instructions
- raw scores at the domain and total level, consistency scores, composite scores, and percentiles
- percentiles at the domain and total level, cutoff/threshold scoring, and standardized scores
- imputation logic, consistency scores, Z-scores, and percentile estimates
- domain and total level scoring, cutoff/threshold scoring, and severity scores

*** =hint

*** =pre_exercise_code
```{r}

```


*** =sct
```{r}
msg_bad <- "Scoring can be complicated. Try again!"
msg_good <- "You're right.  The ADOS-2 includes scores at the domain-level, composite, and total level, as well as giving a calculted severity score, which is a comparison score, and a cutoff or diagnostic category.  Additionally, there's imputation logic (clinicians can code for 'N/A' in the record booklet."
test_mc(correct = 4, feedback_msgs = c(msg_bad, msg_bad, msg_bad, msg_good))
```
