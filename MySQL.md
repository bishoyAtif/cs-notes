## General

- Why MySQL ??
 - Free.
 - Used by many popular web apps.
 - Powerful and fast.
 - highly scalable.
- What is the difference between SQL, MySQL, MySQLi, PDO ?
 - SQL >> Structured Query Language .. The language to treat with DBs.
 - MySQL >> DB Engine .. A softwere to use SQL to treat with DBs .. Like PGSQL and SQLite.
 - MySQLi >> MySQL-Improved .. Extention in PHP to connect to the DB using MySQL.
 - PDO >> PHP Data Object .. Extention in PHP to connect to the DB using many DB engines Like MySQL, 
    PGSQL and SQLite.
- Creating Data Model 
  - Entity class >> Employee .... Entity instance >> first_name, last_name, salary, ID, Skills, Address.
  - Simple component >> has only one value 'Individual column'. Example: first_name.
  Composite component >> has multiple values 'column that can be related to other columns'. 
        Example: Address 'street, zip_code, city'.
  - Shapes of each attribute: 
   Employee >> Rectangle.
   first_name, last_name >> only circle 'Normal Column'.
   ID >> circle with underlined name 'Primary key .. Distinct value'.
   Skilles >> double circle 'Multi valued Attribute' 
- Logical operators:
 - Cond. AND Cond.
 - Cond. OR Cond.
 - Cond. XOR Cond.
 - NOT Cond.
- GRANT PRIVILAGES ON database_name[*].table_name[*] TO 'user_name'@'domain[localhost]' IDENTIFIED BY 'pass'
- START TRANSICTIONS; //starts a thing like session in the db
 - Your queries.
 COMMIT; // Confirms all the changes in the db.
 ROLLBACK; //Discards all the changes if one of them doesn't excecuted successfully.

## Data types

### CHAR

- Character data can be stored as either fixed-length or variable-length strings; the difference is that fixed-length strings are right-padded with spaces and always consume the same number of bytes, and variable-length strings are not right-padded with spaces and don’t always consume the same number of bytes.
- ```CHAR(<max-length>)``` defines a fixed-length character.
- ```VARCHAR(<max-length>)``` defines a variable-length character.
- ```TEXT(<max-length>)``` >> Like ```VARCHAR``` But ```TEXT``` types are much larger than it. By default, ```TEXT``` is indexed for sorting or grouping with only first 1024 characters but VARCHAR is indexed totally.

### Numeric

- MySQL has many numeric types with different sizes like ```SmallInt```, ```MediumInt``` or ```BigInt```.
- ```INT(<optiobal-minimum-width>) <UNSIGNED>```. Minimum width represents the minimum width of the data when the data is retrived.
  - Example: ```CREATE TABLE students(id INT(4) UNSIGNED);```
- It's usually used with ZEROFILL qualifier.
- ```FLOAT(total-width, float-width)``` represents float columns. ```DOUBLE``` can be used instead of ```FLOAT``` for large numbers.
  - Example: ```FLOAT(5,2) == 123.12```.
  - a column defined as float(4,2) will store a total of four digits, two to the left of the decimal and two to the right of the decimal. Therefore, such a column would handle the numbers 27.44 and 8.19 just fine, but the number 17.8675 would be rounded to 17.87, and attempting to store the number 178.375 in your float(4,2) column would generate an error.

### Date

- ```DATETIME``` and ```TIMESTAMP``` both stores timestamps but ```DATETIME``` has a much more wide range than ```TIMESTAMP```
  - ```TIMESTAMP``` stores from 1970 to 2037 only.
  - ```TIMESTAMP``` is also useful because if you don't specify a date it will automatically store the current time.
- ```YEAR``` type can store from 1901 to 2155.

### Miscellanious

- ```ENUM(<value1, value2>)``` stores multiple options to choose only one of them.
- SET >> stores multiple records to choose one or more from them

## CONSTRAINTS

- It's rules for columns within a table.
- ```NOT NULL``` can't be empty field.
- ```CHECK(<condition>)``` will check a condition before inserting into this column. ***MySQL Parses CHECK constraints but it doesn't enforce it.***
  - ```field_name [>, <, =] some_value``` comparison between the value inserted and predefined ```some_value```.
  - ```field_name in (value1, value2 ...)```
- ```DEFAULT <value>``` It is used as a default value if no value is inserted in this field.
- ```AUTO_INCREMENT``` is used with the primary keys to increment it automatically.
- ```USIGNED``` is used with ```INT``` types and will not allow negative numbers.
- ```UNIQUE``` will not allow for duplicate values in the column specified for it. It will raise an error when trying to insert duplicate values.

### Indecies

## Queries

### Working with databases

- SHOW DATABASES; >> returns all the databases in your server.
- CREATE DATABASE [ IF NOT EXISTS ] 'db_name'; >> creating the databse.
- DROP DATABASE [IF EXISTS] 'db_name'; >> deleting the database.
- USE 'db_name'; >> selecting the database from the command line to be used.

### Manipulating Tables Structure

