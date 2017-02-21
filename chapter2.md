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

*Note: If this is the first time you've logged in, you'll need to fill out your "Profile".  Make sure that the primary email address you add there is your CHOP email!  After finishing your profile, you may need to "return to previous page" and login again.*

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


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:b560dfee00
## Your First REDCap Database!

Now it's time to create your first REDCap database.  If you're not already logged in to CHOP's REDCap instance, do so now.  Go to the main REDCap home page.  If you're within a project, you can get there by clicking on the REDCap logo in the upper left.  Not in a project?  Then just click on the Home tab.  Familiarize yourself with the information that's available on this Home tab -- boilerplate security language, a "Getting Started" document, your username and profile, the version of REDCap, and more!

Now, time to create your first database!

- Click on "Create New Project"
- Add a meaningful title, like "Joe's First REDCap DB".  
- For Purpose, choose "Practice / Just for fun."  
- Add some project notes!
- In answer to the question "Start project from scratch or begin with a template?", choose the template option, and select "Classic Database."

What data collection instruments are in your project?
*** =instructions
-  Demographics, Consent, Baseline Data, Final Data
-  Demographics, Baseline Data, Month 1 Data, Month 2 Data, Month 3 Data, Completion Data
-  Consent, Genomic Data, Phenotypic Data, Outcome Measure 1, Outcome Measure 2
-  Consent, Baseline Data, Genomic Data, Month 1 Data, Month 2 Data, Month 3 Data

*** =hint
- Can't log in to REDCap?  Are you using the correct CHOP id and password?
- Can't create a database?  Does your profile have your CHOP email address as your primary address?

*** =pre_exercise_code
```{r}
# None
```

*** =sct
```{r}
msg_bad <- "No, I don't think you've gotten it quite right!"
msg_good <- "You've got it!  Congrats on making your first REDCap database!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_good, msg_bad, msg_bad))
```
--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:45aefb0a9f
## Edit a field

The next few questions depend on your being logged in to REDCap and accessing the following page: [https://redcap.research.chop.edu/index.php?action=training](https://redcap.research.chop.edu/index.php?action=training).

Please watch the second video, "Detailed Overview", in the "Just Getting Started?" section.  You need to have your own REDCap database open so you can follow along with the Detailed Overview Video.

Go into the Online Designer for your database, and click on the Demographics instrument in order to edit it.
Then edit the question that has the text "Date subject signed consent".

Which field shows up as a "Small reminder text" beneath the data entry box, reading YYYY-MM-DD?

*** =instructions
- Field Annotation
- Validation
- Field Label
- Field Note
*** =hint

Try rewatching starting at 4:50 to see how to get into the Online Designer and edit a field.

*** =pre_exercise_code
```{r}
# None
```

*** =sct
```{r}
msg_bad <- "No, not quite!"
msg_good <- "You're right.  A Field Note helps prompt data entry personnel so that they input the right kind of data with the right format!"
test_mc(correct = 4, feedback_msgs = c(msg_bad, msg_bad, msg_bad, msg_good))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:23033c3f56
## Using the Online Designer

This question depends on your being logged in to REDCap and accessing the following page: [https://redcap.research.chop.edu/index.php?action=training](https://redcap.research.chop.edu/index.php?action=training).  This question assumes you have watched the second video, "Detailed Overview", in the "Just Getting Started?" section.  

You need to have your new REDCap database open.

Using what you've learned, go into the Online Designer for your database, and click on the Demographics instrument in order to edit it.

Then edit the question that has the text "Date subject signed consent".  You can do this by clicking on the pencil icon.

Which field shows up as a "Small reminder text" beneath the data entry box, reading YYYY-MM-DD?

*** =instructions
- Field Annotation
- Validation
- Field Label
- Field Note
*** =hint

Try rewatching starting at 4:50 to see how to get into the Online Designer.  The video shows how to create new fields, but it's easy to edit existing fields by clicking on the pencil.

*** =pre_exercise_code
```{r}
# None
```

*** =sct
```{r}
msg_bad <- "No, not quite!"
msg_good <- "You're right.  A Field Note helps prompt data entry personnel so that they input the right kind of data with the right format!"
test_mc(correct = 4, feedback_msgs = c(msg_bad, msg_bad, msg_bad, msg_good))
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:3fc1f46a4a
## Data Entry

This question depends on your being logged in to REDCap and accessing the following page: [https://redcap.research.chop.edu/index.php?action=training](https://redcap.research.chop.edu/index.php?action=training).  This question assumes you have watched the second video, "Detailed Overview", in the "Just Getting Started?" section.  

You need to have your new REDCap database open.

Using what you've learned, add some new data for subject CAR-123.  The data you're going to enter is a completely blank Demographics form.  Don't add or change anything, and click "Save Record".

What error message do you receive?

*** =instructions
- "Please add First Name, Last Name before saving."
- "Invalid Consent date -- please check data!"
- "Incomplete data, would you like to continue?"
- No error message, the record saves with the message "Study ID CAR-123 successfully edited".

*** =hint

Try rewatching starting at 8:30 to see how to add data.  In the case of your database, you won't see an "Add new record" button, you'll see a box that is labeled "Enter a new or existing Study ID".  That's where you'll enter your subject's ID and then hit enter.

*** =pre_exercise_code
```{r}
# None
```

*** =sct
```{r}
msg_bad <- "No, not quite!"
msg_good <- "You're right.  There are no errors, but we can imagine that we want errors to pop up.  We should make some of our fields 'required'."
test_mc(correct = 4, feedback_msgs = c(msg_bad, msg_bad, msg_bad, msg_good))
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:f7976d6617
## Give yourself API access

This question depends on your being logged in to REDCap and accessing the following page: [https://redcap.research.chop.edu/index.php?action=training](https://redcap.research.chop.edu/index.php?action=training).  This question assumes you have watched the second video, "Detailed Overview", in the "Just Getting Started?" section.  

You need to have your new REDCap database open.

Go into User Rights and give yourself both kinds of API access: API Export and API Import/Update.  Then hit "Save Changes".
Reload the page in your browser, and you should see a change in the "Applications" section of the page.  What two new applications are available to you?

*** =instructions
- API and API Sandbox
- API Export and API Import / Update
- API and API Playground
- API Development and API Production

*** =hint
Watch the Detailed Overview video at around 11:00 to see how to access User Rights.  Click on your name to be able to edit your privileges.

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
msg_bad <- "No, that's not the pair I'm looking for."
msg_good <- "You got it.  API lets you request, access, or reset your API token, while API Playground allows you to practice using the API and see how various languages encode the call to the API."
test_mc(correct = 3, feedback_msgs = c(msg_bad, msg_bad, msg_good, msg_bad))
```
