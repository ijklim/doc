# Setting variables

  ```sql
  SET
    @columnName = '',
    @databaseName = '',
    @tableName = ''
  ;
  ```

# Tables in a database

  ```sql
  SELECT TABLE_NAME FROM information_schema.tables
  WHERE TABLE_SCHEMA = @databaseName;
  ```
# Find all tables with a specific column name

  ```sql
  SELECT DISTINCT TABLE_NAME
  FROM INFORMATION_SCHEMA.COLUMNS
  WHERE 1
    AND COLUMN_NAME = @columnName
    AND TABLE_SCHEMA = @databaseName
  ;
  ```

# Update based on another table

  ```sql
  -- MySQL
  UPDATE
    table1,
    table2
  SET table1.column1 = table2.column2
  WHERE 1
    AND table1.id = table2.id
  ;
  ```

# Find max length of data in a column

  ```sql
  SELECT MAX(LENGTH(@columnName))
  FROM @tableName;
  ```