- ```SHOW TABLES``` shows all the tables in your database.
- ```DESCRIBE <table_name>``` shows the full structure of a specific table.
- To create a table
  ```sql
    /* Syntax */
    CREATE TABLE <table_name> (
      field_1 VARCHAR CONSTRAINT,
      field_2 INT NOT NULL UNSIGNED,
      CONSTRAINT <constraintName> UNSIGNED
    )

    /* For example */
    CREATE TABLE person (
      person_id SMALLINT UNSIGNED,
      fname VARCHAR(20),
      lname VARCHAR(20),
      gender  ENUM('M','F'),
      birth_date DATE,
      street VARCHAR(30),
      city VARCHAR(20),
      state VARCHAR(20),
      country VARCHAR(20),
      postal_code VARCHAR(20),
      CONSTRAINT pk_person PRIMARY KEY (person_id)
    );
  ```
- ```DROP TABLE <table_name>``` to delete a table.
- ```ALTER TABLE table_name RENAME new_table_name``` will rename a table.
- ```ALTER TABLE table_name MODIFY column_name new_data_type``` will alter the data type of a column.
- ALTER TABLE table_name ADD column_name [CONSTRAINTS]; >> adding new column to a table.
 -- ALTER TABLE users ADD age INT ( FIRST | AFTER name )
- ALTER TABLE table_name CHANGE old_column_name new_column_name data_type 'Must be specified'.
- ALTER TABLE table_name DROP column_name.
- ALTER TABLE table_name ENGINE=MyISAM 'For example'


### Manipulating Data

- ```INSERT INTO table_name (field_1, field_2, ...) VALUES(value_1, value_2 ...)``` is used to insert data into a table.

### Querying Data

- ```SELECT column_1, column_2 FROM table_name```;
  - ```*``` matches all columns of a table.
-  ```WHERE [condition]``` is used to filter rows of a table.
  - Example: ```SELECT id, name FROM users WHERE age > 18```
- ```ORDER BY``` clause is used to order the rows returned asccendingly or descindingly according to a specific column. ```ASC```, the default option or ```DESC``` is used when ordering. Multi columns can be used with the same ```ORDER BY``` clause and the result will be ordered by first column, then if the first column for is equal in some rows, sql will order those columns by the second column.
  ```sql
    SELECT id, name FROM users WHERE age > 18 ORDER BY name DESC
  ``` 
- SOURCE /path/to/source/file; >> runs SQL commands from an external file. 
- \c >> Canceling a line of input.
- LIKE 'b%' >> a word begins with b
 LIKE '%b%' >> a word contains b
 - '%' Wild card for any number of chars.
 - '_' Wild card for one char.
- WHERE field_name IS NULL; >> checks for the null values in the table;
- GROUP BY >> Used for retrieving information about a group of data.
- HAVING >> Used with GROUP BY to implement a condition on a group.
- DELET FROM table_name WHERE [Condition];
- UPDATE table_name SET field_1 = value_1, ... WHERE CONDITION;1
- AS >> used to rename the column on a single query to ease the retrive of the data.
- LIMIT - >> used to retrive a specific amount - of columns. 
 Example: "SELECT * FROM books LIMIT 5" >> gets the first 5 rows from the table books
- LIMIT -, ->> Example: "SELECT author,title FROM classics LIMIT 3,1"
    LIMIT 1,3 means return three rows starting from the second row.
- MATCH .. AGAINST >> can be used on columns that have been given a FULLTEXT index
 - Example: "SELECT author,title FROM classics WHERE MATCH(author,title) AGAINST('and')" asks for any of 
  these columns that contain the word and to be returned. Because and is a stopword, MySQL will ignore it 
  and the query will always produce an empty set—no matter what is stored in the columns.
 - Example: SELECT author,title FROM classics WHERE MATCH(author,title) AGAINST('curiosity shop');
  asks for any rows that contain both of the words curiosity and shop anywhere in them, in any order, to be 
  returned.
- MATCH .. AGAINST "Boolean mode":
  - any of the words can return the row it contains 
  - you can use + or - sign to include or reject a word from being in the row.
  - you can use double quotes around the text to match the exact text not a combination of its words.
 Example: "SELECT author,title FROM classics
    WHERE MATCH(author,title)
    AGAINST('+charles -species' IN BOOLEAN MODE)"
   - asks for all rows containing the word charles and not the word species to be returned.
 Example: "SELECT author,title FROM classics
    WHERE MATCH(author,title)
    AGAINST('"origin of"' IN BOOLEAN MODE);
   - uses double quotes to request that all rows containing the exact phrase origin of be returned.
- WHERE field_name BETWEEN -1 and -2 >> select within a range.
- WHERE field_name IN (-1, -2, -3) >> selects from a specific values.
 Example : "SELCT * FROM books WHERE id IN (5,6,7)"; 
- DISTINCT field_name >> takes the first row of the rows the have repeated field_name
 Example : "SELECT DISTINCT name, age FROM students";
