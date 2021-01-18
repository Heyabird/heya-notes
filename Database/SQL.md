# SQL
- Structured Query Language (SQL) is a language used for interacting with [[Relational Database]] Management Systems (RDMS).
- SQL implementations vary between systems.
- SQL is actually a hybrid of 4 different types of languages.
	1. Data query language
	2. Data definition language
	3. Data control language
	4. Data manipulation language


#### Queries
- Set of instructions given to the RDMS that tells the system what data you want it to retreive for you. The goal is to only get the data you need. For example:
```sql
SELECT employee.name, employee.age
FROM employee
WHERE employee.salary > 30000;
```

#### Main Data Types
- INT -- Whole number
- DECIMAL (M,N) -- Decimal. M is the total number of digits. N is the total number of digits after the decimal.
- VARCHAR(1) -- String. (1) represents the max number of characters.
- BLOB - Binary large object. Structure that can store large amounts of binary data. Often used for images or files.
- DATE - 'YYYY-MM-DD'
- TIMESTAMP - 'YYYY-MM-DD HH:MM:SS'


<hr>

## Working with Schema

#### Create a Table
- The convention is to use all caps when writing SQL reserved words.
- End all SQL commands with a semicolon (;).

For example, this code:
 
```sql
CREATE TABLE student (
	student_id INT PRIMARY KEY,
	name VARCHAR(20),
	major VARCHAR(20)
	);
```

which is the same as this code:
```sql
CREATE TABLE student (
	student_id INT,
	name VARCHAR(20),
	major VARCHAR(20),
	PRIMARY KEY(student_id)
	);
```

The above will create:

student id | name | major
-----------|-------|----------
1                | Kate   | sociology
2               | Jack   | Biology
3               | Claire | English
4               | Jack   | Biology

To view the table, you can run:
```sql
DESCRIBE student;
```

#### Delete a Table
```sql
DROP TABLE student;
```

#### Modify a Table
Add a column:
```sql
ALTER TABLE student ADD gpa DECIMAL(3,2);
```
Drop a column:
```sql
ALTER TABLE student DROP COLUMN gpa;
```

#### Constraints
```sql
CREATE TABLE student (
	student_id INT PRIMARY KEY,
	name VARCHAR(20) NOT NULL,
	major VARCHAR(20) UNIQUE
	);
```
- NOT NULL - cannot be empty / null
- UNIQUE - has to be unique
<hr>

## Working with Data

#### Inserting Data
```sql
INSERT INTO student VALUES(1, 'Jack', 'Biology');
```

If you didn't want to fill in data for all columns: 
```sql
INSERT INTO student(student_id, name) VALUES(2, 'Kate');
```

#### View
```sql
SELECT * FROM student;
```
