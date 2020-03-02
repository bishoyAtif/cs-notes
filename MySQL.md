                                      -----------------------------
                                      <<<<<<<    General    >>>>>>>
                                      -----------------------------

- Why MySQL ??
    # Free.
    # Used by many popular web apps.
    # Powerful and fast.
    # highly scalable.

- What is the difference between SQL, MySQL, MySQLi, PDO ?
    # SQL    >> Structured Query Language .. The language to treat with DBs.
    # MySQL  >> DB Engine .. A softwere to use SQL to treat with DBs .. Like PGSQL and SQLite.
    # MySQLi >> MySQL-Improved .. Extention in PHP to connect to the DB using MySQL.
    # PDO    >> PHP Data Object .. Extention in PHP to connect to the DB using many DB engines Like MySQL, 
                PGSQL and SQLite.

- Creating Data Model 
    
    # Entity class >> Employee .... Entity instance >> first_name, last_name, salary, ID, Skills, Address.
    
    # Simple component >> has only one value 'Individual column'. Example: first_name.
      Composite component >> has multiple values 'column that can be related to other columns'. 
                             Example: Address 'street, zip_code, city'.

    # Shapes of each attribute: 
        Employee >> Rectangle.
        first_name, last_name >> only circle 'Normal Column'.
        ID >> circle with underlined name 'Primary key .. Distinct value'.
        Skilles >> double circle 'Multi valued Attribute' 

- Logical operators:
  # Cond. AND Cond.
  # Cond. OR Cond.
  # Cond. XOR Cond.
  # NOT Cond.

- GRANT PRIVILAGES ON database_name[*].table_name[*] TO 'user_name'@'domain[localhost]' IDENTIFIED BY 'pass'

- START TRANSICTIONS; //starts a thing like session in the db
  # Your queries.
  COMMIT; // Confirms all the changes in the db.
  ROLLBACK; //Discards all the changes if one of them doesn't excecuted successfully.
                       
                                        <<<<<<<    Data types    >>>>>>>

