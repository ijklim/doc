# SQL

* XAMPP Replacing MariaDB with MySQL: https://odan.github.io/2019/11/17/xampp-replacing-mariadb-with-mysql-8.html
## SQL Commands

```sql
-----------
-- MySQL --
-----------
-- Version info
SHOW VARIABLES LIKE "%version%";
SELECT VERSION();

-- Show database users
SELECT * FROM mysql.user;
-- Create user
CREATE USER 'admin'@'%' IDENTIFIED WITH caching_sha2_password BY 'db_password_here';
-- Change password
ALTER USER 'root'@'localhost' IDENTIFIED BY 'PASSWORD_HERE';
-- Permission
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

-- Show databases
SHOW DATABASES;
-- Create database
CREATE DATABASE <DATABASE_NAME> CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Find and create DROP TRIGGER statements for all triggers from a database
SELECT CONCAT('DROP TRIGGER ', Trigger_Name, ';')
FROM information_schema.TRIGGERS
WHERE TRIGGER_SCHEMA = @databaseName;

-- Update based on another table
UPDATE
  table1,
  table2
SET table1.column1 = table2.column2
WHERE 1
  AND table1.id = table2.id
;


-- Setting variables
SET
  @columnName = '',
  @databaseName = '',
  @tableName = ''
;

-- List tables in a database
SELECT TABLE_NAME FROM information_schema.tables
WHERE TABLE_SCHEMA = @databaseName;

-- Find all tables with a specific column name
SELECT DISTINCT TABLE_NAME
FROM INFORMATION_SCHEMA.COLUMNS
WHERE 1
  AND COLUMN_NAME = @columnName
  AND TABLE_SCHEMA = @databaseName
;

-- Find max length of data in a column
SELECT MAX(LENGTH(@columnName))
FROM @tableName;

-- IF statement
SELECT IF(orders.date_entered > '2021-08-08', 1, 0) AS recent FROM orders;
```

## MySQL Cli Commands

```sh
# Check MySQL version
mysql -V

# Restore database to a server
mysql -h<host_name> -u<user_name> -p<password> <database_name> < <file_name>
```