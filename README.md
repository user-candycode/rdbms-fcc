**<h1>Here we will create a unix user as postgress user so that we will not have to invoke super user commands to launch postgres client every time we want to use postgres, also it will be easier to use in projects like developing an app with python or any other language that requires postgres connection.<br>
i.e put o/p of step 1 in place of LINUX_USERNAME anywhere you see it inside a command.</h1>**

## Steps to follow:


### step1: ***Check your user name of account that you use on your machine.***
```bash
LINUX_USERNAME@NAMEofSYSTEM:~$ echo $USER
```
>Note: in this case o/p: LINUX_USERNAME remember this for later use.

<hr>

### step2: ***login as a super user called postgres.***

```bash
LINUX_USERNAME@NAMEofSYSTEM:~$ sudo su - postgres
```
>Note: this will change your unix user to postgres
```bash
postgres@NAMEofSYSTEM:~$
```

<hr>

### step3: ***start psql client to invoke postgres application.***

```bash
postgres@LINUX_USERNAME:~$ psql
```
>Note: This will switch the bash workspace to postgres
```psql
postgres=#
```

<hr>

### step4: ***To review all current roles or list of users.***

```sql
postgres=# \du
```
>Note: "\l" to wiew all  databases, also "\c any_of_the_listed_database_name" to access any data base relations(tables),tuples(rows),attributes(columns),values(data represented using columns and rows) using sql queries

<hr>

### step5: ***Create a new user account named LINUX_USERNAME(here LINUX_USERNAME is the output of step 1 and we will grant it nosuperuser that can perform almost allsuperuser tasks in postgres):***

```sql
postgres=# CREATE USER LINUX_USERNAME WITH PASSWORD 'secretPassword';
```
>Note: If your username consist of any special symbol like '-' i.e LINUX-USERNAME (will throw an error as postgres does not like special symbol in defining any user defined entity anywhere in postgres)
(solution: use double quotes around your user name or any other entity such as defining database name or column name i.e "LINUX-USERNAME")

<hr>

### step6: ***Alter the role to enable a non-expiring password:***

```sql
postgres=# ALTER ROLE LINUX_USERNAME VALID UNTIL 'infinity';
```

<hr>

### step7: ***Alter the role to enable the creation of roles:***

```sql
postgres=# ALTER ROLE LINUX_USERNAME CREATEROLE;
```
<hr>

### step8: ***Alter the role to prevent superuser:***

```sql
postgres=# ALTER ROLE LINUX_USERNAME NOSUPERUSER;
```
<hr>

### step9: ***Grant all table privileges:***

```sql
postgres=# GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO LINUX_USERNAME;
```
<hr>

### step10: ***Type \du to review the new role.***

```sql
postgres=# \du
```
<hr>

### step11: ***Create a database with same name as you created a postgres user i.e o/p of step1.***

```sql
postgres=# CREATE DATABASE LINUX_USERNAME;
```
<hr>

### step12: ***Type \l to view your database amoung all the databases.***

```sql
postgres=# \l
```
<hr>

### step13: ***Exit postgres***

```sql
postgres=# \q
```
<hr>

### step14: ***Exit your superuser***

```bash
postgres@LINUX_USERNAME:~$ exit
```

>Note: NOW you shold be at  
```bash
LINUX_USERNAME@NAMEofSYSTEM:~$
```
<hr>

### step15: ***open new terminal or clear the terminal using 'clear' command and use psql to invoke postgres***

```bash
LINUX_USERNAME@NAMEofSYSTEM:~$ psql
```

>Note: o/p  
```sql
LINUX_USERNAME=>
```

OR

### step15: ***use tuple query executing single query and exiting***

```bash
LINUX_USERNAME@NAMEofSYSTEM:~$ psql -X --username=LINUX_USERNAME --password --dbname=LINUX_USERNAME --no-align --tuples-only -c "\du"
```
>Note:this will prompt for password that was set in step 5 i.e secretPassword, "\du" is the query to be run(type any query between double quotes and it wil run in postgress silently and only display the output)

<hr>

**<h2>Prerequsite: Install postgress on system (will strongly advise to use the default package manager of your distribution other wise "to each his own") Good Luck!!😎</h2>**
