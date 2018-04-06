## PostgreSQL

###### General notes
  * By default, Postgres uses 'ident' authentication, wher eit associates Postgres roles to a matching Unix/Linux system account
  * A user named 'postgres' is created by default when you install the server
  * If a role exists within Postgres, a Unix/Linux username with the same name will be able to sign in as that role

###### Install postgresql:
  `# apt install postgresql postgresql-contrib`

###### Switch to postgres user and access the PostgreSQL prompt as that user:
  `sudo -i -u postgres`
  `psql`

###### Accessing the PostgreSQL prompt without switching accounts
  `sudo -u postgres psql`

###### Create a new role:
  From the PostgreSQL prompt:
  `CREATE ROLE myrole;`
  Or:
  `sudo -u postgres createuser --interactive`

###### Add password to role:
  From the PostgreSQL prompt:
  `ALTER ROLE myrole WITH PASSWORD 'password'`

###### List roles
  From the PostgreSQL prompt:
  \du

###### Drop a role:
  From the PostgreSQL prompt:
  `DROP ROLE myrole;`

###### Grant a role full permissions to a database:
  From the PostgreSQL prompt:
  `GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser;`

###### Create a new database:
  From the PostgreSQL prompt:
  `create database my_db;`

###### List databases:
  `\l`

###### Configure server to listen on interfaces other than localhost:
  Edit `/etc/postgresql/9.5/main/postgresql.conf`
  Set `listen_addresses = '*'`
  Restart postgres


## Previous issues
###### Unable to connect to PostgreSQL from another instance:
  Allow the subnet by editing `/etc/postgresql/9.5/main/pg_hba.conf` and adding:
  `host    all             all             172.16.248.0/22         md5`
