# Relational Database

### Database
src: https://www.youtube.com/watch?v=HXV3zeQKqGY
- Database (DB)
- Database management system (DBMS) - handles security, backups, importing/exporting data, concurrency, interacts with software apps / programming interfaces
	- example: [[MySQL]]
- C.R.U.D. (Create, Read, Update, Delete) are the 4 main operations we can do with a db.
- 2 types of db:
	- Relational (SQL)
	- Non-relational (noSQL)

### Relational Database

Relational db is in a form of a table with columns and rows.
It is important to have a column devoted for **primary keys**, a unique identifier for each row. In the example below, student id is a _surrogate key_ since it doesn't have mapping in the real world outside the db.

student id | name | major | partner_id
-----------|-------|----------|------
1                | Kate   | sociology | 2
2               | Jack   | Biology    | 1
3               | Claire | English     | NULL
4               | Jack   | Biology     | 5

For the example below, email acts as the primary key. Email is a _natural key_.

email | pw | type | student_id
------|-----|-------|----------
haha@bird.com|password|admin|2
wow@bird.com|passwo0d|free|1

**Foreign key** is an attribute in a db table that will link us to another db table. A table can have more than 1 foreign key.

**Composite key** is a set of two attributes that only together act as a unique identifier for the table.

In the example below, the Works_With table has two foreign_ids that act as a composite primary key.

![[Screenshot from SQL tutorial.png.png]]

<hr>
