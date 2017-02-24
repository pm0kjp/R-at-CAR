---
title       : CAR's Tabular Data Warehouse
description : CAR's tabular data warehouse has lots of data available for your use

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:a2b82c380f
## Intro to CAR's Tabular Data Warehouse

Give the following README a look. You'll have to scroll down to read it! [https://github.research.chop.edu/CenterForAutismResearch/Data-Warehouse-New-SQL-Structure](https://github.research.chop.edu/CenterForAutismResearch/Data-Warehouse-New-SQL-Structure)

What describes the principle role of the code in this repository?
*** =instructions
- Downloading data from REDCap into a SQL server
- Providing statistical analysis and data visualization tools
- Creating a SQL data warehouse that pools and cleans REDCap data
- Creating websites that provide for online data collection tools

*** =hint
Give the README a close read, and consider the title of the repository.

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "Oops, not quite!  Try again."
msg_success <- "Exactly! The Data Warehouse New SQL Structure repository both sets up SQL table structure and populates tables to provide study-specific and multi-study data storage.  This is helpful when people want data across multiple studies."
test_mc(correct = 3, feedback_msgs = c(msg_bad, msg_bad, msg_success,  msg_bad))
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:90066c2ce2
## Understanding the Raw Pooled Data Script

Take a look at the first hundred lines or so of [https://github.research.chop.edu/CenterForAutismResearch/Data-Warehouse-New-SQL-Structure/blob/master/raw_pooled_data.sql](the raw_pooled_data.sql) script.

What do you think the purpose of the script is?
- (A) Removing tables that have a name like `some_instrument_name_raw`
- (B) Building tables that have a name like `some_instrument_name_raw` 
- (C) Populating tables that have a name like `some_instrument_name_raw`
*** =instructions
- (A) and (B) only
- (A), (B), and (C)
- (B) and (C) only
- (B) only

*** =hint
A list of several important commands in SQL can be found at [https://www.w3schools.com/sql/sql_quickref.asp](https://www.w3schools.com/sql/sql_quickref.asp). 

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "Oops, not quite!  Try again."
msg_success <- "Exactly! The purpose of the raw_pooled_data.sql script is to destroy the table if it currently exists and rebuild it, but empty, with no data being added just yet.  We get fresh data from REDCap every time we rebuild the data warehouse, so we remove old tables entirely and rebuild them from scratch."
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_bad, msg_bad, msg_bad))
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:d6b31655c7
## Study-Specific SQL

Once we have a "landing spot" for raw pooled data (pooled here means including studies from several different sources), we want to bring in the data that will populate the raw pooled data tables.  

Look at the first 70 lines of [https://github.research.chop.edu/CenterForAutismResearch/Data-Warehouse-New-SQL-Structure/blob/master/4880.sql](the 4880.sql script).  What do you think is happening here?

- (A) A table is destroyed
- (B) A table is built
- (C) Data is pulled into the table from a CSV
- (D) Data is copied from the table into a raw pooled table

*** =instructions
- (A) and (B) only
- (A) through (D)
- (B) through (D)
- (B) and (C) only


*** =hint
A list of several important commands in SQL can be found at [https://www.w3schools.com/sql/sql_quickref.asp](https://www.w3schools.com/sql/sql_quickref.asp). 

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "Nope, that's not it!"
msg_success <- "Exactly! Each study-specific script first destroys an instrument table (an instrument = any tabular data form) if it currently exists and rebuilds it, but empty, with no data being added just yet.  Then we load data into that table from a .csv (which we've gotten from REDCap using the API in a previous step).  Finally, we copy the data contained in that study-specific table into the raw table corresponding to that instrument."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:524289ea84
## A review so far

CAR's tabular data warehouse is complex!  This is our methodology:

- (1) For each study, download CSV's from each instrument in the study (could be one, could be dozens!).  This takes place using the API, using code you haven't seen yet.
- (2) For each kind of instrument (an instrument means a single kind of questionnaire, like ADHD-Home or the ADOS Module 3), create an empty table that reflects all the fields we expect to have for that questionnaire, regardless of the source of the data.
- (3) For each study, create a SQL table for each downloaded CSV we did in step (1), load the CSV data into it, and also add that data to the integrated or pooled data table that holds data for that particular instrument across various studies.
- (4) Once all the studies are loaded, and all the pooled raw data tables are populated, take the data in the pooled raw data tables and clean it to create a pooled cleaned table for each instrument.

What kind of pooled tables do we have?


*** =instructions
- Pooled raw data (unaltered -- or minimally altered -- data coming as it exists in REDCap databases)
- Pooled cleaned data (data that comes from multiple sources but has undergone cleaning to make it more useful and/or trustworthy)
- Both pooled raw and cleaned data
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "Nope, that's not it!"
msg_success <- "Yep, you got it. It's important to clean the data well, doing things like removing meaningless / empty rows, scoring the data in ways not already done in the source database, improving variable names, and so on.  The easiest way for us to do this is to have one single 'dirty' (raw) pooled table that we use as our source, then we apply various commands to clean that data and create a pooled cleaned table."
test_mc(correct = 3, feedback_msgs = c(msg_bad, msg_bad, msg_success))
```

