## Import .csv data to Heidi:  
- Open the .csv file in UE  
- Convert to hexadecimal display: Control + H  
- Convert empty fileds to '\N'  
   ```
   Control + R (replace)
   2C 2C --> 2C 5C 4E 2C, e.g. ,, --> ,\N,
   2C 0D 0A --> 2C 5C 4E 0D 0A, e.g. ,\r\n --> ,\N\r\n
   ```
- Import .csv file, with lines terminated by \r\n  

## Open a .db file  
   Reference: http://johnatten.com/2014/12/07/installing-and-using-sqlite-on-windows/#Getting-Started---Using-SQLite-on-Windows  
- Download the sqlite3 (including sqlite.def, sqlite3.dll, sqlite3.exe, add the path to environment variables)  
- In command prompt, cd to the directory with .db file  
- Type commands:  
   ```
   sqlite3
   .open DBNAME.db
   .tables
   select * from TABLENAME limit 10
   ```
- GUI-Based Tools: sqlitebrowser  

## Access and manipulate data  
- Create a table (by copying another table)  
   ```
   CREATE TABLE TABLENAME AS
   SELECT * FROM TABLETAMPLATE
   ```
- Delete all rows in a table  
   ```
   DELETE FROM TABLENAME;
   ```