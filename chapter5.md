---
title       : Accessing a MySQL Database with R
description : In this chapter, you'll learn how to access a MySQL database like CAR's tabular data warehouse using R.  We'll cover connecting to the data warehouse, retrieving data, and cleaning up after yourself!


--- type:NormalExercise lang:r xp:100 skills:1 key:14335d7bec
##  Using RMySQL

You won't be able to access the actual CAR Tabular Data Warehouse from this site, as it's firewalled off (also, hello!  PHI is on that server!).  You will be able to access a *public* MySQL database, however, and this can help you understand the process.  We'll access some simulated data that's similar to what you would see in the CAR Tabular Data Warehouse.

A quick note about this database: it contains *completely fabricated* data.  It is meant to look realistic, so we have some subjects with more symptoms and others meant to look like typically developing controls, but it does *not* come from actual subjects.  It is 100% simulated.

We'll be using a package called "RMySQL".  RMySQL allows you to easily create a MySQL database connection that persists over time and allows you to reach into a MySQL instance, at the server level or at the database level. It, in turn, relies on DBI, a package that can make connections with various flavors of SQL databases.


*** =instructions
Load RMySQL into your R session using the `library()` command.

*** =hint
`?library()` might help!

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# use library().
```

*** =solution
```{r}
library(RMySQL)
```

*** =sct
```{r}
test_function("library",
              not_called_msg = "You didn't call `library()`!",
              incorrect_msg = "You didn't call `library()` with the correct arguments.")
success_msg("Right on!  That's the first step.")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:6dbf1aeb3b
## Making a database connection

After loading RMySQL, you'll be able to make a database connection using dbConnect(). You'll need to use a few parameters:

- host: What is the URL of the server running MySQL?  In our case, we're going to use car-simulation-station.c9az8e0qjbgo.us-east-1.rds.amazonaws.com
- user: What's the user name?  In our case, "datacamp_user".
- password: What's the password for that user?  In our case, its "learn tabular data for fun and profit"  (yep, spaces and all!).  
- db:  What specific database do you want to connect to?  If you don't know, you can leave this blank (we will, for now!)

After connecting, you have an open connection object.  It's polite to drop that connection when it's not being used.  We'll definitely be polite and clean up after ourselves.

To disconnect we use dbDisconnect().

*** =instructions
Fill in the host and user parameters and see if you can make a connection.
You'll then issue a SQL command that will ask the SQL server to return all the databases.
All SQL commands end with a semicolon.
We've included code here that will show you all the databases available on this server.

*** =hint
Just copy and paste the user and host information into the ????? spots!


*** =pre_exercise_code
```{r}
library(RMySQL)
```

*** =sample_code
```{r}
myConnection <- dbConnect(MySQL(), user="???????", 
                                   host="???????")
                                
# List available databases.  
# The part in quotes is a SQL query -- you could also issue this query directly into SQL -- it's independent from R.  R is just passing that query to the SQL server.
dbGetQuery(myConnection, "SHOW DATABASES;")

# Let's be friendly!
dbDisconnect(myConnection)
```

*** =solution
```{r}
myConnection <- dbConnect(MySQL(), user="genome", 
                                   host="genome-mysql.cse.ucsc.edu",
                                   password="learn tabular data for fun and profit")
                                
# List available databases.  
# The part in quotes is a SQL query -- you could also issue this query directly into SQL -- it's independent from R.  R is just passing that query to the SQL server.
dbGetQuery(myConnection, "SHOW DATABASES;")

# Let's be friendly!
dbDisconnect(myConnection)
```

*** =sct
```{r}
test_function("dbConnect", args = c("user", "host", "password"),
              not_called_msg = "You didn't call `dbConnect()`!",
              incorrect_msg = "You didn't call `dbConnect()` with the correct arguments.")

test_function("dbGetQuery", 
              not_called_msg = "You didn't call `dbGetQuery()`!",
              incorrect_msg = "You didn't call `dbGetQuery()` with the correct arguments.")

test_function("dbDisconnect", 
              not_called_msg = "You didn't call `dbDisconnect()`!",
              incorrect_msg = "You didn't call `dbDisconnect()` with the correct arguments.")


success_msg("Good work! You were able to make a connection to a remote data server and see what databases are available to you.  Now scroll around on the right to see the various databases listed in your console.")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:259c740531
## Connecting to a specific database

We saw a number of databases at UCSC that we can connect to.  Let's choose caePb1, which I chose at random.  

After connecting to a specific database, we can do things like look at the various tables within the database, get data from specific tables, and more.  There are a couple of ways to think about using R and SQL together:

- You could become really good at SQL and do a lot of your data selection, combining, and reshaping in SQL, and bring the already beautiful data into R
- You could just do the basics in SQL -- get all the data from a table, for example, and do the selection, combining, and reshaping within R.

Generally I suggest the second approach, just to minimize the number of things that scientists have to learn in order to use the data in the CAR Tabular Data Warehouse.  But data analysts on the data team should be able to do either approach!

Let's get some information about the tables in the caePb1 database.


*** =instructions
Using dbConnect, connect to the database caePb1.  Call your connection myConnection.  As a reminder, the host is genome-mysql.cse.ucsc.edu, the user is genome.  

Then use dbGetQuery to issue the SQL query "SHOW TABLES;".  Capitalization is not that important in SQL keywords, but the tradition is to capitalize them.  Capitalization does matter, however, in things like table names or database names!  dbGetQuery has two parameters: the connection variable (in your case myConnection) and the quoted query.

*** =hint
- Try dbConnect(MySQL(), user="genome", 
                         host="genome-mysql.cse.ucsc.edu", 
                         db="caePb1")



*** =pre_exercise_code
```{r}
library(RMySQL)
```

*** =sample_code
```{r}
# Make a connection to the MySQL database.  You'll add three parameters: host, user, and db.
myConnection <- dbConnect(MySQL(),  ???????)

