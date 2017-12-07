# The First Order
## A New Hobby for our Troopers - NFL

### Relational Databases and SQL
One of the most important parts of creating a new database is the planning. It is easy to change a receipe, harder to remvoe the apple from an apple pie. What this means is that is comparatively easier to make changes to a database in the design stage of a project as opposed to change the structure of a database after it has been created. The purpose of this report is to create a database containing information about National Football League matches, followed by merging in another NFL data set that was not part of the original database. To finish, some simple analysis will then be conducted on the new database. All this is being done to appease Supreme Leader Snoke, as he has grown bored with his existing databases and wishes to have a new one to conduct analysis on.

The database model will be examining in this report is the Relational Database Model, also known as relational database management system (RDMS). It s based on the relational model invented by Edgar F. Codd, of IBM's San Jose Research Laboratory. Most databases in widespread use are based on the relational database model. Codd now has the definition of a "normalised" model named after him, along with a man called Raymond Boyce who augmented Codd's inital work to create the Boyce - Codd Normal Form in 1974. We will discuss normalisation later in this report.

The ANSI standard language for dealing with relational databases is call Structured Query Langauge, or SQL for short. SQL first appeared in 1974, and became ANSI standard in 1986. SQL is not considered a full programming language, and thus is relatively easy to pick up due to the simple nature of the language.

### Our NFL Data
Our NFL database contains information about the first week of games in the 2016 NFL season. Initially it was structured:


| Team | Quarterback | Conference | Division | Stadium | City | College | Attendence | Score | Total Yards | Turn Overs | 1st Downs |
|------|-------------|------------|----------|---------|------|---------|------------|-------|-------------|------------|-----------|
|      |             |            |          |         |      |         |            |       |             |            |           |
|      |             |            |          |         |      |         |            |       |             |            |           |
|      |             |            |          |         |      |         |            |       |             |            |           |

Our table is almost in 1NF, or first normal form. First normal is defined as (list defintion)

As we can see, we are merely missing a primary key. 
_Quarterback_, _
