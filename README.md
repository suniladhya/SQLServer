# SQLServer 

[While](https://www.sqlshack.com/sql-while-loop-understanding-while-loops-in-sql-server/)
## Table Variable
```
declare @TableVariable Table (ColumnName1 nvarchar(150), ColumnName2 nvarchar(150) );
```
## Update with Conditions
```
UPDATE [dbo].[Table] SET ColumnName1 = 
CASE   
  WHEN isNull(ColumnName1,'') = '' THEN 'value'
  WHEN  CHARINDEX('abc', ColumnName1) = 0 THEN ColumnName1+',xyz' 
  ELSE ColumnName1 
END 
  ```
## All Columns
```
SELECT COLUMN_NAME
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'Your Table Name'
```
