# Citrix.WEM.SDK.Configuration.Database #

### Property Commandlets.BaseWemDatabaseCommand`1.SqlServerCredential

PSCredential for connecting to the SQL instance for database creation. Leave empty to use Windows Authentication for current user.





---
### Property Commandlets.BaseWemDatabaseCommand`1.WindowsAccount

Windows account granted access to WEM database.





---
### Property Commandlets.BaseWemDatabaseCommand`1.DatabaseServerInstance

SQL Server on which the database will be hosted. (serveraddress,port\instancename).





---
### Property Commandlets.BaseWemDatabaseCommand`1.DatabaseName

Name of the WEM database to create.





---
### Property Commandlets.BaseWemDatabaseCommand`1.PSDebugMode

Debug mode displays extra exception information. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
## Type Commandlets.NewWemDatabase

Creates a WEM database.

The New-WemDatabase cmdlet creates one Workspace Environment Management (WEM) database. The database is created on the SQL server.

#### Example: Create a database instance on the remote SQL DatabaseServerInstance (10.10.10.10). It uses SQL DatabaseServerInstance authentication for the initialization connection: 



#####  code

```powershell
    $passwd = ConvertTo-SecureString "[Password]" -AsPlainText -Force
    $sqlServerCred = New-Object System.Management.Automation.PSCredential("sa", $passwd);
    $DBname = "WEM_DB";
    $fileFolder = "C:\Program Files\Microsoft SQL DatabaseServerInstance\MSSQL11.MSSQLSERVER\MSSQL\DATA\";
    New-WemDatabase -DatabaseServerInstance "10.10.10.10" -DatabaseName $DBname -DataFilePath($fileFolder+$DBname+"_Data.mdf") -LogFilePath($fileFolder+$DBname+"_Log.ldf") -DefaultAdministratorsGroup "[Domain]\[GroupName]" -SqlServerCredential $sqlServerCred
```





#### Example: Create a database instance on the remote SQL DatabaseServerInstance(10.10.10.10). It uses Windows authentication for the initialization connection: 



#####  code

```powershell
    $DBname = "WEM_DB";
    $fileFolder = "C:\Program Files\Microsoft SQL DatabaseServerInstance\MSSQL11.MSSQLSERVER\MSSQL\DATA\";
    New-WemDatabase -DatabaseServerInstance "[Server\Instance]" -DatabaseName $DBname -DataFilePath($fileFolder+$DBname+"_Data.mdf") -LogFilePath($fileFolder+$DBname+"_Log.ldf") -DefaultAdministratorsGroup "[Domain]\[GroupName]"
```





#### Example: Create a database instance on the remote SQL DatabaseServerInstance(10.10.10.10). It uses Windows authentication for the initialization connection with adding extra database user via "WindowsAccount" attribute: 



#####  code

```powershell
    $DBname = "WEM_DB";
    $fileFolder = "C:\Program Files\Microsoft SQL DatabaseServerInstance\MSSQL11.MSSQLSERVER\MSSQL\DATA\";
    New-WemDatabase -DatabaseServerInstance "[Server\Instance]" -DatabaseName $DBname -DataFilePath($fileFolder+$DBname+"_Data.mdf") -LogFilePath($fileFolder+$DBname+"_Log.ldf") -DefaultAdministratorsGroup "[Domain]\[GroupName]" -WindowsAccount "[Domain]\[UserName]
```





#### Example: Creating new database instance on the remote SQL DatabaseServerInstance(10.10.10.10). It uses single configuration object for connecting to the server and configuring database: 



#####  code

```powershell
    $fileFolder = "C:\Program Files\Microsoft SQL DatabaseServerInstance\MSSQL11.MSSQLSERVER\MSSQL\DATA\";
    $DBname = "WEMDB_1_Obj";    
    $cfg = New-Object Citrix.WEM.SDK.Configuration.Database.SDKNewDatabaseConfiguration;
    $cfg.DatabaseServerInstance = "[Server\Instance]";
    $cfg.DatabaseName = $DBname;
    $cfg.DataFilePath = ($fileFolder+$DBname+"_Data.mdf");
    $cfg.LogFilePath =  ($fileFolder+$DBname+"_Log.ldf") ;
    $cfg.DefaultAdministratorsGroup = "[Domain]\[GroupName]";    
    $cfg.WindowsAccount = "[Domain]\[UserName]";
    New-WemDatabase -Configuration $cfg;
```





