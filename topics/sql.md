# SQL Syntax

```sql
-- (MySQL) Show database users
SELECT * FROM mysql.user;

-- (MySQL) Version info
SHOW VARIABLES LIKE "%version%";

-- (MySQL) Show databases
SHOW DATABASES;

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

-- (MySQL) Update based on another table
UPDATE
  table1,
  table2
SET table1.column1 = table2.column2
WHERE 1
  AND table1.id = table2.id
;

-- Find max length of data in a column
SELECT MAX(LENGTH(@columnName))
FROM @tableName;

-- (MySQL) Find and create DROP TRIGGER statements for all triggers from a database
SELECT CONCAT('DROP TRIGGER ', Trigger_Name, ';')
FROM information_schema.TRIGGERS
WHERE TRIGGER_SCHEMA = @databaseName;
```

## MySQL Cli Commands

```sh
# Check MySQL version
mysql -V

# Restore database to a server
mysql -h<host_name> -u<user_name> -p<password> <database_name> < <file_name>
```