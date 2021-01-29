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

#### IF NOT EXISTS
```sql
CREATE TABLE IF NOT EXISTS mytable ( 
	column DataType TableConstraint DEFAULT default_value,
	another_column DataType TableConstraint DEFAULT default_value_, 
	… 
);
```
If there already exists a table with the same name, the SQL implementation will usually throw an error, so to suppress the error and skip creating a table if one exists, you can use the `IF NOT EXISTS` clause:

#### Delete a Table
```sql
DROP TABLE student;
```
the database may throw an error if the specified table does not exist, and to suppress that error, you can use the `IF EXISTS` clause:
```sql 
DROP TABLE IF EXISTS mytable;
```
if you have another table that is dependent on columns in table you are removing (for example, with a `FOREIGN KEY` dependency) then you will have to either update all dependent tables first to remove the dependent rows or to remove those tables entirely.

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

#### INSERT ON DUPLICATE KEY UPDATE (Only on MySQL)
When you insert a new row into a table if the row causes a duplicate in `[UNIQUE](https://www.mysqltutorial.org/mysql-unique/)` index or `[PRIMARY KEY](https://www.mysqltutorial.org/mysql-primary-key/)` , MySQL will issue an error.

However, if you specify the `ON DUPLICATE KEY UPDATE` option in the `INSERT` statement, MySQL will [update](https://www.mysqltutorial.org/mysql-update-data.aspx) the existing row with the new values instead.


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
LIMIT 2 OFFSET 5; 
```
**OFFSET** specifies wheere to begin counting

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

<hr>

#### LIKE
To select all customers with a CustomerName starting with "a":
```sql
SELECT * FROM Customers  
WHERE CustomerName LIKE 'a%';
```
- % represents multiple characterse
- _ represents one character

#### COLUMN ALIAS
```sql
SELECT column_name AS alias_name
FROM table_name;
```

#### TABLE ALIAS
```sql
SELECT c.name, t.name  
FROM character AS c  
LEFT JOIN character_tv_show AS ct  
ON c.id = ct.character_id  
LEFT JOIN tv_show AS t  
ON ct.tv_show_id = t.id;
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

#### GROUP BY
```sql
SELECT COUNT(sex), sex FROM employee
GROUP BY sex;
```

- SUM and GROUP BY example:
![[Screen Shot 2021-01-24 at 3.33.46 PM.png]]
<hr>
- MIN, MAX
- HAVING = WHERE for aggregates (comes after GROUP BY)
```sql	
	SELECT Role, SUM(Years_employed) FROM employees
	GROUP BY Role
	HAVING Role = 'Engineer';
```

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

- self join - 
	- to get away with ambiguous table names, use alias (in this case, 'buddies')
	![[Screen Shot 2021-01-24 at 3.41.25 PM.png]]

<hr>

## Sub/Nested Query
```sql
SELECT * FROM CUSTOMERS
WHERE ID IN (SELECT ID
	FROM CUSTOMERS
	WHERE SALARY > 4500);
```
![[Screen Shot 2021-01-25 at 9.24.50 PM.png]]

## If
```sql
SELECT OrderID, Quantity, IF(Quantity>10, "MORE", "LESS")
FROM OrderDetails;
```
- return MORE f the condition is TRUE, or LESS if the condition is FALSE.
![[SQL IF statement.png]]

<hr>
- Khan Academy SQL practice: https://www.khanacademy.org/computing/computer-programming/sql/relational-queries-in-sql/pt/combining-multiple-joins

## CASE
```sql
SELECT *,  
CASE WHEN species = 'human' THEN 2 ELSE 4 END AS num_legs  
FROM friends_of_pickles;
```

![[Screen Shot 2021-01-26 at 1.14.34 PM.png]]

## SUBSTRING (SUBSTR)
`SUBSTR(name, 1, 5)` is the first 5 characters of the name.  
`SUBSTR(name, -4)` is the last 4 characters of the name.

`SELECT * FROM robots WHERE SUBSTR(name, -4) LIKE '20__';` is another way of returning all of the robots that have been released between 2000 and 2099.

## COALESCE 
`COALESCE` takes a list of columns, and returns the value of the first column that is not null.
If value of _gun_ is not null, that is the value returned. Otherwise, the value of _sword_ is returned. Then you would run:  
`SELECT name, COALESCE(gun, sword) AS weapon FROM fighters;`

<hr>

## Order of Execution of a Query
1. FROM annd JOINs
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. DISTINCT
7. ORDER BY
8. LIMIT / OFFSET

<hr>

SQL Exercise Resources
- https://www.sqlteaching.com/
- https://sqlbolt.com/lesson/select_queries_introduction
- 