# Getting stated with Postgresql

#### Managing the service 

```BASH 
 sudo systemctl enable postgresql.service
 sudo systemctl start postgresql.service
 sudo systemctl status postgresql.service
 sudo systemctl stop postgresql.service
 
```
#### Upgrade the packages 
```BASH
pacman -S postgresql postgresql-libs postgresql-old-upgrade
```

#### Running Postgres
```BASH 
sudo -u postgres -i
psql 
```

#### Creating Operations 
```BASH
[postgres] createdb <dbname>
[postgres] createuser --interactive
```
#### PSQL 

* For printing out lists 
```SQL
postgres=#\list
```

* To list all users
```SQL
postgres=#\du
```
* To set password for the user 
```SQL
postgres=#\password no_one 
```
* To remove user or database 
```SQL
postgres=#drop database <database_name>
postgres=#drop user <user_name>
```

* Login right 
```SQL
ALTER ROLE <username> WITH LOGIN;
```

* Reset password 
```SQL
ALTER USER user_name WITH PASSWORD 'new_password';
```
