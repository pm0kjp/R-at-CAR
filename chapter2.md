---
title       : Understanding REDCap
description : REDCap is the principle collection method for CAR's tabular data

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:0e8ff0b7d4
## REDCap helps us with tabular data

REDCap is a product of Vanderbilt University and it has features that make it ideal for storing tabular data related to research.

Please read the following documents before proceeding:
[REDCap home page](https://redcap.research.chop.edu/)

REDCap does not offer which of the following?
*** =instructions
- a "Data Dictionary" template that allows you to do database design outside of REDCap
- a browser-based "Online Designer"
- an API that allows you to access REDCap from a programming environment
- a "Migrate to Qualtrics" module that allows for seamless data transfer

*** =hint
Read the entire page, including the sidebar!

*** =pre_exercise_code
```{r}
# No PEC
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
msg_data_dic <- "No, REDCap does allow you to work with a data dictionary:  'Using REDCap's stream-lined process for rapidly developing projects, you may create and design projects using 1) the online method from your web browser using the Online Designer; and/or 2) the offline method by constructing a data dictionary template file in Microsoft Excel, which can be later uploaded into REDCap.'"
msg_online_designer <- "No, REDCap does have a web-based 'Online Designer': 'Using REDCap's stream-lined process for rapidly developing projects, you may create and design projects using 1) the online method from your web browser using the Online Designer; and/or 2) the offline method by constructing a data dictionary template file in Microsoft Excel, which can be later uploaded into REDCap.'"
msg_api <- "No. REDCap has an API that we use very frequently: 'REDCap API - Have external applications connect to REDCap remotely in a programmatic or automated fashion.'"
msg_qualtrics <- "Yep, you got it!  Qualtrics is another survey engine that is not officially supported by CHOP.  Some studies need to use Qualtrics for some special functionality, but we have to be very careful not to store PHI there.  REDCap does not interface directly with Qualtrics."
test_mc(correct = 4, feedback_msgs = c(msg_data_dic, msg_online_designer, msg_api, msg_qualtrics))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:bb4ff05dee
## Starting With REDCap

Log in to CHOP's REDCap instance at [https://redcap.research.chop.edu/](https://redcap.research.chop.edu/).  Use your CHOP username and password that you use for other CHOP things, like email.

Which one of these is represented in the tabs across the top?
*** =instructions
- Download Center
- Copy Existing Project
- Training Resources
- API 

*** =hint

*** =pre_exercise_code
```{r}
# None
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
msg_bad <- "No, that's not a tab!"
msg_good <- "You obviously logged in.  Training Resources is our next destination!"
test_mc(correct = 3, feedback_msgs = c(msg_bad, msg_bad, msg_good, msg_bad))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:651f79c23d
## REDCap Getting Started Tutorials

The next few questions depend on you being logged in to REDCap and accessing the following page: [https://redcap.research.chop.edu/index.php?action=training](https://redcap.research.chop.edu/index.php?action=training).

Please watch the first video, "Brief Overview", in the "Just Getting Started?" section.

Which of the following kinds of data entry methods was NOT included in the video?
*** =instructions
- Signature Box, where a mobile user can sign his/her name or initials
- Drop-Down menus with one possible answer per line
- Checkboxes
- Date picker (clickable calendar)
- Radio buttons (clickable circles)
*** =hint

The video is just four minutes long, watch it again!

*** =pre_exercise_code
```{r}
# None
```

*** =sct
```{r}
msg_bad <- "No, this is a supported data entry method shown in the video!"
msg_good <- "You're right.  A signature box was not shown.  But that *is* a kind of data entry method you can add in REDCap!"
test_mc(correct = 1, feedback_msgs = c(msg_good, msg_bad, msg_bad, msg_bad, msg_bad))
```