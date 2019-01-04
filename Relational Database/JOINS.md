# JOINS 

**Tl;dr**: JOINS make the relational models come to life by associating tables together.  

## Cross JOIN

* Simplest join 
* Returns all the rows from both the tables 
* No WHERE clause 
* Least useful 
* Inefficient 
* Creats Cartesian Product 

*Example Statement:* What are all the first name and email addresses I have ?

```SQL
SELECT p.first_name,e.email_address FROM person p,email_address e;
```

**The above SQL statement BAD practice.**

It's a bad practice beacause it has multiple table and does not have a WHERE clause. 

## Inner JOIN 

* Matches column value in the first table to the second table with the help of the primark key and the forgien key .
* Does not deal with NULL values. 

*Example Statement:* What are the contacts' email addresses ?

```SQL
SELECT p.first_name,p.last_name,e.email_address
FROM person p INNER JOIN email_address e ON 
p.person_id = e.email_address_person_id;
```

## Outer JOIN

* Works even when no match 

### Left Outer JOIN
* All the rows from the left side will be returned 
* NULL for non-matching right side table 

*Example Statement:* What are the contacts' email addresses, including those that do not have an email ?

```SQL
SELECT p.first_name,p.last_name,e.email_address
FROM person p LEFT OUTER JOIN email_address e 
ON p.person_id = e.email_address_person_id;
```

### Right Outer JOIN

* All the rows from the right side will be returned 
* NULL for non matching left side table

*Example Statement:* What are the contacts' email addresses, including those email that I don't have a person for ?

```SQL
SELECT p.first_name,p.last_name,e.email_address
FROM person p RIGHT OUTER JOIN email_address e 
ON p.person_id = e.email_address_person_id;
```

### Full Outer JOIN 

*Example Statement:* What are the contacts' email addresses, including those email that I don't have a person for and even those that have a person contact but not an email ?



```SQL
SELECT p.first_name,p.last_name,e.email_address
FROM person p FULL OUTER JOIN email_address e 
ON p.person_id = e.email_address_person_id;
```

### Self JOIN

* Join a table to itself
* No special syntax 
* Useful when table contains hierarchical data

