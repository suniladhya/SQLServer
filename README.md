# SQLServer 

[While](https://www.sqlshack.com/sql-while-loop-understanding-while-loops-in-sql-server/)
| [SSIS](https://www.c-sharpcorner.com/UploadFile/ff0d0f/deployment-models-in-ssis/)
| [Functions](https://docs.microsoft.com/en-us/sql/t-sql/functions/functions?view=sql-server-ver15)
| [AlwaysOn](https://www.red-gate.com/simple-talk/sql/database-administration/sql-server-2012-alwayson/)
| [AlwaysOnAvailibility](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-ver15)[[1]](https://www.youtube.com/watch?v=kOHrHYc6sAM)
| [SecurityGroups](https://www.mssqltips.com/sqlservertip/1831/using-windows-groups-for-sql-server-logins-as-a-best-practice/)
| [SQL Interview Question](https://www.edureka.co/blog/interview-questions/sql-interview-questions)
| [Database Normalization](https://www.studytonight.com/dbms/database-normalization.php)
| [FileStream Restore](https://www.sqlshack.com/restoring-a-sql-server-filestream-enabled-database/)
| [Interview](https://www.interviewbit.com/sql-interview-questions/)
| [While Vs Cursor](https://sqlundercover.com/2017/11/16/sql-smackdown-cursors-vs-loops/)
| [Update with Select stmt](https://www.sqlshack.com/how-to-update-from-a-select-statement-in-sql-server/)
|
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
```SQL
declare @TableVariable Table (ColumnName1 nvarchar(150), ColumnName2 nvarchar(150) );
```
## Update with Conditions
```SQL
UPDATE [dbo].[Table] SET ColumnName1 = 
CASE   
  WHEN isNull(ColumnName1,'') = '' THEN 'value'
  WHEN  CHARINDEX('abc', ColumnName1) = 0 THEN ColumnName1+',xyz' 
  ELSE ColumnName1 
END 
  ```
  ```SQL
UPDATE alias1 SET alias1.col1= alias2.col2
FROM Table01 alias1
	INNER JOIN Table01 alias2 
	ON (alias1.coln = alias2.coln AND alias1.col2n = alias2.col2n AND alias1.col3n = alias2.col3n)
WHERE 
alias1.col1 IS Null
AND alias2.col1 IS NOT Null
  ```
## All Columns
```SQL
SELECT COLUMN_NAME
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'Your Table Name'
```
## Normallization
Design technique that organizes tables in a manner that reduces redundancy and dependency of data.[[1]](https://www.guru99.com/database-normalization.html)

## Iterate through each record of a table
* Create a Table Variable with a Record Id and additional Columns
* Iterate through each record using While loop using the Record Id
```sql
DECLARE @Temp TABLE(
	RecordId INT NOT NULL,
	col1 INT NOT NULL,
  col2 VARCHAR(250) NULL,
  col3 VARCHAR(250) NULL
);

INSERT INTO @DoPInterimTemp(RecordId,col1, col2,col3)
	SELECT  ROW_NUMBER() OVER (order by ID) RecordId, src_col1, src_col2, src_col3 
	FROM [dbo].[src_Table]
  
SET @TempCnt = @@ROWCOUNT;

SET @RecCounter = 1;

WHILE @RecCounter <= @TempCnt
  BEGIN
    --Logic to process each record
  END
```
## Duplicate Record on Specific Columns 
[[1]](https://chartio.com/learn/databases/how-to-find-duplicate-values-in-a-sql-table/)
```SQL
SELECT [Col1],[Col2], COUNT(*) [DUPLICATE COUNT] FROM Tab1
GROUP BY [Col1],[Col2]
HAVING COUNT(*) > 1
AND [Col1] = 'Val'
```

## Multiple Join Condition
```SQL
select one.*, two.meal
from table1 as one
left join table2 as two
on (one.weddingtable = two.weddingtable and one.tableseat = two.tableseat)

```
## Multiple Transaction
```SQL
BEGIN TRANSACTION one;
BEGIN TRY
    /*SQL statements goes here*/
END TRY
BEGIN CATCH
    IF @@TRANCOUNT > 0
        ROLLBACK TRANSACTION one;

END CATCH

IF @@TRANCOUNT > 0
    COMMIT TRANSACTION one;


BEGIN TRANSACTION two;
BEGIN TRY
    /*SQL statements goes here*/
END TRY
BEGIN CATCH
    IF @@TRANCOUNT > 0
        ROLLBACK TRANSACTION two;
END CATCH

IF @@TRANCOUNT > 0
    COMMIT TRANSACTION two;
```    
