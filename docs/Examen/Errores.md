# Errores

No borres el fichero `ErrorViewModel.cs`


## Error al borrar base de datos en SQL SERVER
El error se debe a que hay todavía conexiones activas, para ello, ejecutamos el siguiente comando para visualizar si hay conexiones activas en la base de datos.
```sql
SELECT *
FROM sys.sysprocesses
WHERE DB_NAME(dbid) = 'NOMBRE_DB'
```
Si hay conexiones activas, hay que desconectarlas con el siguiente comando. 

```sql
ALTER DATABASE NOMBRE_DB SET SINGLE_USER WITH ROLLBACK IMMEDIATE
```

Ahora nos debería de dejar borrar la base de datos.

```sql
DROP DATABASE NOMBRE_DB
```
