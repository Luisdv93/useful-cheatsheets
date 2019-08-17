# MySQL Cheatsheet

## Create / Delete Database

```sql
CREATE DATABASE db_name: To create a new db.

CREATE DATABASE db_name CHARACTER SET utf8: To create a new db with utf8 chars.

DROP DATABASE db_name: To completely delete a db.

ALTER DATABASE db_name CHARACTER SET utf8: To alter the chars set of a db.
```

## Browsing

```sql
SHOW DATABASES: Show all the created dbs.

USE db_name: Select this db to work with.

SELECT database(): Used to know which db you are using at the moment.

SHOW TABLES: Show all the tables created in the used db.

SHOW FIELDS FROM table / DESCRIBE table: Show all the fields of a table.

SHOW CREATE TABLE table: Show the commands used to populate the table.
```

## Select

```sql
SELECT * FROM table: Selects every field from the table.

SELECT * FROM table1, table2: Selects every field from all the tables specified.

SELECT first_name FROM table1 AS name: Selects a field assign a temporary alias to it.

SELECT field1, field2 FROM table1, table2: Select the specified field from the specified tables.

SELECT * FROM table WHERE condition: Selects only the records that match the condition.

SELECT * FROM table WHERE condition GROUPBY field: Selects the records that match the condition and group them by the given field. For example group by name.

SELECT * FROM table WHERE condition GROUPBY field HAVING condition2: Selects the records that match the conditions, group them by the given field and additionally only those that match the HAVING condition.

SELECT * FROM table WHERE condition ORDER BY field1: Selects the records that meet the condition and order them by the given field, useful for dealing with numbers or order by alphabetical order.

SELECT * FROM table WHERE condition ORDER BY field1, field2 DESC: Same as the above but specifying DESC will order the records in descedant order.

SELECT * FROM table WHERE condition LIMIT 10: Selects the records that meet the condition and limit the number of records shown.

SELECT DISTINCT field1 FROM table: Selects the matching records but only the ones that have an unique specified field.

DESCRIBE table1 / DESC table1 / SHOW COLUMNS FROM table1: To show and describe the columns of a table.

SHOW WARNINGS: Show the warnings from any perfomed operation before.
```

## Conditions

```sql
field1 = value1: Equal to.

field1 != value1: Not equal to.

field1 < <= >= > value1: Less than or equal to. Also less or equal and greater than or equal.

field1 LIKE '%value': Used for searching. % at the beginning means that anything can go before the given value.

field1 LIKE 'value%': Used for searching. % at the end means that anything can go after the given value.

field1 LIKE 'ca_': Used for searching. _ represents a single char. In this case it could either be cat or car.

field1 NOT LIKE 'value%': Used for searching, it will match everything that doesnt start with value.

field1 BETWEEN 5 AND 10: To select only the records among the range specified in between.

field1 % 2 != 0: Used to select the rows that are not odd.

field1 IS NULL: Used to check if a field is null.

field1 IS NOT NULL: Used to check if a field is not null.

field1 IS IN (value1, value2): Used to check if a field value is part of the given list.

field1 IS NOT IN (value1, value2): Used to check if a field value is not part of the given list.

condition1 AND condition2: Check if both conditions are true.

condition1 OR condition2: Check if one of the conditions is true.
```

## Create Table

```sql
CREATE TABLE table (field1 type1, field2 type2, ...): Creates a simple table with the given field and data types.

CREATE TABLE table (field1 type1, field2 type2, ..., INDEX (field)): Creates a table with a index used to speed the searching of that given field.

CREATE TABLE table (field1 type1, field2 type2, ..., PRIMARY KEY (field1) AUTO_INCREMENT): Creates a table and assigns a field to become a primary key of that table and and auto incremented.

CREATE TABLE table (field1 type1, field2 type2, ..., PRIMARY KEY (field1,
field2)): Creates a table and assigns multiple fields to become the primaries keys of that table.

CREATE TABLE table1 (fk_field1 type1, field2 type2, ...,
  FOREIGN KEY (fk_field1) REFERENCES table2 (t2_fieldA))
    [ON UPDATE|ON DELETE] [CASCADE|SET NULL]: Creates a table and assign a field to be a foreign key reference for another table, the second arguments are used to perfom actions after and update or delete action.

CREATE TABLE table1 (fk_field1 type1, fk_field2 type2, ...,
 FOREIGN KEY (fk_field1, fk_field2) REFERENCES table2 (t2_fieldA, t2_fieldB)): Same as above but the foreign key can reference two fields at the same time.

CREATE TABLE table IF NOT EXISTS (...): Creates a table conditionally to avoid trying to create a table that already exists.
```

## Delete Table

```sql
DROP TABLE table: Deletes the specified table.

DROP TABLE IF EXISTS table: Deletes the table conditionally, only if it exists.

DROP TABLE table1, table2: Drop multiple tables at the same time.
```

## Modify Table

```sql
ALTER TABLE table MODIFY field1 type1: Modify a specific field from a table.

ALTER TABLE table MODIFY field1 type1 NOT NULL: Modify a specific field from a table and make it not null.

ALTER TABLE table CHANGE old_name_field1 new_name_field1 type1: Modify a specific field name and type.

ALTER TABLE table CHANGE old_name_field1 new_name_field1 type1 NOT NULL: Modify a specific field name and type and make it not null.

ALTER TABLE table ALTER field1 SET DEFAULT: Modify a specific field and assign a default value.

ALTER TABLE table ALTER field1 DROP DEFAULT: Modify a specific field and remove the default value.

ALTER TABLE table ADD new_name_field1 type1: Add a new field to a table.

ALTER TABLE table ADD new_name_field1 type1 FIRST: Modify a column to be the first column.

ALTER TABLE table ADD new_name_field1 type1 AFTER another_field: Modify a column to move it after a given column.

ALTER TABLE table DROP field1: Modify a table to delete a field.

ALTER TABLE table ADD INDEX (field): Add a new index to a table.
```