# Issue a SQL query and return the results.  You'll need two parameters here.  You don't have to label them.
dbGetQuery(????, "?????")

# Let's be friendly and respectful of resources!
dbDisconnect(myConnection)
```

*** =solution
```{r}
# Make a connection to the MySQL database.  You'll add three parameters: host, user, and db.
myConnection <- dbConnect(MySQL(), user="genome", 
                                   host="genome-mysql.cse.ucsc.edu", db="caePb1")

# Issue a SQL query and return the results.  You'll need two parameters here.  You don't have to label them.
dbGetQuery(myConnection, "SHOW TABLES;")

# Let's be friendly and respectful of resources!
dbDisconnect(myConnection)
```

*** =sct
```{r}
test_function("dbConnect", args = c("user", "host", "db"),
              not_called_msg = "You didn't call `dbConnect()`!",
              incorrect_msg = "You didn't call `dbConnect()` with the correct arguments.")

test_function("dbGetQuery", 
              not_called_msg = "You didn't call `dbGetQuery()`!",
              incorrect_msg = "You didn't call `dbGetQuery()` with the correct arguments.")

test_function("dbDisconnect", 
              not_called_msg = "You didn't call `dbDisconnect()`!",
              incorrect_msg = "You didn't call `dbDisconnect()` with the correct arguments.")


success_msg("Good work! You were able to make a connection to a remote database and see what tables are available to you.  Now scroll around on the right to see the various tables listed in your console.")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:1d7b5e9b29
## Getting the contents of a table

So far, you can connect to a data *server*, connect to a specific database on a server, and list tables.  In the UCSC example, there were many databases, each with multiple tables containing data relating to genomics.  However, in the case of CAR's Tabular Data Warehouse, we're really only talking about a single database, with many tables.  As a reminder, the tables in the CAR Tabular Data Warehouse include:

- Study and instrument specific tables (e.g. `study_7275_adhd_home`, which contains the ADHD Home instrument for the study named 7275)
- Pooled raw tables (e.g. `adhd_home_raw`, which contains unaltered ADHD Home data from multiple studies)
- Pooled cleaned tables (e.g. `adhd_home_cleaned`, which contains improved, enriched, or validated ADHD home data from multiple studies).

Most frequently, you'll want to get data from a single table into an R object.  Say, for example, you want to do analysis on all the ADHD Home instruments and compare them to ADHD School.  It's a good bet you'll want to load all the data in the table `adhd_home_cleaned` into one R object, maybe named adhdHome, and all the data from `adhd_school_cleaned` into a different R object, say, adhdSchool.  Then you could either compare the two -- which has more subjects?  Which has higher rates of reporting for certain symptoms? -- or combine the data (for the subjects that have *both* a home and a school record, create a table that contains both reports).

Let's practice getting a table from SQL and importing its content into R.


*** =instructions
We've given you all the previous code that connects you to the database.  You need to create an R object titled mRNA that contains all the items (use SELECT *) from the table all_mrna.  Note that in table names (and other names -- column names, database names, etc.), capitalization matters!

Once you populate the table mRNA, please do the following:

- View the first few rows, using head()
- Create a table that shows the values of the `strand` column (use `table()`)



*** =hint
- Don't forget to use dbGetQuery with two parameters -- the connection, and the quoted SQL query.
- `?head()` might help you!
- `?table()` might help you!

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Make a MySQL connection
library(RMySQL)
myConnection <- dbConnect(MySQL(), user="genome", 
                                   host="genome-mysql.cse.ucsc.edu", 
                                   db="caePb1")

# Create a data frame from a SQL table                                 
mRNA <- # Add code here!

# Be polite!
dbDisconnect(myConnection)

# Now you have a data frame, and you've politely dropped the connection.

# View the first few rows of your data frame, using head()

# Create a table that shows the values of the strand column (use table())
                                   
```

*** =solution
```{r}
# Make a MySQL connection
library(RMySQL)
myConnection <- dbConnect(MySQL(), user="genome", 
                          host="genome-mysql.cse.ucsc.edu", 
                          db="caePb1")

# Create a data frame from a SQL table                              
mRNA <- dbGetQuery(myConnection, "SELECT * from all_mrna")

  
# Be polite!
dbDisconnect(myConnection)

# Now you have a data frame, and you've politely dropped the connection.

# View the first few rows of your data frame, using head()
head(mRNA)

# Create a table that shows the values of the strand column (use table())
table(mRNA$strand)
```

*** =sct
```{r}
test_function("head",
              not_called_msg = "You didn't call `head()`!",
              incorrect_msg = "You didn't call `head()` with the correct arguments.")
test_function("table",
              not_called_msg = "You didn't call `table()`!",
              incorrect_msg = "You didn't call `table()` with the correct arguments.")
test_object("myConnection")
test_object("mRNA")
success_msg("Right on!  That's the first step.")
```
