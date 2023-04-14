How to run:
	visualize this table on drawsql.app
		link: https://drawsql.app/teams/rodrigos-team-2/diagrams/meetup

	install PostgreSQL:
		sudo apt-get install postgresql
	
	clone the project from github:

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
