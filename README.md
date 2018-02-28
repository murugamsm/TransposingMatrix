## To transpose query results

EXEC MATRIX.TRANSPOSING
     @query = 'SELECT * FROM SYS.DATABASES';

## To save transposing query results in a temporary or permanent table.

EXEC MATRIX.TRANSPOSING
     @query = 'SELECT * FROM sys.databases',
     @tableName = N'##tempTable';
     
---The same result as in the first query

SELECT *
FROM ##tempTable;

## To choose transposing column

--The first column - name

EXEC MATRIX.Transposing @Query = N'SELECT * FROM sys.databases'
				   ,@Rco = 0;
				   
--The second column - database_id

EXEC MATRIX.Transposing @Query = N'SELECT * FROM sys.databases'
				   ,@Rco = 1;


## To filter before transposing

EXEC MATRIX.Transposing
     @Query = N'SELECT * FROM sys.databases WHERE database_id >= @id1 AND database_id <= @id2;',
     @Params = N'@id1 int=1,@Id2 int=4';

## To transpose with generic header ( key, value, value1 and so on )

EXEC MATRIX.Transposing
     @Query = N'SELECT * FROM sys.databases;',
     @KeyValueOption = 1;


##To transpose with custom header

EXEC MATRIX.Transposing @Query = N'SELECT * FROM sys.databases;'
					  ,@KeyValueOption = 1
					  ,@ColumnMapping = N'Database name,Sys database master'

