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

Syntax: 
```sql
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

In this example, bob@localhost can select data from four columns employeeNumber, lastName, firstName, and email and 

update only the lastName column in the employees table.
```
`Stored routine privileges` apply to stored procedures and stored functions, for example:
```sql
GRANT EXECUTE 
ON PROCEDURE CheckCredit 
TO bob@localhost;

In this example, bob@localhost can execute the stored procedure CheckCredit in the current database.
```
`Proxy user privileges` allow one user to be a proxy for another. The proxy user gets all privileges of the proxied user. For example:
```sql
GRANT PROXY 
ON root 
TO alice@localhost;

In this example, alice@localhost assumes all privileges of root.

Finally, specify the account name of the user that you want to grant privileges after the TO keyword.

Notice that in order to use the GRANT statement, you must have the GRANT OPTION privilege and the privileges that you are 

granting. If the read_only system variable is enabled, you need to have the SUPER privilege to execute the GRANT 

statement.
```
##  Revoke some privilages to users

```sql
Create a user account named dave@localhost
mysql>
mysql> create user dave@localhost identified by 'SecretPass1!';
Query OK, 0 rows affected (0.01 sec)

Create a test database 
mysql>
mysql> create database test;
Query OK, 1 row affected (0.00 sec)

Grant dave@localhost the SELECT, UPDATE, and INSERT privileges on the test  database:
mysql>
mysql> grant update,select,delete on test.* to dave@localhost;
Query OK, 0 rows affected (0.01 sec)

Display the granted privileges of the dave@localhost user account:
mysql>
mysql> show grants for dave@localhost;
+----------------------------------------------------------------+
| Grants for dave@localhost                                      |
+----------------------------------------------------------------+
| GRANT USAGE ON *.* TO `dave`@`localhost`                       |
| GRANT SELECT, UPDATE, DELETE ON `test`.* TO `dave`@`localhost` |
+----------------------------------------------------------------+
2 rows in set (0.00 sec)

mysql>
mysql>

Revoke the UPDATE and INSERT privileges from dave@localhost:
mysql>
mysql> revoke update,delete on test.* from dave@localhost;
Query OK, 0 rows affected (0.00 sec)

Display the granted privileges of the dave@localhost user account:
mysql>
mysql> show grants for dave@localhost;
+------------------------------------------------+
| Grants for dave@localhost                      |
+------------------------------------------------+
| GRANT USAGE ON *.* TO `dave`@`localhost`       |
| GRANT SELECT ON `test`.* TO `dave`@`localhost` |
+------------------------------------------------+
2 rows in set (0.00 sec)

mysql>


ex 2 . Using MySQL REVOKE to revoke all privileges from a user account 

mysql>
mysql> grant execute on test.* to dave@localhost;
Query OK, 0 rows affected (0.00 sec)

mysql>
mysql> show grants for dave@localhost;
+---------------------------------------------------------+
| Grants for dave@localhost                               |
+---------------------------------------------------------+
| GRANT USAGE ON *.* TO `dave`@`localhost`                |
| GRANT SELECT, EXECUTE ON `test`.* TO `dave`@`localhost` |
+---------------------------------------------------------+
2 rows in set (0.00 sec)
mysql>
mysql>

Revoke all privileges of the dave@localhost user account by using the REVOKE ALL statement:
mysql>
mysql> revoke all,grant option from dave@localhost;
Query OK, 0 rows affected (0.00 sec)

mysql>
mysql> show grants for dave@localhost;
+------------------------------------------+
| Grants for dave@localhost                |
+------------------------------------------+
| GRANT USAGE ON *.* TO `dave`@`localhost` |
+------------------------------------------+
1 row in set (0.00 sec)

mysql>
mysql>

```note
When the MySQL REVOKE command takes effect
The effect of REVOKE statement depends on the privilege level:

`Global level`

The changes take effect when the user account connects to the MySQL Server in the subsequent sessions. The changes are not applied to all currently connected users.

`Database level`

The changes take effect after the next USE statement.

`Table and column levels`

The changes take effect on all subsequent queries.

```
## MySQL roles and Management

If you want to grant the same set of privileges to multiple users, you follow these steps:

* First, create a new role.
* Second, grant privileges to the role.
* Third, grant the role to the users.
In case you want to change the privileges of the users, you need to change the privileges of the granted role only. The changes will take effect to all users to which the role granted.

```sql
create a new database named CRM, which stands for customer relationship management

mysql> create database crm;
Query OK, 1 row affected (0.00 sec)
mysql>

mysql> use crm;
Database changed
mysql>

create customer table inside the CRM database.
mysql> create table customers( id int primary key auto_increment, first_name varchar(255) NOT NULL, last_name varchar(255) NOT NULL,phone varchar(25) NOT NULL, email varchar(255));
Query OK, 0 rows affected (0.02 sec)

mysql>
mysql> show tables;
+---------------+
| Tables_in_crm |
+---------------+
| customers     |
+---------------+
1 row in set (0.00 sec)

