# The First Order
## A New Hobby for our Troopers - NFL

### Relational Databases and SQL
One of the most important parts of creating a new database is the planning. It is easy to change a receipe, harder to remvoe the apple from an apple pie. What this means is that is comparatively easier to make changes to a database in the design stage of a project as opposed to change the structure of a database after it has been created. The purpose of this report is to create a database containing information about National Football League matches, followed by merging in another NFL data set that was not part of the original database. To finish, some simple analysis will then be conducted on the new database. All this is being done to appease Supreme Leader Snoke, as he has grown bored with his existing databases and wishes to have a new one to conduct analysis on.

The database model will be examining in this report is the Relational Database Model, also known as relational database management system (RDMS). It s based on the relational model invented by Edgar F. Codd, of IBM's San Jose Research Laboratory. Most databases in widespread use are based on the relational database model. Codd now has the definition of a "normalised" model named after him, along with a man called Raymond Boyce who augmented Codd's inital work to create the Boyce - Codd Normal Form in 1974. We will discuss normalisation later in this report.

The ANSI standard language for dealing with relational databases is call Structured Query Langauge, or SQL for short. SQL first appeared in 1974, and became ANSI standard in 1986. SQL is not considered a full programming language, and thus is relatively easy to pick up due to the simple nature of the language.

### Our NFL Data
Our NFL database contains information about the first week of games in the 2016 NFL season. Initially it was structured:


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

Next, we make it second normal, first we list the dependencies:

* GameID -> TeamName, Conference, Division, Stadium, City, Attendence, Score, Total Yards, Turn Overs, 1st Downs, Home/Away
* QBName ->  College
* TeamName -> Conference,Division
* Stadium -> City

Due to the fact we have a composite key, we see that we have non key attributes that can be determined by part of the primary key, thus failing the 2NF requirements. So we restructure:

GAMES( ___GameID___ , TeamName, Conference, Division, Stadium, City, Attendence, Score, Total Yards, Turn Overs, 1st Downs, Home/Away )
QUARTERBACKS( ___QBName___ , College )

In order to make it 3NF, it must be 2NF and no non primary attributes are dependent are any other non primary attributes. In order to correct this we restructure again:

GAMES( ___GameID___ , *TeamName*, *Stadium*, Attendence, Score, Total Yards, Turn Overs, 1st Downs, Home/Away )
QUARTERBACKS( ___QBName___ , College )
TEAMS( ___TeamName___, Conference, Division)
LOCATONS( ___Stadium___ , City)

Finally, in order to make it Boyce-Codd Normal Form. Boyce-Codd is needed for normalisation due to anomalies still being present in 3NF because of functional dependencies.

GAMES( ___GameID___ , *HomeTeam*, *AwayTeam*, *Stadium*, Attendence, Score, Total Yards, Turn Overs, 1st Downs)
GAMESTATISTICS( *GameID*, *QBName*, *TeamID*, Score, Total Yards, Turn Overs, 1st Downs)
QUARTERBACKS( ___QBName___ , College )
TEAMS( ___TeamName___, Conference, Division)
LOCATONS( ___Stadium___ , City)

Finally we create our ERD to visualise our database.

![ERD](https://github.com/fairfield-university-is510-fall2017/final-project-the-first-order/blob/master/Football_ERD.PNG)

### Creating the Database
We have our ERD, the next step is to create the database. This is done with Data Definition Language or DDL. Our database is created here (https://github.com/fairfield-university-is510-fall2017/final-project-the-first-order/blob/master/DDL.ipynb)



