# TSQL

## Stored procedure template

```sql
/***************************************************************************************
* Database      :
*
* Name          : SampleProcedure
*
* Purpose       :
*
* Versions      : dd/mm/yyyy   v1.0.0   FirstName LastName     Description
*
* Dataset Test  :
*
****************************************************************************************/

CREATE PROCEDURE [dbo].[SampleProcedure]
(
  @var1 VARCHAR(50),
)
WITH EXECUTE AS OWNER AS
BEGIN
  BEGIN TRY

    -- 1) START
    PRINT(CONVERT (VARCHAR (40),GETDATE(),20 ) + ' : 1) START')

    BEGIN TRANSACTION NameProc_NameTransaction -- ********************************************************
    -- /!\ If the name of the transaction is not set "Commit Transaction" commit all open transactions
        -- so if we have nested stored procedure execution we are fucked up

        -- 2) Process
    -- -------
    -- MY CODE
    -- With CREATE And UPDATE in real db table, the rollback is necessary if an error occurs with a named transaction
    -- -------

    -- 2.b) Raise an error manualy
    -- RAISERROR(N'my error message',16,1)

    COMMIT TRANSACTION NameProc_NameTransaction

        -- 3) END
    PRINT(CONVERT (VARCHAR (40),GETDATE(),20 ) + ' : 3) END')

  END TRY
  BEGIN CATCH
  -- Rollback
    IF @@TRANCOUNT > 0
    BEGIN
      ROLLBACK TRANSACTION NameProc_NameTransaction
    END

  -- Throw error
        -- Simple error mesage
        --SET @ErrMsg = ERROR_MESSAGE()
    --PRINT(@ErrMsg)

        -- Created error message
    DECLARE @ErrMsg nvarchar(4000), @ErrSeverity int
    SET @ErrMsg = '[ErrorCode: ' + Convert(varchar, ERROR_NUMBER()) + '] Message: ' + ERROR_MESSAGE() +'(' + ERROR_PROCEDURE() + ': ligne ' + Convert(varchar, ERROR_LINE()) + ')'
    PRINT(@ErrMsg)
    SET @ErrSeverity = ERROR_SEVERITY()
    RAISERROR(N'ERROR: %s',@ErrSeverity,1,@ErrMsg)

  END CATCH
END
```

## Import csv

```sql
BULK INSERT Environment.Store
FROM 'C:\MyPath\MyFile.csv'
WITH
(
    FIRSTROW = 2,           -- Remove header
    FIELDTERMINATOR = ';',  -- CSV field delimiter
    ROWTERMINATOR = '\n',   -- Use to shift the control to next row
    TABLOCK
)
```

## New Identity

Change the next auto incremental value

```sql
-- Check the next id identity
DBCC CHECKIDENT ('MyTable');
-- Set the next id identity
DBCC CHECKIDENT ('MyTable', RESEED, 7777777);
-- Set the normal behavior with next id identity + 1
DBCC CHECKIDENT ('MyTable',NORESEED);
```

## Monitoring

```sql
-- Get last modification date
SELECT name, create_date, modify_date
FROM sys.objects
WHERE type = 'P'and name = 'MyProc'

-- Get all execution in progress
SELECT    OBJECT_NAME(sqltext.objectid) AS ObjectName,
        req.session_id, req.start_time, req.status, req.command, req.database_id, req.user_id, req.wait_time,
        req.open_transaction_count, req.open_resultset_count, req.transaction_id, req.cpu_time, req.total_elapsed_time,
        con.[client_net_address], ses.[login_time], ses.host_name, ses.program_name, ses.client_interface_name, ses.login_name,
        ses.nt_domain, ses.nt_user_name, ses.status, ses.original_login_name,
        dbo.TRIM(sqltext.[TEXT]) AS CleanQuery, sqltext.[TEXT] AS Query
FROM sys.dm_exec_requests req
INNER JOIN sys.dm_exec_connections con ON con.session_id = req.session_id
INNER JOIN sys.dm_exec_sessions ses ON ses.session_id = req.session_id
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS sqltext
WHERE 1=1
AND sqltext.[TEXT] NOT LIKE '%SELECT%dm_exec_requests%'
AND sqltext.[TEXT] <> 'sp_server_diagnostics'
AND req.start_time <= DATEADD(mi, -1, GETDATE())
--AND [TEXT] LIKE '%%'
--AND con.[client_net_address] = ''
ORDER BY req.start_time
```

## Work with xml

- Todo