- CHAR(#) >> String with max length #.

- VARCHAR(#) >> String with variable length with max #.

- TEXT(#) >> Like VARCHAR But TEXT can't be assigned to NULL a
                              TEXT can be indexed with only first n characters but VARCHAR is indexed totally

- INT[#] [UNSIGNED] >> # represents the minimum width of the data when the data is retrived.
                       # It's usually used with ZEROFILL qualifier.
                       # Example: CREATE TABLE students(id INT(4) ZEROFILL);  

- DECIMAL[total_width, float_width] >> # Example: DECIMAL(5,2) == ###.## 

- DATETIME and TIMESTAMP both stores timestamps but DATETIME has a much more wide range than TIMESTAMP 
  # TIMESTAMP stores from 1970 to 2037 only.
  # TIMESTAMP is also useful because if you don't specify a date it will automatically store the current time.

- YEAR >> can store from 1901 to 2155;

- SET  >> stores multiple records to choose one or more from them
  ENUM >> stores multiple records to choose only one of them.
=============================================================================================================
                                        ----------------------------
                                        <<<<<<<    Syntax    >>>>>>>
                                        ----------------------------

- SOURCE /path/to/source/file; >> runs SQL commands from an external file. 

- \c >> Canceling a line of input.

- SHOW DATABASES; >> returns all the databases in your server.

- CREATE DATABASE [ IF NOT EXISTS ] 'db_name'; >> creating the databse.

- DROP   DATABASE [IF EXISTS] 'db_name'; >> deleting the database.

- USE 'db_name'; >> selecting the database from the command line to be used.

- SHOW TABLES; >> returns all the tables in your database.

- DESCRIBE 'table_name';

- CREATE TABLE 'table_name'(field_1 VARCHAR CONSTRAINT, field_2 INT ...); >> creates a table.

- DROP TABLE table_name;

- CONSTRAINTS : It's rules for the database.
    # NOT NULL >> can't be empty field.
    # CHECK(field_name [>, <, =] some_value)
    # DEFAULT 'value' >> It is used if no value is used for this field.
    # AUTO_INCREMENT >> used with primary keys to increment it automatically.
    # USIGNED >> unsigned int.
    # UNIQUE >> no duplecating values.
    
- INSERT INTO table_name (field_1, field_2, ...) VALUES(value_1, value_2 ...);

- SELECT * | column_1, column_2 FROM table_name WHERE [condition];

- LIKE 'b%' >> a word begins with b
  LIKE '%b%' >> a word contains  b
  # '%' Wild card for any number of chars.
  # '_' Wild card for one char.

- WHERE field_name IS NULL; >> checks for the null values in the table;

- ORDER BY field_name [DESC | ASC] >> orders the result asccendingly or descindingly.
  ORDER BY field_name [DESC | ASC], second_field_name [DESC | ASC]

- GROUP BY >> Used for retrieving information about a group of data.

- HAVING >> Used with GROUP BY to implement a condition on a group.

- DELET FROM table_name WHERE [Condition];

- UPDATE table_name SET field_1 = value_1, ...  WHERE CONDITION;1

- Primary and forign keys
    # CONSTRAINT relation_name PRIMARY KEY (column_name)
    # CONSTRAINT relation_name FOREIGN KEY (column_name) REFERENCES foreign_table_name(foreign_column_name)

- Using CASCADE to update all related records automatically
  Example: CONSTRAINT relation_name FOREIGN KEY (column_name) 
           REFERENCES foreign_table_nameforeign_column_name)  
           ON DELETE CASCADE
           ON UPDATE CASCADE

- AS >> used to rename the column on a single query to ease the retrive of the data.

- LIMIT # >> used to retrive a specific amount # of columns.  
  Example: "SELECT * FROM books LIMIT 5" >> gets the first 5 rows from the table books

- LIMIT #, #>> Example: "SELECT author,title FROM classics LIMIT 3,1"
               LIMIT 1,3 means return three rows starting from the second row.

- MATCH .. AGAINST >> can be used on columns that have been given a FULLTEXT index
                      
  # Example: "SELECT author,title FROM classics WHERE MATCH(author,title) AGAINST('and')" asks for any of 
    these columns that contain the word and to be returned. Because and is a stopword, MySQL will ignore it 
    and the query will always produce an empty set—no matter what is stored in the columns.
  
  # Example: SELECT author,title FROM classics WHERE MATCH(author,title) AGAINST('curiosity shop');
    asks for any rows that contain both of the words curiosity and shop anywhere in them, in any order, to be 
    returned.

- MATCH .. AGAINST "Boolean mode":
    # any of the words can return the row it contains 
    # you can use + or - sign to include or reject a word from being in the row.
    # you can use double quotes around the text to match the exact text not a combination of its words.

  Example: "SELECT author,title FROM classics
            WHERE MATCH(author,title)
            AGAINST('+charles -species' IN BOOLEAN MODE)"
          # asks for all rows containing the word charles and not the word species to be returned.

  Example: "SELECT author,title FROM classics
            WHERE MATCH(author,title)
            AGAINST('"origin of"' IN BOOLEAN MODE);
          # uses double quotes to request that all rows containing the exact phrase origin of be returned.

- ALTER TABLE table_name RENAME new_table_name >> renaming a table; 
- ALTER TABLE table_name MODIFY column_name new_data_type >> altering the data_type of a column.
- ALTER TABLE table_name ADD column_name [CONSTRAINTS]; >> adding new column to a table.
  ## ALTER TABLE users ADD age INT ( FIRST | AFTER name )
- ALTER TABLE table_name CHANGE old_column_name new_column_name data_type 'Must be specified'.
- ALTER TABLE table_name DROP column_name.
- ALTER TABLE table_name ENGINE=MyISAM 'For example'
- WHERE field_name BETWEEN #1 and #2 >> select within a range.
- WHERE field_name IN (#1, #2, #3) >> selects from a specific values.
  Example : "SELCT * FROM books WHERE id IN (5,6,7)"; 
- DISTINCT field_name >> takes the first row of the rows the have repeated field_name
  Example : "SELECT DISTINCT name, age FROM students";
  
- NATURAL JOIN >> automatically joins columns that have the same name. 

- JOIN :
    # INNER JOIN >> selects from two tables with a matual field on them
      # Example: "SELECT book.name, category.name 
                  FROM books
                  INNER JOIN categories
                  ON book.category = categories.id
                  "
    # LEFT JOIN  >> selects from two tables with the matual field and all the records from the left table even 
                    if not in the right table.
    # RIGHT JOIN >> The opposite of the LEFT JOIN.
- UNION = FULL JOIN:
  # SELECT if from books UNION select id from categories;
    # It will join the id column with the data of the two tables.
- Dynamic tables:
  # CREATE VIEW view_name AS SELECT name FROM books INNER JOIN categories ON ....
  # the view dynamically changes its data according to the tables that consists of
- Using newsted queries:
  Example: "INSERT INTO bookname SELECT name FROM books";
- Using Regexp : SELECT * FROM users WHERE name REGEXP 'Regex';
- Using mysqldump >> used to backup all the db into a file to be restored later
  mysqldump -u user_name -p 'Database' > file_name.sql
  # The first section of the command will print the all the commands to restore the DB so we must redirect it using ">" 
    to a file to be used later.
- To restore a database from a file .. just use "mysql -r user -p password [ -D Database ] < file_name.sql"
  we use "-D Database" when restoring a specific table in the DB.

                                        <<<<<<<    Normalization   >>>>>>>
- First Normal Form:
    # Each column has a single value.
    # No repeatition for the values of the same column.
    # It should be a primary key to identify each row.

- Seconde Normal Form:
    # No repeation for the values in multiple column.

=============================================================================================================
                                        ----------------------------
                                        <<<<<<<    Indexes   >>>>>>>
                                        ----------------------------
- Adding index to a row in an existing table >> ALTER TABLE books ADD INDEX(author(20))
    # Adding index to the first 20 chars of the column authors.
    # If MySQL finds two indexes with the same contents, it will have to waste time going to the table itself 
      and checking the column that was indexed to find out which rows really matched.

- FULLTEXT Index: Used only with MyISAM storage engine
    # It's recommended to load your data into a table that has no FULLTEXT index and then create the index 
      than to load data into a table that has an existing FULLTEXT index.
    # Used to search in large texts .. particular with MATCH .. AGAINST
- CREATE INDEX index_name ON table_name(field_name); >> creating an index.
- DROP INDEX index_name ON table_name; >> Dropping an index.
=============================================================================================================
                                        ----------------------------------
                                        <<<<<<<    Row Functions   >>>>>>>
                                        ----------------------------------
- UPPER(field_name), LOWER(field_name) >> makes the entire row lower or upper case.
  Example : "SELECT id, UPPER(name) from categories";
  ## Used when searching for a string in database to make sure that the string in the database is collected 
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

- TRUNCATE(float, numbers after decimal point #) >> cuts the floating number with only # numbers after the 
  decimal point
  Example : TRUNCATE(1.5556,2) : 1.55

- MOD(field, #) >> Returns the division of field % #
- YEAR(timestamp) //Getting the year.
- MONTH(timestamp) //Getting the month num.
- MONTHNAME(timestamp) // Getting the month name.
                                        -------------------------------------
                                        <<<<<<<    Column Functions   >>>>>>>
                                        -------------------------------------
- AVG(field_name) >> Get the average of the numbers in the column.
- COUNT(field_name) >> Get the number of the rows in the column.
- MIN(field_name), MAX(field_name) >> Get the min and the max numbers of the values in the rows in a column.
- SUM(field_name) >> Get the sum of all the values in a row.