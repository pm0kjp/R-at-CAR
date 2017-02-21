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
