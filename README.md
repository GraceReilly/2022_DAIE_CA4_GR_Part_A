# Part-A---Database-Design-SQL-Querying

LINK TO GITHUB

https://github.com/GraceReilly/Part-A---Database-Design-SQL-Querying.git

----------------------------------------------------------------



FIRST R NOTEBOOK 




---
title: "2022_DAIE_CA4_GR"
subtitle: 'Database Design & SQL Querying '
date: "2023-01-11"
output:
  pdf_document: default
  html_document: null
---

# Part A - Database Design & SQL Querying

## Student Name - Grace Reilly / Student ID - D00232395

### Contents

-   Connecting Database to SQLite and Displaying Data

```{r echo=FALSE, message=FALSE, warning=FALSE}
library(RSQLite)
library(DBI)

# Connect to SQLite database
con <- dbConnect(SQLite(), dbname = "~/CA1/daie_ca4_data.sqlite")


# Display Data
Team_Member_data <- dbReadTable(con, "Team_Member")
print(Team_Member_data)

asset_data <- dbReadTable(con, "asset")
print(asset_data)

library_data <- dbReadTable(con, "library")
print(library_data)

work_Item_data <- dbReadTable(con, "work_Item")
print(work_Item_data)

project_data <- dbReadTable(con, "project")
print(project_data)

# Close the database connection

dbDisconnect(con)

```





SECOND R NOTEBOOK



---
title: "R Notebook"
output:
  pdf_document: default
  html_document:
    df_print: paged
---

## Part A- Database Design & SQL Querying

## Student Name - Grace Reilly / Student ID - D00232395

### Contents

-   ER Diagram

-   Query 1. SELECT with WHERE, LIKE, and OR

-   Query 2. SELECT with DISTINCT and ORDER BY

-   Query 3. Inner Join

-   Query 4. Sub-query with SELECT

-   Query 5. SELECT across a date range

-   References

### Er Diagram

![](ER_Diagram.png)

### Queries

-   Query 1. Select with WHERE, LIKE, and OR

```{r echo=FALSE, message=FALSE, warning=FALSE}
    library(DBI)
    library(RSQLite)
    # Connecting to the SQLite database
    con <- dbConnect(SQLite(), dbname = "~/CA1/daie_ca4_data.sqlite")

    # running query on the work_item table to select all columns from the table that include the word deisgn
    result_select <- dbGetQuery(con, "SELECT * FROM work_Item WHERE name LIKE '%Design%' AND (team_member_id = 2 OR team_member_id = 4)")

    # the result for work_item including the word design are shown
    head(result_select)


    dbDisconnect(con)

```

-   Query 2. SELECT with DISTINCT and ORDER BY

```{r echo=FALSE, message=FALSE, warning=FALSE}
    library(DBI)
    library(RSQLite)
    # Connecting to the SQLite database
    con <- dbConnect(SQLite(), dbname = "~/CA1/daie_ca4_data.sqlite")


    # running query to select the distinct project name and project_id columns from the project table and showing the resulting in descending ord by project_id
    result_order_by <- dbGetQuery(con, "SELECT DISTINCT projectname, project_id FROM project ORDER BY project_id DESC")



    head(result_order_by)


    dbDisconnect(con)
```

-   Query 3. Inner Join

```{r echo=FALSE, message=FALSE, warning=FALSE}
library(DBI)
library(RSQLite)
con <- dbConnect(SQLite(), dbname = "~/CA1/daie_ca4_data.sqlite")

# Seleting columns from the project table where the project_id column is present in the work_item table. The team_member_id having a value of 2.
result_subquery <- dbGetQuery(con, "SELECT * FROM project
WHERE project_id IN (SELECT project_id FROM work_Item
                    WHERE team_member_id = 2)")


head(result_subquery)


dbDisconnect(con)

```

-   Query 4. Sub-query with SELECT

```{r echo=FALSE, message=FALSE, warning=FALSE}
    library(DBI)
    library(RSQLite)
    con <- dbConnect(SQLite(), dbname = "~/CA1/daie_ca4_data.sqlite")



    # Select all columns from the project table where the delivery_date is between the below dates.
    result_date <- dbGetQuery(con, "SELECT * FROM project
    WHERE deliverydate BETWEEN '2022-01-01' AND '2022-12-31'")



    head(result_date)


    dbDisconnect(con)
```

-   Query 5. SELECT across a date range

```{r echo=FALSE, message=FALSE, warning=FALSE}
    library(DBI)
    library(RSQLite)
    con <- dbConnect(SQLite(), dbname = "~/CA1/daie_ca4_data.sqlite")


    # Inner join for the team_member and work_item tables on the id column from the team_member table. Result is the join of work_item and team_member_id
    result_join <- dbGetQuery(con, "SELECT Team_Member.*, Work_Item.* FROM Team_Member
    INNER JOIN Work_Item ON Team_Member.id = Work_Item.team_member_id")


    head(result_join)

    dbDisconnect(con)
```

    ## References

-   Site - LearnSQL at: <https://learnsql.com/blog/sql-subquery-examples/> (Accessed 18 January 2023)

-   Youtube -SQL Tutorial - Full Database Course for Beginners at: <https://www.youtube.com/watch?v=HXV3zeQKqGY&ab_channel=freeCodeCamp.org> (Accessed 18 January 2023)

-   Site - SQL RDBMS Concepts at: <https://www.tutorialspoint.com/sql/sql-rdbms-concepts.htm> (Accessed 17 & 18 January 2023)

-   Site - Vertabelo at : <https://vertabelo.com/blog/normalization-1nf-2nf-3nf/> (Accessed 20 January 2023)