## Update

```sql
UPDATE table1 SET field1=new_value1 WHERE condition: Update a record from a table where the condition is met.
```

## Delete

```sql
DELETE FROM table1 / TRUNCATE table1: Delete all records.

DELETE FROM table1 WHERE condition: Delete all records that meet the condition.

DELETE FROM table1, table2 FROM table1, table2 WHERE table1.id1 =
  table2.id2 AND condition: Deletes matching records from multiple tables at the same time.
```

## Insert

```sql
INSERT INTO table1 (field1, field2, ...) VALUES (value1, value2, ...): Insert the given values into the specified fields.
```

## Common Data Types

```
CHAR(num): A static length string, everything needs to be the same length.

VARCHAR(num): A variable length string that can go from 1 to 255 characters. If you exceed the set number it will truncate the text.

INT: An intenger up to 4294967295 and can be negative.

DECIMAL(num, num): A decimal number. The first number is the total number of digits and the second numbers is how many numbers come after the decimal point.

FLOAT/DOUBLE(num, num): Can store higher numbers at the cost of precision, doubles also needs double the memory to store it. Floats are precise up to 7 digits and doubles up to 15.
```

## Dates

```sql
DATE: Stores date with no time, example: 'YYYY-MM-DD'.

TIME: Stores time with no date, example: 'HH:MM:SS'.

DATETIME: Stores dates with time, example: 'YYYY-MM-DD HH:MM:SS'.

DATE_FORMAT(date): Probably the most powerful function, can format dates in all sorts of ways.

CURTIME(): Inserts the current time.

CURDATE(): Inserts the current date.

NOW(): Inserts the current datetime.

DATEDIFF(date1, date2): Returns the difference in days as numbers.

DATEADD(date, INTERVAL, unit): Adds dates together
```

## String Functions

```sql
SELECT CONCAT(column1, 'text', column2, 'more text'): Used to combine columns into a single column.

SELECT CONCAT_WS(' - ', column1, column2 ): Used to combine columns into a single column and use a separator between each one.

SELECT SUBSTRING('hello world', 1, 4): Used to get a portion of a string, indexes in mysql start at 1 so you would get 'hell'.

SELECT SUBSTRING('hello world', 4): Omit the second index and it will grab everything starting from that index. -index can be used to go in reverse.

SELECT REPLACE('Hello World', 'Hell', '&\$#@'): Replace a portion of a string with another one.

SELECT REVERSE('Hello World'): Reverses a string.

SELECT CHAR_LENGTH('Hello World'): Tells you the character count of the given string.

SELECT UPPER('Hello World'): Convert the given string into uppercase.

SELECT LOWER('Hello World'): Convert the given string into lowercase.
```

## Aggregate Functions

```sql
SELECT COUNT(field1): Provides the count of all the matching rows from the query

SELECT COUNT(field1) FROM table1 WHERE field1 LIKE '%The': Can be combined with other functions.

SELECT field1, COUNT(*) FROM table1 GROUP BY field1: Group rows by a certain column, useful for counting.

SELECT MIN(field1) FROM table1: Calculates the minimum value from a table.

SELECT * FROM table1 WHERE field1 = (SELECT MIN(field1) from table1) : Min needs a subquery to grab the related fields to make bigger queries. In this case the second query will execute first. This is way is slow. ORDER BY field1 ASC LIMIT 1 achieves the same but it is faster.

SELECT MAX(field1) FROM table1: Calculates the maximum value from a table.

SELECT * FROM table1 WHERE field1 = (SELECT MAX(field1) from table1) : Min needs a subquery to grab the related fields to make bigger queries. In this case the second query will execute first. This is way is slow. ORDER BY field1 DESC LIMIT 1 achieves the same but its faster.

SELECT SUM(field1) FROM table1: Calculates the sum of all records.

SELECT field1, SUM(field1) FROM table1 GROUP BY field1: To calculate the sum of a given group, for example the sum of total sales by year.

SELECT field1: Get the average number from the given column.

SELECT field1, AVG(field1) FROM table1 GROUP BY field1: To calculate the average of a given group, for example the average amount of sales for a given year.
```

## Joins

```sql
SELECT * FROM table1, table2: A cross join, pretty useless since it matches everything from tables together without a proper relation.

SELECT * FROM table1, table2 WHERE table1.id = table2.table1_id: A cross join or implicit join that matches the data from table1 to table22 where the join condition is met.

SELECT * FROM table1 JOIN table2 ON table1.id = table2.table1_id An explicit inner join, will match the rows where the FK of table2 matches the table1 id.

SELECT * FROM table1 LEFT JOIN table2 ON table1.id = table2.table1_id A left join will match all the records from the first table with the data that matches in the second one, the ones that dont match are left NULL.

SELECT IFNULL(SUM(amount), 0) FROM table1 LEFT JOIN table2 ON table1.id = table2.table1_id A left join will match all the records from the first table with the data that matches in the second one, the ifnull will check if the data is null and replace it with the 2nd argument.

SELECT * FROM table1 RIGHT JOIN table2 ON table1.id = table2.table1_id A right join will match all the records from the first table with the data that matches in the second one, the ones that dontt match are left NULL.´
```

## Backup Database to SQL File

```sql
mysqldump -u Username -p dbNameYouWant > databasename_backup.sql
```

## Restore from backup SQL File

```sql
mysql - u Username -p dbNameYouWant < databasename_backup.sql
```
