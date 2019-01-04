# Filtering Result with WHERE 

```SQL
SELECT p.last_name FROM person p WHERE p.last_name ='JHON';
```

## Boolean Keywords 

### AND

* Combines two expression , if both are true row is includes. 
* If either is false, row is excluded. 

```SQL
SELECT p.last_name FROM person p 
WHERE p.last_name ='JHON'AND p.birthday = '12/01/1997';
```

### OR

* Combines two expression , if either are true row is includes. 
* If both are false, row is excluded. 

```SQL
SELECT p.last_name FROM person p 
WHERE p.last_name ='JHON'OR p.last_name = 'doe';
```
### BETWEEN 

* Acts on one column and two values, TRUE if the column value is between the two values 
* Inclusive - includes two values (like >= & <=)


```SQL
SELECT p.last_name FROM person p WHERE p.last_name ='JHON' 
WHERE p.contacted BETWEEN 1 AND 20;
```

### LIKE 

* Read more about it !

*Example Statement:* Find the people in contact list where first name begins with letter J ?


```SQL
SELECT p.first_name,p.last_name FROM person p 
WHERE p.first_name LIKE 'J%';
```
* '%J%' would look for characters in the name that has J in it anwhere in the middle. 

### IN 

* This helps in simplfying the SQL statement where a multiple of OR clause could be used.
* Instead of that a single IN could do the job. 

*Example Statement:* Who all are people in my list who has name 'Jhon' or 'Bob' ?

```SQL
SELECT p.first_name,p.last_name FROM person p 
WHERE P.first_name  IN ('Jhon','Bob');
```
* This statement could have been a bit messy if names would be Jhon, Bob , Raven , Max as it would use multiple OR statements .
* But in the IN expression you could just add two more names. 

### IS 

* It only works for the value that might be null.
* IS is always accompanied by a NULL 

*Example Statement:* Who all are people in my contact list that do not have a last name ?

```SQL
SELECT p.first_name,p.last_name FROM person p 
WHERE p.last_name IS NULL;
```

### IS NOT 

* It only works for the value that is not null.
* IS NOT is always accompanied by a NULL 

*Example Statement:* Who all are people in my contact list that have a last name ?


```SQL
SELECT p.first_name,p.last_name FROM person p 
WHERE p.last_name IS NOT NULL;
```

*TIP:* Looking at the IS and IS NOT we realize that DB like to handel NULL values in an detailed manner. 