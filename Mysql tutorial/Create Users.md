# Create Users

source: `{{ page.path }}`


## MySQL CREATE USER Example
The following are the step required to create a new user in the MySQL server database.
```sql
Step 1: Open the MySQL server by using the mysql client tool.

Step 2: Enter the password for the account and press Enter.

Enter Password: ********  
Step 3: Execute the following command to show all users in the current MySQL server.

mysql> select user from mysql.user;  
We will get the output as below:
mysql> select user from mysql.user;
+------------------+
| user             |
+------------------+
| jame             |
| musk             |
| mysql.infoschema |
| mysql.session    |
| mysql.sys        |
| root             |
| writer           |
+------------------+
8 rows in set (0.00 sec)

mysql>

Step 4: Create a new user with the following command.
mysql>
mysql> CREATE USER IF NOT EXISTS sindhuri@localhost IDENTIFIED BY 'Internal@123';
Query OK, 0 rows affected (0.01 sec)

mysql>
```

```javascript
Grant Privileges to the MySQL New User
MySQL server provides multiple types of privileges to a new user account. Some of the most commonly used privileges are given below:

1. ALL PRIVILEGES: It permits all privileges to a new user account.
2. CREATE: It enables the user account to create databases and tables.
3. DROP: It enables the user account to drop databases and tables.
4. DELETE: It enables the user account to delete rows from a specific table.
5. INSERT: It enables the user account to insert rows into a specific table.
6. SELECT: It enables the user account to read a database.
7. UPDATE: It enables the user account to update table rows.
```
```sql
If you want to give all privileges to a newly created user, execute the following command.
mysql> GRANT ALL PRIVILEGES ON * . * TO sindhuri@localhost;  

If you want to give specific privileges to a newly created user, execute the following command.
mysql> GRANT CREATE, SELECT, INSERT ON * . * TO sindhuri@localhost;  

Sometimes, you want to flush all the privileges of a user account for changes occurs immediately, type the following command.
FLUSH PRIVILEGES;  

If you want to see the existing privileges for the user, execute the following command.
mysql> SHOW GRANTS for username;  
```
## Create a user database and grant privilages

```sql
mysql> select user from mysql.user;
+------------------+
| user             |
+------------------+
| jame             |
| musk             |
| mysql.infoschema |
| mysql.session    |
| mysql.sys        |
| root             |
| writer           |
+------------------+
8 rows in set (0.00 sec)
mysql>

mysql> CREATE USER IF NOT EXISTS sindhuri@localhost IDENTIFIED BY 'Internal@123';
Query OK, 0 rows affected (0.01 sec)

mysql>


mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| student            |
| sys                |
| vehicles           |
+--------------------+
6 rows in set (0.00 sec)
mysql>

creating internal database 

mysql> create database internal;
Query OK, 1 row affected (0.00 sec)

mysql>

mysql> use internal;
Database changed
mysql>

Creating a table lists under internal database
mysql> create table lists( id int auto_increment primary key, todo varchar(100) not null, completed bool default false);
Query OK, 0 rows affected (0.01 sec)

mysql> 

Providing grant privilages to user sindhuri for internal database
mysql> grant all privileges on internal.* to sindhuri@localhost;
Query OK, 0 rows affected (0.00 sec)

mysql>

mysql -u sindhuri -p
Enter password: *********
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| internal           |
+--------------------+
2 rows in set (0.00 sec)

mysql> use internal;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+--------------------+
| Tables_in_internal |
+--------------------+
| lists              |
+--------------------+
1 row in set (0.00 sec)

mysql> select * from lists;
Empty set (0.00 sec)

mysql>
```

## Grant Permissions  in different ways

The CREATE USER statement creates one or more user accounts with no privileges. It means that the user accounts can log in to the MySQL Server, but cannot do anything such as selecting a database and querying data from tables.

To allow user accounts to work with database objects, you need to grant the user accounts privileges. And the GRANT statement grants a user account one or more privileges.

The following illustrates the basic syntax of the GRANT statement:

```sql
`Syntax:` 

GRANT privilege [,privilege],.. 
ON privilege_level 
TO account_name;

* This example grants the SELECT privilege on the table employees  in the sample database to the user acount bob@localhost:

GRANT SELECT ON employees TO bob@localhost;

* The following example grants UPDATE, DELETE, and INSERT privileges on the table employees to bob@localhost:

GRANT INSERT, UPDATE, DELETE ON employees TO bob@localhost;

```
Specify the `privilege_level` that determines the level to which the privileges apply. MySQL supports the following main `privilege levels`

![](./images/1.PNG)

`Global privileges` apply to all databases in a MySQL Server. To assign global privileges, you use the *.* syntax, for example:
```sql
GRANT SELECT ON *.* TO bob@localhost;

The account user bob@localhost can query data from all tables in all database of the current MySQL Server.
```
`Database privileges` apply to all objects in a database. To assign database-level privileges, you use the ON database_name.* syntax, for example:
```sql
GRANT INSERT ON classicmodels.* TO bob@localhost;

In this example, bob@localhost can insert data into all tables in the classicmodels database.
```
`Table privileges` apply to all columns in a table. To assign table-level privileges, you use the ON database_name.table_name syntax, for example:
```sql
GRANT DELETE ON classicmodels.employees TO bob@localhsot;

In this example, bob@localhost can delete rows from the table employees in the database classicmodels.

If you skip the database name, MySQL uses the default database or issues an error if there is no default database
```
`Column privileges` apply to single columns in a table.  You must specify the column or columns for each privilege, for example:
```sql
GRANT 
   SELECT (employeeNumner,lastName, firstName,email), 
   UPDATE(lastName) 
ON employees 
TO bob@localhost;

In this example, bob@localhost can select data from four columns employeeNumber, lastName, firstName, and email and update only the lastName column in the employees table.
```
`Proxy user privileges` allow one user to be a proxy for another. The proxy user gets all privileges of the proxied user. For example:
```sql
GRANT PROXY 
ON root 
TO alice@localhost;

In this example, alice@localhost assumes all privileges of root.

Finally, specify the account name of the user that you want to grant privileges after the TO keyword.

Notice that in order to use the GRANT statement, you must have the GRANT OPTION privilege and the privileges that you are granting. If the read_only system variable is enabled, you need to have the SUPER privilege to execute the GRANT statement.
```