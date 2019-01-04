# Basic SQL commands 

## SELECT 

* Retrives one or more rows from one or more tables , eg:
```SQL
SELECT first_name, last_name FROM contacts;
```
* After every  column comes a comma , except the last column.

* Using '*' in the select stament is considered a bad practice.

* Qualifying Column name with Table name is a good practice, eg:

```SQL
SELECT person.first_name,person.last_name FROM person ;
```
* Dot in the SQL statement represents the realtionship as column is a child of table person. 

* Qualifying can be done easily by *aliasing* the table name, eg:

```SQL
SELECT p.first_name,p.last_name FROM person p; 
```
* Aliasing just helps in increasing the readibilty of the SQL statement. 



**TIP:** *The keywords are written in uppercase and the indentifires are written in lower case in the SQL statement.*

## INSERT 

* Add one or more rows into a table.
* Works only with a single table,eg:

```SQL
INSERT INTO contacts (first_name, last_name)VALUES('node', 'Onion');
```

## UPDATE

* Modifies one or more rows in a table,eg:

```SQL
UPDATE contacts SET last_name='mat' WHERE id = 1 ;
```

## DELETE 

* Remove one or more rows from one table,eg:

```SQL
DELETE FROM contacts WHERE id = 2;
```
