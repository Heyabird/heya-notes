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
	major VARCHAR(20) DEFAULT 'undecided'
	);
```
- NOT NULL - cannot be empty / null
- UNIQUE - has to be unique
- DEFAULT - default value
- AUTO_INCREMENT - data automatically incremented by 1 

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

#### Updating Rows

To update:
```sql
UPDATE student
SET major = 'Bio'
WHERE major = 'Biology';
```

To update multiple values:
```sql
UPDATE student
SET name = 'Tom', major = 'Bio'
WHERE student_id = 1;
```

To update all values in a column:
```sql
UPDATE student
SET major = 'undecided'
```

You can also use OR logic or AND logic:
```sql
UPDATE student
SET major = 'Biochemistry'
WHERE major = 'Biology' OR 'Chemistry';
```

### Deleting Rows

To delete all rows:
```sql
DELETE FROM student
```

You can also be more specific:

```sql
DELETE FROM student
WHERE name = 'TOM' AND major = 'Undecided'
```

<hr>

## Writing Queries

#### Getting data
```sql
SELECT * FROM student;
```

To select values from specific columns:
```sql
SELECT name, major FROM student;
```

You can also specify the table:
```sql
SELECT student.name, student.major
```

#### Ordering
```sql
SELECT student.name, student.major
FROM student
ORDER BY name DESC;
```
By default ordering is in ascending order (ASC), but you use descending order (DESC).

You can also order by columns:
```sql 
ORDER BY major, student_id DESC;
```

#### Filtering

You can use: <, >, <=, >=, <> (not equal to), AND, OR, NOT, IN

```sql
SELECT *
FROM student
WHERE major <> 'Biology' OR name IN ('Claire', 'Kate', 'Mike');
```

#### Limiting
gives back specific number of rows.
```sql
LIMIT 2;
```

#### Distinct
```sql
SELECT DISTINCT Country from Customers;
```

#### Combining AND, OR and NOT
```sql
WHERE Country = 'Germany' AND (City='Berlin' OR City='Munchen');
```
```sql
WHERE NOT Country = 'Germany' AND NOT Country = 'USA'
```

#### Insert Into
```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)  
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```

#### LIKE
To select all customers with a CustomerName starting with "a":
```sql
SELECT * FROM Customers  
WHERE CustomerName LIKE 'a%';
```

#### ALIASES/AS
```sql
SELECT column_name AS alias_name
FROM table_name;
```

<hr>

## SQL Functions
#### COUNT
```sql
SELECT COUNT(emp_id) FROM employee;
```
#### AVG
```sql
SELECT AVG(salary) FROM employee;
```
#### SUM
```sql
SELECT SUM(salary) FROM employee;
```

#### Aggregation (SUM and GROUP BY)
```sql
SELECT COUNT(sex), sex FROM employee
GROUP BY sex;
```

<hr>

## Wild Card
= a way of defining different patterns to match data to
```sql
-- Find any client who are an LLC
SELECT * 
FROM client
WHERE client_name LIKE '%LLC';
```

- % = any number of characters
- _ = one character

```sql
--find any branch suppliers who are in the label business
SELECT * from branch_supplier
where supplier_name LIKE '%Label%';

--find any employee born in October
SELECT * from employee
WHERE birth_day LIKE '____-10%';
```

<hr>

## Union
= special SQL operator we can use to combine multiple select statements
```sql
--find all employee and branch names 
SELECT first_name FROM employee
UNION
SELECT branch_name FROM branch
UNION
SELECT client_name FROM client;
```
- the unioned tables need to have same number of columns retrieved
- they also need similar data types (like strings)
- the first select statement will become the column name, unless you use AS

<hr>

## Join

![[SQL Joins.png]]
```sql
SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee JOIN branch
ON employee.emp_id = branch.mgr_id
```

<hr>

## Sub/Nested Query
```sql
SELECT * FROM CUSTOMERS
WHERE ID IN (SELECT ID
	FROM CUSTOMERS
	WHERE SALARY > 4500);
```
