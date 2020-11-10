# SQLServer 

[While](https://www.sqlshack.com/sql-while-loop-understanding-while-loops-in-sql-server/)
| [SSIS](https://www.c-sharpcorner.com/UploadFile/ff0d0f/deployment-models-in-ssis/)
| [Functions](https://docs.microsoft.com/en-us/sql/t-sql/functions/functions?view=sql-server-ver15)
| [AlwaysOn1](https://www.red-gate.com/simple-talk/sql/database-administration/sql-server-2012-alwayson/)
| [AlwaysOn2](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-ver15#:~:text=In%20a%20read%2Dscale%20availability,node%20of%20the%20same%20WSFC.)
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
## StoredProc Format
```SQL
SET ANSI_NULLS ON  
GO  
SET QUOTED_IDENTIFIER ON  
GO  
-- =============================================
-- Stored Procedure Name : [dbo].[usp_StoredProcedureName]
-- Author:      <Author,,Name>  
-- Create date: <Create Date,,>  
-- Description: <Description,,>  
-- =============================================
IF EXISTS (SELECT * FROM sysobjects WHERE id = object_id(N'[dbo].[SPNAME]') AND OBJECTPROPERTY(id, N'IsProcedure') = 1)
BEGIN
	DROP PROCEDURE dbo.SPNAME
END
CREATE PROCEDURE [dbo].[usp_StoredProcedureName]
(
	@Parameter1 INT
	,@Parameter2 VARCHAR(50)
	,@ReturnValue1 INT OUTPUT
	,@ErrorCode INT = 0 OUTPUT
) AS
/*
	*****************************Revision Details*****************************
	Project/
	Revision No. Changed On  Changed By  Change Description
	------------ ----------  ----------  ------------------
	1234	     2018/01/10   Mr. ABC     New column 'NewColumnName' added.
	1235         2018/03/16   Mr. XYZ     Column 'ColumnName' deleted.
*/
 
BEGIN
	SET NOCOUNT ON
	BEGIN TRY
		BEGIN TRANSACTION
			--INSERT statement and other logic go here.
		COMMIT TRANSACTION
		RETURN 0
	END TRY
	BEGIN CATCH
		IF @@TRANCOUNT > 0
		ROLLBACK TRANSACTION
		RETURN 1
	END CATCH
END
```
## Stored Procedure Catch Block
  ```SQL
  PRINT 'XACT_State(-1: Uncommittable, 1:Committable, 0:No active user transaction):'
  PRINT XACT_STATE();
  SELECT ERROR_NUMBER() AS ErrorNumber  
            ,ERROR_SEVERITY() AS ErrorSeverity  
            ,ERROR_STATE() AS ErrorState  
            ,ERROR_PROCEDURE() AS ErrorProcedure  
            ,ERROR_LINE() AS ErrorLine  
            ,ERROR_MESSAGE() AS ErrorMessage; 	    
```
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
## Always On
There are two different architectures for availability groups.
1. Always On availability groups
2. Read-scale availability group

## Simple Cursor
```sql
DECLARE @cur1_cid int                
 DECLARE cur CURSOR LOCAL FOR                
    SELECT DISTINCT col1  FROM [dbo].[Table3] 
	WHERE Col3 
	IN(
	SELECT c.Id from Table1 cs
	Inner Join Table2 c on cs.Name = c.Name)
 OPEN cur                
 FETCH NEXT FROM cur INTO @cur1_cid                
 WHILE @@FETCH_STATUS = 0                
  BEGIN                
   EXEC StoredProc @cur1_cid                
   FETCH NEXT FROM cur INTO @cur1_cid                
  END                
 CLOSE cur                
 DEALLOCATE cur 
 ```
 ```sql
 DECLARE 
    @product_name VARCHAR(MAX), 
    @list_price   DECIMAL;

DECLARE cursor_product CURSOR
FOR SELECT 
        product_name, 
        list_price
    FROM 
        production.products;

OPEN cursor_product;

FETCH NEXT FROM cursor_product INTO 
    @product_name, 
    @list_price;

WHILE @@FETCH_STATUS = 0
    BEGIN
        PRINT @product_name + CAST(@list_price AS varchar);
        FETCH NEXT FROM cursor_product INTO 
            @product_name, 
            @list_price;
    END;

CLOSE cursor_product;

DEALLOCATE cursor_product;
 ```
## Objet Definition
### View
```SQL
SELECT DEFINITION 
FROM SYS.OBJECTS O JOIN SYS.SQL_MODULES M ON M.object_id = O.object_id
WHERE O.object_id = object_id( '[SCHEMA].[ViewName]') AND O.TYPE = 'V'
```
## Dynamic Replacement in a string
```SQL
declare @vSurveyMessage Nvarchar(1000)
declare @vfirstname Nvarchar(1000)

set @vSurveyMessage =  'Recently we invited you to participate in a survey to help  + [@vfirstname]';

set @vfirstname = 'Hello'
set @vSurveyMessage= REPLACE(@vSurveyMessage,'[@vfirstname]','Hello Sunil')
print @vSurveyMessage

```
