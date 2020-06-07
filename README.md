# SQLServer 

[While](https://www.sqlshack.com/sql-while-loop-understanding-while-loops-in-sql-server/)
| [SSIS](https://www.c-sharpcorner.com/UploadFile/ff0d0f/deployment-models-in-ssis/)
| [Functions](https://docs.microsoft.com/en-us/sql/t-sql/functions/functions?view=sql-server-ver15)
| [AlwaysOn](https://www.red-gate.com/simple-talk/sql/database-administration/sql-server-2012-alwayson/)
| [AlwaysOnAvailibility](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-ver15)[[1]](https://www.youtube.com/watch?v=kOHrHYc6sAM)
| [SecurityGroups](https://www.mssqltips.com/sqlservertip/1831/using-windows-groups-for-sql-server-logins-as-a-best-practice/)
| [SQL Interview Question](https://www.edureka.co/blog/interview-questions/sql-interview-questions)
| [Database Normalization](https://www.studytonight.com/dbms/database-normalization.php)
## SQL Server in different User
Hold <kbd>shift</kbd> and right click on SQL Server Mangement studion icon. You can Run as other windows account user.
## Multiple Instances of SQL Server in one Server
1. 3rd Party s/w may require a DB in a separate instance (CPU core and Memory can be assigned independently)
2. Multiple Languages
3. Versioning of SQL Server
* Instances are of two Types(Default instance, Named Instance)
* In SQL Server 20** Configuration Manager we can find them.

SSMS -> Default Instance -> . or local or Localhost or SysName

SSMS -> Default Instance -> ./Name or local/Name or Localhost/Name or SysName/Name

Course: T-SQL Training with Real World Scenarios:Tricks of the Trade in Udemy
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
## Normallization
Design technique that organizes tables in a manner that reduces redundancy and dependency of data.[[1]](https://www.guru99.com/database-normalization.html)
