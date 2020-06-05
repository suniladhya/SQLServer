# SQLServer 

[While](https://www.sqlshack.com/sql-while-loop-understanding-while-loops-in-sql-server/)
| [SSIS](https://www.c-sharpcorner.com/UploadFile/ff0d0f/deployment-models-in-ssis/)
| [Functions](https://docs.microsoft.com/en-us/sql/t-sql/functions/functions?view=sql-server-ver15)
| [AlwaysOn](https://www.red-gate.com/simple-talk/sql/database-administration/sql-server-2012-alwayson/)
| [AlwaysOnAvailibility](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-ver15)
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
