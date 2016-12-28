## mysql

###### Access mysql:
  `$ mysql -u root -p`

###### Create a database:
  `create database dbname;`

###### Show existing databases:
  `show databases;`

###### Show existing tables in a database:
  `use mydb;`
  `show tables;`

###### Display users:
  `SELECT User,Host FROM mysql.user;`

###### Create a user:
  `CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';`
  `CREATE USER 'myuser'@'10.10.%.%' IDENTIFIED BY 'mypassword'; (If needing to connect via unix socket)`

###### Create a user and a grant at the same time:
  `grant all privileges on db_name.* to user@localhost identified by 'secret_password';`

###### Change user's password:
  `SET PASSWORD FOR 'myuser'@'localhost' = PASSWORD('newpass');`
  `SET PASSWORD FOR 'myuser'@'10.10.%.%' = PASSWORD('newpass'); (If needing to connect via unix socket)`
  `FLUSH PRIVILEGES;`

###### Delete a user:
  `drop user 'dashboard'@'%.nsbloomfield.com';`

###### Delete a user (another method):
  `DELETE FROM mysql.user WHERE User='name';`

###### Show privileges for a user:
  `show grants for 'dashboard'@'10.10.%.%';`

###### Grant privileges to a user:
  `GRANT ALL PRIVILEGES ON mydb.* TO 'myuser'@'localhost';`
  `GRANT ALL PRIVILEGES ON mydb.* TO 'myuser'@'10.10.%.%'; (If needing to connect via something other than localhost)`
  `FLUSH PRIVILEGES;`

#### Previous issues
###### Access denied for debian-sys-maint error:
  It may be necessary to reinstall `mysql`
  Grab password for `debian-sys-maint` from `/etc/mysql/debian.cnf`
  `GRANT ALL PRIVILEGES ON *.* TO 'debian-sys-maint'@'localhost' IDENTIFIED BY '<password>';`

[Source](http://stackoverflow.com/questions/11644300/access-denied-for-user-debian-sys-maint)

###### Links:
[Check and repair myqsl tables:](http://www.thegeekstuff.com/2011/12/mysqlcheck/)