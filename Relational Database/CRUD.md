# CRUD

|INSERT i.e CREATE | SELECT i.e READ|
| ------------- |:------------------:|
| **UPDATE** | **DELETE** |


## INSERT 

* To create an entry in a table 
* Only one table is allowed 
* It requires list of columns and values.

*Example:*
```SQL
INSERT INTO person (person_id,first_name,last_name,contact_number)
VALUES(121,'Mad','Max',9812313412) 
```

## Bulk INSERT 

* Insert multiple rows with one statement either with multiple values list or SELECT statement with following table name. 

*Example:*
```SQL
INSERT INTO person p
SELECT * FROM old_person op 
WHERE op.person_id > 300 ;
```
## UPDATE 

* Modifies column(s) in a single table 
* WHERE clause dictates with rows get updated 
* SET keyword follows table name , defines what are the columns that we want to update and what are those values. 

*Example:*
```SQL
UPDATE email_address e SET e.email_address = 'max@email.com'
WHERE e.email_address_id = 5;
```

## DELETE 

* Deletes one or more rows in a table.
* It's **PERMANENT !**
*
*Example:*
```sql
DELETE FROM person p 
WHERE p.id = 5;
 ```
 