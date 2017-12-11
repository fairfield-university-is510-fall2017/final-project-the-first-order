# The First Order
## A New Hobby for our Troopers - NFL

### Relational Databases and SQL
One of the most important parts of creating a new database is the planning. It is easy to change a recipe,  but harder to remvoe the apple from an apple pie. This means that it is comparatively easier to make changes to a database in the design stage of a project, as opposed to making changes to the structure of a database after it has been created. The purpose of this report is to create a database containing information about National Football League (NFL) match-ups, followed by merging in another NFL data set that is not part of the original database. To finish, some simple analysis will then be conducted on the newly merged database. This merging is underway to appease Supreme Leader Snoke, as he has grown bored with his existing databases and wishes to have a new one on which to conduct analysis.

The database model we will be examining in this report is the Relational Database Model, also known as relational database management system (RDMS). It is based on the relational model invented by Edgar F. Codd, of IBM's San Jose Research Laboratory. Most databases in widespread use are based on the relational database model. Codd now has the definition of a "normalized" model named after him, along with a man called Raymond Boyce, who augmented Codd's inital work to create the Boyce - Codd Normal Form in 1974. We will discuss normalization later in this report.

The American National Standards Institute (ANSI) standard language for dealing with relational databases is call Structured Query Langauge, or SQL for short. SQL first appeared in 1974, and became ANSI standard in 1986. SQL is not considered a full programming language, and thus is relatively easy to pick up due to the simple nature of the language.

### Our NFL Data
Our NFL database contains information about the first week of games in the 2016 NFL season. Initially, it was structured:


|Game| Team | Quarterback | Conference | Division | Stadium | City | College | Attendence | Score | Total Yards | Turn Overs | 1st Downs |Home/Away|
|-----|------|-------------|------------|----------|---------|------|---------|------------|-------|-------------|------------|-----------|---------|
|    |      |             |            |          |         |      |         |            |       |             |            |           |         |    |


Our table is almost in 1NF, or first normal form. First normal is defined as being a relation and having a primary key. A relation is defined:
* Rows contain data about an entity.
* Columns contain data about atributes of the entities.
* All entries in a column are of the same kind.
* Each column has a unique name.
* Cells of the table hold a single value.
* The order of the columns is unimportant.
* The order of the rows is unimportant.
* No two rows are identical.

We are merely missing a primary key. 
_GameID_, _QBName_, TeamName, Conference, Division, Stadium, City, College, Attendence, Score, Total Yards, Turn Overs, 1st Downs, Home/Away

Next, we convert the data set to second normal, starting with a list of dependencies:

* GameID -> TeamName, Conference, Division, Stadium, City, Attendence, Score, Total Yards, Turn Overs, 1st Downs, Home/Away
* QBName ->  College
* TeamName -> Conference,Division
* Stadium -> City

Due to the fact we have a composite key, we see that we have non key attributes that can be determined by part of the primary key, thus failing the 2NF requirements. So we restructure:

GAMES( <u>GID</u>, TeamName, Conference, Division, Stadium, City, Attendence, Score, Total Yards, Turn Overs, 1st Downs, Home/Away )
QUARTERBACKS( <u>QBID</u>,___QBName___ , College )

In order to make it 3NF, it must be 2NF and have no non primary attributes that are dependent on any other non primary attributes. In order to correct this, we restructure again:

GAMES( <u>GID</u>___GameID___ , *TeamName*, *Stadium*, Attendence, Score, Total Yards, Turn Overs, 1st Downs, Home/Away )
QUARTERBACKS( ___QBName___ , College )
TEAMS( ___TeamName___, Conference, Division)
LOCATONS( ___Stadium___ , City)

Finally, we take steps to transition to Boyce-Codd Normal Form. Boyce-Codd is needed for normalization due to anomalies still being present in 3NF because of functional dependencies.

GAMES( ___GameID___ , *HomeTeam*, *AwayTeam*, *Stadium*, Attendence, Score, Total Yards, Turn Overs, 1st Downs)
GAMESTATISTICS( *GameID*, *QBName*, *TeamID*, Score, Total Yards, Turn Overs, 1st Downs)
QUARTERBACKS( ___QBName___ , College )
TEAMS( ___TeamName___, Conference, Division)
LOCATONS( ___Stadium___ , City)

Finally we create our ERD to visualise our database.

![ERD](https://github.com/fairfield-university-is510-fall2017/final-project-the-first-order/blob/master/Football_ERD.PNG)

### Creating the Database
We have our ERD, the next step is to create the database. This is done with *Data Definition Language* or DDL. Our database is created here (https://github.com/fairfield-university-is510-fall2017/final-project-the-first-order/blob/master/DDL.ipynb)

DDL is a language used to describe the structure of a database, specifically, it is used to create, modify, and drop database structures. 

In order to create the tables for our database, we use Create Table Statements, allowing us to give our tables names, as well as define all of the columns and indexes, meaning create column names along with their data types and constraints. When determining the datatype to declare for each column, we think about the nature of the data and it's intended use. Once the data types are determined, we place constraints on the columns to signify the following:
* Does the column accept NULL values?
* Must all column values be unique?
* Should a value be assigned to the attribute when a new row is added?
* Do we want to use a serial number generator to populate the column?

Below is a sample of DDL language used to create our NFL database:
<insert SQL code>

### Inserting Values to the Database
*Data Manipulation Language*, or DML, is a language used to describe the processing of a database. Our database is populated here (https://github.com/fairfield-university-is510-fall2017/final-project-the-first-order/blob/master/DML.ipynb)

SQL DML statements  are used to query, insert, modify, and delete data. Now that our database is structured, we will use DML to insert the data into our newly created tables.

In order to add the data into the tables, we utlize the Insert Into command, along with a select statement:
<insert SQL code>
  
With our NFL database structured and populated, we are ready to merge additional data sets. 

### NFL Analysis

![Avg Yards Per Play]( https://github.com/fairfield-university-is510-fall2017/final-project-the-first-order/blob/master/Avg_Yards_Per_Play.png “Avg Yards Per Play”)

![Total Turnovers by Team]( https://github.com/fairfield-university-is510-fall2017/final-project-the-first-order/blob/master/Total_Turnovers_by_Team.png “Total Turnovers by Team”)

![Week 1 Yards Gained by Division and Conference]( https://github.com/fairfield-university-is510-fall2017/final-project-the-first-order/blob/master/Avg_Total_W1_Yards_by_Division_and_Conf.png “Week 1 Yards Gained by Division and Conference”)

![ Week 1 Yards Gained]( https://github.com/fairfield-university-is510-fall2017/final-project-the-first-order/blob/master/Avg_Total_W1_Yards_Per_Team.png “Week 1 Yards Gained”)

![Average Points Scored]( https://github.com/fairfield-university-is510-fall2017/final-project-the-first-order/blob/master/Avg_Points_Scored_by_Division_and_Conf.png “Average Points Scored”)






