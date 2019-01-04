# ODER BY and GROUP BY


## ODER BY
* Allows sorting of result 
* Specify with one or more columns seprated by commas
* Default odering is asending(ASC) or DESC

*Example Statement:* People in my contact list orderd by the last name ?

```SQL
SELECT p.last_name,p.first_name FROM person p 
ORDER BY p.last_name 
```

## SET Function 

* Computes new values from colum values 
* Use in place of SELECT clause
* Passes column name to function


| Keyword        | Result           | 
| ------------- |:-------------:|
| COUNT   | Count the column specified (includes NULL if used ) | 
| MAX   | Max value of the column(NULL not included) |  
| MIN | Min value of the column (NULL not included) | 
| SUM | Sum of all the values of the column (NULL not included) | 
|AVG|Average of all the values of the column(NULL not included) |

*Example Statement:*Total number of contacts in the contact list ?

```SQL
SELECT SUM (p.contacted_number) FROM person p;
```

## GROUP BY 

* Allows multiple coulmns with a set function
* Breaks result set into sub sets and runs set function for those sub-sets.
* Appears after the FROM and/or WHERE clause.

*Example Statement:* What is the count of every unique first name among my contacts ?

```SQL
SELECT COUNT (p.first_name),p.first_name 
FROM person p 
GROUP BY p.first_name;
```

## HAVING 

* It works as a where clause against the GROUP BY clause

*Example Statement:* What is the count of every unique first name among my contacts that appear at least 5 times ?

```SQL
SELECT COUNT (DISTINCT p.first_name),
p.first_name 
FROM person p 
GROUP BY p.first_name;
HAVING COUNT(DISTINCT P.first_name) >= 5;
```
This would give only the name of the person that are unique in the list and appear 5 or 5+ times.  