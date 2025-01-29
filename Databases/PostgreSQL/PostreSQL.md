# PostgreSQL

`Summary by Ahmad Wali Sharify`

PostgreSQL is a powerful, open source object-relational database. 

A system with over 35 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance.   

You Can install it via its Official Site [postgres](www.postgres.com) For Windows and All other Operating Systems.
After Installation you can Connect to it Via 2 Major Interface:

1. GUI (pgAdmin 4)
2. CLI (Command Based Interface)

pgAdmin is more Graphical and slow in performance alongside CLI a bit tricky but more efficient and useful. 

Connecting and developing databases are a CLI thing, not GUI 
interface.

<br>

# CLI

to run it in any terminal: first install `psql shell`

then to start with a database:
```postgreSQL shell
sudo -u postgres psql
postgres=# create database mydb;
postgres=# create user myuser with encrypted password 'mypass';
postgres=# grant all privileges on database mydb to myuser;

GRANT ALL ON DATABASE pharmacy_v1 TO admin WITH GRANT OPTION;

psql -U postgres -p 5432 -h localhost database-name
// linux = sudo -u postgres psql
-U is for postgres User
-p is for port
-h is for host 
then you will prompt to enter your database password. 
#test= will show you, you are here in postgres CLI Interface
```
- all commands in psql start with \
- all SQL commands in psql ends with **;**


some useful commands in psql:

- \l is for listing all database in your PostgreSQL database
- \d will describe your database
- \c database-name will connect you to that database 
- \q will quit
- \dt will list all your tables in database
- \? is for help
 
some useful SQL commands:

**to Create a Database**
```sql 
CREATE DATABASE test;
```
**to Create a Table**
```sql
CREATE TABLE person (
        id          int,
        name        VARCHAR(50)
    );
```
**to Drop "Delete" a Database or Table:**
```sql
DROP DATABASE test;
DROP TABLE person;
```