mysql>
mysql> describe table customers;
+----+-------------+-----------+------------+------+---------------+------+---------+------+------+----------+-------+
| id | select_type | table     | partitions | type | possible_keys | key  | key_len | ref  | rows | filtered | Extra |
+----+-------------+-----------+------------+------+---------------+------+---------+------+------+----------+-------+
|  1 | SIMPLE      | customers | NULL       | ALL  | NULL          | NULL | NULL    | NULL |    1 |   100.00 | NULL  |
+----+-------------+-----------+------------+------+---------------+------+---------+------+------+----------+-------+
1 row in set, 1 warning (0.00 sec)

After that, insert data into the customers table.
mysql>
mysql> INSERT INTO customers(first_name,last_name,phone,email) VALUES('John','Doe','(408)-987-7654','john.doe@mysqltrial.org'),('Lily','Bush','(408)-987-7985','lily.bush@mysqltrial.org');
Query OK, 2 rows affected (0.01 sec)
Records: 2  Duplicates: 0  Warnings: 0
mysql>
mysql>
mysql> select * from  customers;
+----+------------+-----------+----------------+-----------------------------+
| id | first_name | last_name | phone          | email                       |
+----+------------+-----------+----------------+-----------------------------+
|  1 | John       | Doe       | (408)-987-7654 | john.doe@mysqltrial.org  |
|  2 | Lily       | Bush      | (408)-987-7985 | lily.bush@mysqltrial.org |
+----+------------+-----------+----------------+-----------------------------+
2 rows in set (0.00 sec)
mysql> 
mysql>
Delete the user with name John in customers table 
mysql> delete from  customers where first_name = "John";
Query OK, 1 row affected (0.00 sec)

mysql> select * from  customers;
+----+------------+-----------+----------------+-----------------------------+
| id | first_name | last_name | phone          | email                       |
+----+------------+-----------+----------------+-----------------------------+
|  2 | Lily       | Bush      | (408)-987-7985 | lily.bush@mysqltrial.org |
+----+------------+-----------+----------------+-----------------------------+
1 row in set (0.00 sec)

mysql> delete from  customers where first_name = "lily";
Query OK, 1 row affected (0.00 sec)

mysql>
mysql>
mysql> select * from  customers;
Empty set (0.00 sec)

