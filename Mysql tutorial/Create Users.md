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