Update-WemDatabase





---
### Property Commandlets.NewWemDatabase.DataFilePath

Path to the .mdf file location on the SQL Server. You must provide a valid filepath, otherwise the cmdlet will fail. No default value is assumed.





---
### Property Commandlets.NewWemDatabase.LogFilePath

Path to the .ldf file location on the SQL Server. You must provide a valid filepath, otherwise the cmdlet will fail. No default value is assumed.





---
### Property Commandlets.NewWemDatabase.DefaultAdministratorsGroup

Default group of WEM administrators with Full Access to the administration console.





---
### Property Commandlets.NewWemDatabase.VuemUserSqlPassword

Specific password for the WEM vuemUser SQL user account. Leave empty to create a default password.





---
### Property Commandlets.NewWemDatabase.Configuration

Configuration set to save settings in.





---
## Type Commandlets.UpdateWemDatabase

Updates an existing WEM database.

The Update-WemDatabase cmdlet updates an existing Workspace Environment Management (WEM) database instance on the SQL server.

#### Example: Update an existing database to the latest version. Uses Windows authentication for the initialization connection: 



#####  code

```powershell
    Update-WemDatabase -DatabaseServerInstance "NK_SQL" -DatabaseName "WEM_DB"
```





#### Example: Update an existing database to the latest version. Uses SQL Server authentication for the initialization connection: 



#####  code

```powershell
    $password = ConvertTo-SecureString "[Password]" -AsPlainText -Force; 
    $sqlServerCred = New-Object System.Management.Automation.PSCredential("sa", $password);
    Update-WemDatabase -DatabaseServerInstance "NK_SQL" -DatabaseName "WEM_DB" -SqlServerCredential $sqlServerCred;
```





#### Example: Update an existing database to the latest version. Uses SQL Server authentication for the initialization connection and adds extra database user via "WindowsAccount" attribute: 



#####  code

```powershell
    $password = ConvertTo-SecureString "[Password]" -AsPlainText -Force; 
    $sqlServerCred = New-Object System.Management.Automation.PSCredential("sa", $password);
    Update-WemDatabase -DatabaseServerInstance "NK_SQL" -DatabaseName "WEM_DB" -SqlServerCredential $sqlServerCred -WindowsAccount "[Domain]\[UserName]";
```





#### Example: Update an existing database instance on the remote SQL Server (10.10.10.10). Uses a single configuration object for connecting to the server and for configuring the database: 



#####  code

```powershell
    $cfg_obj = New-Object Citrix.WEM.SDK.Configuration.Database.SDKDatabaseConfiguration
    $cfg_obj.DatabaseServerInstance = "10.10.10.10";
    $cfg_obj.DatabaseName = "WEM_DB";
    $cfg_obj.WindowsAccount = "[Domain]\[UserName]";
    Update-WemDatabase -Configuration $cfg_obj;
```





New-WemDatabase





---
### Property Commandlets.UpdateWemDatabase.Configuration

Configuration set.





---
## Type SDKDatabaseConfiguration

 SDK Database Configuration object. 



---
### Property SDKDatabaseConfiguration.SqlServerCredential

 PSCredential for connecting to the SQL instance for database creation. Leave empty to use Windows Authentication for current user. 



---
### Property SDKDatabaseConfiguration.WindowsAccount

 Windows account granted access to WEM database. 



---
### Property SDKDatabaseConfiguration.DatabaseServerInstance

 SQL Server on which the database will be hosted (serveraddress,port\instancename). 



---
### Property SDKDatabaseConfiguration.DatabaseName

 Name of the WEM database to create or update. 



---
## Type SDKNewDatabaseConfiguration

 SDK new database Configuration object. 



---
### Property SDKNewDatabaseConfiguration.DataFilePath

 Path to the .mdf file location on the SQL Server. You must provide a valid filepath, otherwise the cmdlet will fail. No default value is assumed. 



---
### Property SDKNewDatabaseConfiguration.LogFilePath

 Path to the .ldf file location on the SQL Server. You must provide a valid filepath, otherwise the cmdlet will fail. No default value is assumed. 



---
### Property SDKNewDatabaseConfiguration.DefaultAdministratorsGroup

 Default group of WEM administrators with Full Access to the Administration Console. 



---
### Property SDKNewDatabaseConfiguration.VuemUserSqlPassword

 Specific password for the WEM vuemUser SQL user account. Leave empty to create a default password. 



---