Inserting the correct email of users  and inserting to customers table
mysql> INSERT INTO customers(first_name,last_name,phone,email) VALUES('John','Doe','(408)-987-7654','john.doe@mysql.org'),('Lily','Bush','(408)-987-7985','lily.bush@mysql.org');
Query OK, 2 rows affected (0.01 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql>
mysql>
mysql> select * from  customers;
+----+------------+-----------+----------------+---------------------+
| id | first_name | last_name | phone          | email               |
+----+------------+-----------+----------------+---------------------+
|  3 | John       | Doe       | (408)-987-7654 | john.doe@mysql.org  |
|  4 | Lily       | Bush      | (408)-987-7985 | lily.bush@mysql.org |
+----+------------+-----------+----------------+---------------------+
2 rows in set (0.00 sec)

mysql>
mysql>

Here commit it updates to and show to new sessions users
mysql> commit;
Query OK, 0 rows affected (0.00 sec)

It will rollback to previous session of current user
mysql>
mysql> rollback;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from  customers;
+----+------------+-----------+----------------+---------------------+
| id | first_name | last_name | phone          | email               |
+----+------------+-----------+----------------+---------------------+
|  3 | John       | Doe       | (408)-987-7654 | john.doe@mysql.org  |
|  4 | Lily       | Bush      | (408)-987-7985 | lily.bush@mysql.org |
+----+------------+-----------+----------------+---------------------+
2 rows in set (0.00 sec)
mysql>

```

Creating roles: 

To interact with the CRM database, you need to create accounts for developers who need full access to the database. In addition, you need to create accounts for users who need only read access and others who need both read/write access.

To avoid granting privileges to each user account individually, you create a set of roles and grant the appropriate roles to each user account.

```sql
To create new roles, you use CREATE ROLE statement:

mysql> create role crm_dev,crm_read,crm_write;
Query OK, 0 rows affected (0.00 sec)

mysql> 

To grant privileges to a role, you use GRANT statement. The following statement grants all privileges to crm_dev role:
mysql>
mysql> grant all on crm.* to crm_dev;
Query OK, 0 rows affected (0.00 sec)

The following statement grants SELECT privilege to crm_read role:
mysql>
mysql> grant select on crm.*  to crm_read;
Query OK, 0 rows affected (0.00 sec)
mysql>

The following statement grants INSERT, UPDATE, and DELETE privileges to crm_write role

mysql> grant insert,update,delete on crm.* to crm_write;
Query OK, 0 rows affected (0.00 sec)

```
Assigning roles to user accounts
Suppose you need one user account as the developer, one user account that can have read-only access and two user accounts that can have read/write access.

To create new users, you use CREATE USER statements as follows:
```sql
-- developer user 
mysql>
mysql> CREATE USER crm_dev1@localhost IDENTIFIED BY 'Secure$1782';
Query OK, 0 rows affected (0.01 sec)
-- read access user
mysql>
mysql> CREATE USER crm_read1@localhost IDENTIFIED BY 'Secure$5432';
Query OK, 0 rows affected (0.01 sec)

-- read/write users
mysql>
mysql> CREATE USER crm_write1@localhost IDENTIFIED BY 'Secure$9075';
Query OK, 0 rows affected (0.01 sec)

mysql>
mysql> CREATE USER crm_write2@localhost IDENTIFIED BY 'Secure$3452';
Query OK, 0 rows affected (0.01 sec)
mysql>

The following statement grants the crm_rev role to the user account crm_dev1@localhost:
mysql>
mysql> grant crm_dev to crm_dev1@localhost;
Query OK, 0 rows affected (0.00 sec)
mysql>

The following statement grants the crm_read role to the user account crm_read1@localhost
mysql> grant crm_read to crm_read1@localhost;
Query OK, 0 rows affected (0.01 sec)
mysql>

The following statement grants the crm_read and crm_write roles to the user accounts crm_write1@localhost and crm_write2@localhost:
mysql> grant crm_read,crm_write to crm_write1@localhost,crm_write2@localhost;
Query OK, 0 rows affected (0.01 sec)
mysql>

To verify the role assignments, you use the SHOW GRANTS statement as the following example
mysql> show grants for crm_dev1@localhost;
+-----------------------------------------------+
| Grants for crm_dev1@localhost                 |
+-----------------------------------------------+
| GRANT USAGE ON *.* TO `crm_dev1`@`localhost`  |
| GRANT `crm_dev`@`%` TO `crm_dev1`@`localhost` |
+-----------------------------------------------+
2 rows in set (0.00 sec)
mysql>

mysql> show grants for crm_read1@localhost;
+-------------------------------------------------+
| Grants for crm_read1@localhost                  |
+-------------------------------------------------+
| GRANT USAGE ON *.* TO `crm_read1`@`localhost`   |
| GRANT `crm_read`@`%` TO `crm_read1`@`localhost` |
+-------------------------------------------------+
2 rows in set (0.00 sec)

mysql> show grants for crm_write1@localhost;
+------------------------------------------------------------------+
| Grants for crm_write1@localhost                                  |
+------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `crm_write1`@`localhost`                   |
| GRANT `crm_read`@`%`,`crm_write`@`%` TO `crm_write1`@`localhost` |
+------------------------------------------------------------------+
2 rows in set (0.00 sec)

mysql> 
mysql>
mysql> show grants for crm_write2@localhost;
+------------------------------------------------------------------+
| Grants for crm_write2@localhost                                  |
+------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `crm_write2`@`localhost`                   |
| GRANT `crm_read`@`%`,`crm_write`@`%` TO `crm_write2`@`localhost` |
+------------------------------------------------------------------+
2 rows in set (0.00 sec)

mysql>

To specify which roles should be active each time a user account connects to the database server, you use the SET DEFAULT ROLE statement.

The following statement sets the default for the crm_read1@localhost account all its assigned roles 

mysql>
mysql> SET DEFAULT ROLE ALL TO crm_read1@localhost;
Query OK, 0 rows affected (0.00 sec)
mysql>

mysql>mysql -u crm_read1 -p
Enter password:**********
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| crm                |
| information_schema |
+--------------------+
2 rows in set (0.00 sec)

mysql> use crm;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+---------------+
| Tables_in_crm |
+---------------+
| customers     |
+---------------+
1 row in set (0.00 sec)

mysql> select current_role();
+----------------+
| current_role() |
+----------------+
| `crm_read`@`%` |
+----------------+
1 row in set (0.00 sec)

mysql> SELECT COUNT(*) FROM customers;
+----------+
| COUNT(*) |
+----------+
|        2 |
+----------+
1 row in set (0.00 sec)

mysql>
```
`Setting active roles`
A user account can modify the current user’s effective privileges within the current session by specifying which granted role are active.
```sql
The following statement set the active role to NONE, meaning no active role.
SET ROLE NONE;

To set active roles to all granted role, you use:
SET ROLE ALL;

To set active roles to default roles that set by the SET DEFAULT ROLE statement, you use:
SET ROLE DEFAULT;
```

`Revoking privileges from roles`
To revoke privileges from a specific role, you use the REVOKE statement. The REVOKE statement takes effect not only the role but also any account granted the role.

```sql
mysql> revoke insert,delete,update  on crm.* from crm_write;
Query OK, 0 rows affected (0.01 sec)

mysql>
mysql> drop role crm_read, crm_write;
Query OK, 0 rows affected (0.00 sec)
mysql>
mysql>
```

`Copying privileges from a user account to another`
MySQL treats user accounts like roles, therefore, you can grant a user account to another user account like granting a role to that user account. This allows you to copy privileges from a user to another user.

Suppose you need another developer account for the CRM database
```sql
mysql>
mysql> CREATE USER crm_dev2@localhost IDENTIFIED BY 'Secure$6275';
Query OK, 0 rows affected (0.01 sec)

copy privileges from the crm_dev1 user account to crm_dev2 user account as follows:
mysql> GRANT crm_dev1@localhost TO crm_dev2@localhost;
Query OK, 0 rows affected (0.01 sec)
mysql>
```