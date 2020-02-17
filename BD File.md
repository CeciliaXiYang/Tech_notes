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
   Reference:  
   http://johnatten.com/2014/12/07/installing-and-using-sqlite-on-windows/#Getting-Started---Using-SQLite-on-Windows  
- Download the `sqlite3` (including sqlite.def, sqlite3.dll, sqlite3.exe, add the path to environment variables)  
- In command prompt, cd to the directory with .db file  
- Type commands  

   ```
   sqlite3
   .open DBNAME.db
   .tables
   select * from TABLENAME limit 10
   ```
- GUI-Based Tools: `sqlitebrowser`  

## Access and manipulate data  
- Create a table (by copying another table)  

   ```
   CREATE TABLE TABLENAME AS
   SELECT * FROM TABLETAMPLATE
   ```
- Delete all rows in a table  

   ```
   DELETE FROM TABLENAME
   ```

## Load a .bak file into the MySQL 
- .bak file is a backup of the data. It cannot be directly imported into the MySQL
- **Preparations:** 
   1) Intall the SQL Server and MySQL
   

- **Steps:**
   A detailed tutorial for the data migration from SQL Server to MySQL: 
   https://mysqlworkbench.org/2012/07/migrating-from-ms-sql-server-to-mysql-using-workbench-migration-wizard/ 
   
- **Important settings:** 
   1) Set up the as username and password in SQL Server
      - Secruity --> Logins --> Right click sa properties
      - Reset the password
      - Click Status tab： Set "Permission to connect to database engine" --> "Grant" and "Login" --> "Enabled"
      - Right click server properties: Set "Server authentication" --> "SQL Server and Windows Authentication mode" and "Login auditing" --> "Successful logins only"
   
   2) In SQL Server Configuration manager 
      - In "SQL Server Network Configuration" --> "protocols for MSSQLSERVER", set TCP/IP as enabled
      - Right Click the TCP/IP properties --> Check the IP address, the TCP port in IPAll is set as '1433'
      - In "SQL Server Services", ensure the instances have the running state
   
   3) Firewall settings: allow SQL server to communicate through windows defender firewall
      - Open windows defender firewall, add "C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Binn\sqlservr.exe"
   
   4) Restart the SQL Server using services.msc
   
   5) Fix the error "SQL Server does not exist or access denied Fixed" --> Create alias on client side
      Reason: The server name has not been set up as the alias for the IP address
      - Search for 'cliconfg.exe'
      - Create TCP/IP alias --> Enable the TCP/IP and make sure there is no Named Piped in the list (right side)
      - Click Alias tab, fill in server alias, choose TCP/IP Network libraries, and fill in SQL Server IP in Server name
      - Now the remote server can be connected by server name
      
- **Q&A when setting up DB on server: **
   1) Q: How to fix phpMyAdmin 403 forbidden error?  
      A: Update the access permission of the file etc/httpd/conf.d/phpMyAdmin.conf: 
         `sudo chmod -R 755 phpMyAdmin.conf` 
         Besides, `sudo vim phpMyAdmin.conf` and update the content 
         ```
         <IfModule mod_authz_core.c>
           # Apache 2.4
           <RequireAny>
             Require all granted
           </RequireAny>
         </IfModule>
         <IfModule !mod_authz_core.c>
           # Apache 2.2
           Order Allow,Deny
           Allow from localhost all
           Require all granted
         </IfModule> 
         ``` 
         Reference: https://bobcares.com/blog/phpmyadmin-403-forbidden-error/ 
         
   2) Q: How to access the DB on server via localhost? 
      A: Use the xampp app. If the Port 3306 in use by "Unable to open process", open the terminal: 
         step 1: `sc delete mysql` to terminate the running service 
         step 2: close the xampp control pannel and restart it
         step 3: click config, a my.ini file will be open. Replace the port 3306 to 3307 
         step 4: open the xampp control panel config, click Service and Port Settings and change the port to 3307 
         The web server now can be accessed by: http://localhost/phpmyadmin/ 
         
         Reference: https://www.youtube.com/watch?v=gVWVTsTPxRk 
         
   3) 
         
         
         
      
      