- NATURAL JOIN >> automatically joins columns that have the same name. 
- JOIN :
  - INNER JOIN >> selects from two tables with a matual field on them
  - Example: "SELECT book.name, category.name 
     FROM books
     INNER JOIN categories
     ON book.category = categories.id
     "
  - LEFT JOIN >> selects from two tables with the matual field and all the records from the left table even if not in the right table.
  - RIGHT JOIN >> The opposite of the LEFT JOIN.
- UNION = FULL JOIN:
 - SELECT if from books UNION select id from categories;
  - It will join the id column with the data of the two tables.
- Dynamic tables:
 - CREATE VIEW view_name AS SELECT name FROM books INNER JOIN categories ON ....
 - the view dynamically changes its data according to the tables that consists of
- Using newsted queries:
 Example: "INSERT INTO bookname SELECT name FROM books";
- Using Regexp : SELECT * FROM users WHERE name REGEXP 'Regex';
- Using mysqldump >> used to backup all the db into a file to be restored later
 mysqldump -u user_name -p 'Database' > file_name.sql
 - The first section of the command will print the all the commands to restore the DB so we must redirect it using ">" 
  to a file to be used later.
- To restore a database from a file .. just use "mysql -r user -p password [ -D Database ] < file_name.sql"
 we use "-D Database" when restoring a specific table in the DB.

## Normalization

- First Normal Form:
  - Each column has a single value.
  - No repeatition for the values of the same column.
  - It should be a primary key to identify each row.
- Seconde Normal Form:
  - No repeation for the values in multiple column.

## Indexes

- Adding index to a row in an existing table >> ALTER TABLE books ADD INDEX(author(20))
  - Adding index to the first 20 chars of the column authors.
  - If MySQL finds two indexes with the same contents, it will have to waste time going to the table itself and checking the column that was indexed to find out which rows really matched.
- FULLTEXT Index: Used only with MyISAM storage engine
  - It's recommended to load your data into a table that has no FULLTEXT index and then create the index 
  than to load data into a table that has an existing FULLTEXT index.
  - Used to search in large texts .. particular with MATCH .. AGAINST
- ALTER TABLE <table-name> DROP INDEX index_name ON table_name; >> Dropping an index.
- ```CONSTRAINT relation_name PRIMARY KEY (column_name)``` can be used to define a primary key, a unique indentifier for each row.
- ```CONSTRAINT relation_name FOREIGN KEY (column_name) REFERENCES foreign_table_name(foreign_column_name)``` is used to make a foreign key constraint, a key that represents a primary key or at less a unique column for a table added in another table to represents that row from the first table.
  - You can use ```ON DELETE``` and ```ON UPDATE``` with the foreign key to make action on the rows that have foreign keys when their primary keys are changed or deleted.
  - ```ON DELETE CASCADE``` will delete all the child rows if the primary row is deleted.
  - ```ON DELETE SET NULL``` will set the related foreign key to null in all the child rows if the primary row is deleted.
    ```sql
      CONSTRAINT relation_name FOREIGN KEY column_name
      REFERENCES foreign_table_name(foreign_column_name) 
      ON DELETE CASCADE
      ON UPDATE CASCADE
    ```

## DateTime

- ```NOW()``` in a built-in function that returns the current datetime and can be used in selection comparison between timestamps fields.

## Row Functions

- UPPER(field_name), LOWER(field_name) >> makes the entire row lower or upper case.
 Example : "SELECT id, UPPER(name) from categories";
 -- Used when searching for a string in database to make sure that the string in the database is collected 
  without worring about the text I have entered is lower or upper case.
- LENGTH(field_name) >> gets the length of each field in a cloumn.
 Example : "SELECT name, LENGTH(name) from categories";
- INSTR(field_name, "String") >> searches in the field for a specific string and returns its first index 
 "Indexed from 1 not 0" , returns 0 if not exists.
 Example: "SELECT name, INSTR(name, 'a') from books" >> returns the first index of the char 'a' in each book
- SUBSTR(field_name, beginning, length) >> returns a string from the beginning index and with a specific length
 Example: "SELECT name, SUBSTR(name, 1, 3) from categories";
- CONCAT(field_name, "String", ["Another string", ... ]) >> returns a string from the concatanation of each 
 field and "String";
 Example: "SELECT name, CONCAT(name, 'is good')";
- ROUND(float, numbers after decimal point) >> (1.522, 1) : 1.5, (1.556, 2) : 1.56
- TRUNCATE(float, numbers after decimal point -) >> cuts the floating number with only - numbers after the 
 decimal point
 Example : TRUNCATE(1.5556,2) : 1.55
- MOD(field, -) >> Returns the division of field % -
- YEAR(timestamp) //Getting the year.
- MONTH(timestamp) //Getting the month num.
- MONTHNAME(timestamp) // Getting the month name.

## Column Functions

- AVG(field_name) >> Get the average of the numbers in the column.
- COUNT(field_name) >> Get the number of the rows in the column.
- MIN(field_name), MAX(field_name) >> Get the min and the max numbers of the values in the rows in a column.
- SUM(field_name) >> Get the sum of all the values in a row.