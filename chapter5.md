---
title       : Accessing CAR's Tabular Data Warehouse with R
description : In this chapter, you'll learn how to access CAR's tabular data warehouse using R.  We'll cover connecting to the data warehouse, retrieving data, and cleaning up after yourself!


--- type:NormalExercise lang:r xp:100 skills:1 key:14335d7bec
##  Accessing the Data Warehouse

You won't be able to access the actual CAR Tabular Data Warehouse from this site, as it's firewalled off (also, hello!  PHI is on that server!).  You will probably be able to access a *public* MySQL database, however, and this can help you understand the process.  We'll access the [UC Santa Cruz Genome Browser](https://genome.ucsc.edu/index.html), and we'll be very careful not to drive excessive traffic to their servers!

We'll be using a package called "RMySQL".  RMySQL allows you to create a database connection that persists over time and allows you to reach into a MySQL instance, at the server level or at the database level. It, in turn, relies on DBI, a package that can make connections with various flavors of SQL databases.


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

- host: What is the URL of the server running MySQL?  In our case, we're going to use genome-mysql.cse.ucsc.edu
- user: What's the user name?  In our case, "genome".
- password: What's the password for that user?  In our case, there is none -- we can leave this blank!
- db:  What specific database do you want to connect to?  If you don't know, you can leave this blank.

After connecting, you have an open connection object.  It's polite to drop that connection when it's not being used.  Since we're relying on the kindness of strangers, we'll definitely be polite!

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
                                   host="genome-mysql.cse.ucsc.edu")
                                
# List available databases.  
# The part in quotes is a SQL query -- you could also issue this query directly into SQL -- it's independent from R.  R is just passing that query to the SQL server.
dbGetQuery(myConnection, "SHOW DATABASES;")

# Let's be friendly!
dbDisconnect(myConnection)
```

*** =sct
```{r}
test_function("dbConnect", args = c("user", "host"),
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


