###Overview
Visualize this [table](https://drawsql.app/teams/rodrigos-team-2/) on [drawsql.app](https://www.drawsql.app)

These .sql file are a list of commands that once the database is created, you can setup the tables, seed sample information, and delete the tables. This functionallity is similar to what you would see in an ORM (Object-Relational Mapping) Alter

##Install PostgreSQL:
```
sudo apt-get install postgresql
```

##Allow yourself to login to postgresql

Edit the file pg_hba.conf:
note: the version number may be different for you, mine is 14.
```
vi /etc/postgresql/14/main/pg_hba.conf
```

Modify the line:
```
# Database administrative login by Unix domain socket
local   all             postgres        peer
```
To be:

```
# Database administrative login by Unix domain socket
local   all             postgres        trust
```

Restart the service:
```
sudo service postgresql restart
```
Login to PostgreSQL:
```
psql -U postgres -d postgres
```

Create database 'results':
```
psql -U postgres -d postgres -c 'CREATE DATABASE results'
```

Create 'api' user with password:
```
psql -U postgres -d postgres -c "CREATE USER api WITH PASSWORD 'password';"
```

Allow user 'api' to have access to database 'results':
```
psql -U postgres -d postgres -c 'GRANT ALL PRIVILEGES ON DATABASE results TO api;'
```

Edit the file pg_hba.conf again to revert postgres user to 'peer' and add api user as 'md5':
note: the version number may be different for you, mine is 14.
```
vi /etc/postgresql/14/main/pg_hba.conf
```

Revert 'postgres' user to be 'peer':
```
# Database administrative login by Unix domain socket
local   all             postgres        peer
```

Add 'api' user as 'md5,' this will require a password:
```
# TYPE  DATABASE        USER            ADDRESS  
local   results         api             md5
```

Restart the service:
```
sudo service postgresql restart
```


##clone the project from github:

https version:
git clone https://github.com/RCornidez/postgresql_template.git

ssh version:
git clone git@github.com:RCornidez/postgresql_template.git

navigate within the folder and run the following commands:

create the database:
psql -U postgres -d postgres -c 'CREATE DATABASE results'

create the table:
psql -U postgres -d results -a -f ./setup_tables.sql

seed test data into table:
psql -U postgres -d results -a -f ./seed_tables.sql

delete table from database:
psql -U postgres -d results -a -f ./drop_tables.sql
