# Citrix.WEM.SDK.Configuration.Database #

#### Property Commandlets.BaseWemDatabaseCommand`1.SqlServerCredential

PSCredential for connecting to the SQL instance for database creation. Leave empty to use Windows Authentication for current user.





---
#### Property Commandlets.BaseWemDatabaseCommand`1.DatabaseServerInstance

SQL Server on which the database will be hosted. (serveraddress,port\instancename).





---
#### Property Commandlets.BaseWemDatabaseCommand`1.DatabaseName

Name of the WEM database to create.





---
#### Property Commandlets.BaseWemDatabaseCommand`1.PSDebugMode

Debug mode displays extra exception information. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
## Type Commandlets.NewWemDatabase

Create a WEM database.

The New-WemDatabase cmdlet creates one Workspace Environment Management (WEM) database. The database is created on the SQL Server.

##### Example: 

######  code

```
    $passwd = ConvertTo-SecureString "[Password]" -AsPlainText -Force
    $sqlServerCred = New-Object System.Management.Automation.PSCredential("sa", $passwd);
    $DBname = "WEM_DB";
    New-WemDatabase -DatabaseServerInstance "10.10.10.10" -DatabaseName $DBname -DefaultAdministratorsGroup "[Domain]\[GroupName]" -SqlServerCredential $sqlServerCred
```

Create a database instance on the remote SQL Server (10.10.10.10) by using SQL Server authentication.







##### Example: 

######  code

```
    $DBname = "WEM_DB";
    $fileFolder = "C:\Program Files\Microsoft SQL DatabaseServerInstance\MSSQL11.MSSQLSERVER\MSSQL\DATA\";
    New-WemDatabase -DatabaseServerInstance "[Server\Instance]" -DatabaseName $DBname -DataFilePath($fileFolder+$DBname+"_Data.mdf") -LogFilePath($fileFolder+$DBname+"_Log.ldf") -DefaultAdministratorsGroup "[Domain]\[GroupName]"
```

Create a database instance on the remote SQL Server (10.10.10.10) by usingWindows authentication.







##### Example: 

######  code

```
    $DBname = "WEM_DB";
    $fileFolder = "C:\Program Files\Microsoft SQL DatabaseServerInstance\MSSQL11.MSSQLSERVER\MSSQL\DATA\";
    New-WemDatabase -DatabaseServerInstance "[Server\Instance]" -DatabaseName $DBname -DataFilePath($fileFolder+$DBname+"_Data.mdf") -LogFilePath($fileFolder+$DBname+"_Log.ldf") -DefaultAdministratorsGroup "[Domain]\[GroupName]" -WindowsAccount "[Domain]\[UserName]
```

Create a database instance on the remote SQL Server (10.10.10.10) by using Windows authentication. You can add extra database users by using the "WindowsAccount" attribute.







##### Example: 

######  code

```
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

Create a new database instance on the remote SQL Server (10.10.10.10) by using a single configuration object to connect to the server and to configure the database.







Update-WemDatabase





---
#### Property Commandlets.NewWemDatabase.WindowsAccount

Windows account granted access to WEM database.





---
#### Property Commandlets.NewWemDatabase.DataFilePath

Path to the .mdf file location on the SQL Server. Leave empty to auto-populate the Data file field with the correct path of the SQL being used. If auto-population fails, the path of the SQL Server 2008 R2 is used by default.





---
#### Property Commandlets.NewWemDatabase.LogFilePath

Path to the .ldf file location on the SQL Server. Leave empty to auto-populate the Log file field with the correct path of the SQL being used. If auto-population fails, the path of the SQL Server 2008 R2 is used by default.





---
#### Property Commandlets.NewWemDatabase.DefaultAdministratorsGroup

Default group of WEM administrators with Full Access to the administration console.





---
#### Property Commandlets.NewWemDatabase.VuemUserSqlPassword

Specific password for the WEM vuemUser SQL user account. Leave empty to create a default password.





---
#### Property Commandlets.NewWemDatabase.CommandTimeout

Timeout period for connection attempts to the WEM database. After this time an error message is displayed. Leave empty to use default timeout of 300 seconds.





---
#### Property Commandlets.NewWemDatabase.Configuration

Configuration set to save settings in.





---
## Type Commandlets.NewWemDatabaseOnCloud

Create a WEM database on Cloud.

The New-WemDatabaseOnCloud cmdlet creates one Workspace Environment Management (WEM) database. The database is created on the SQL server.

##### Example: 

######  code

```
    $passwd = ConvertTo-SecureString "[Password]" -AsPlainText -Force
    $sqlServerCred = New-Object System.Management.Automation.PSCredential("sa", $passwd);
    $DBname = "WEM_DB";
    $elasticPool = "elasticPoolName";
    New-WemDatabase -DatabaseServerInstance "10.111.12.145" -DatabaseName $DBname -SqlServerCredential $sqlServerCred -ElasticPool $elasticPool
```

Create a new database instance on the remote SQL Server (10.111.12.145) by using SQL Server authentication.







##### Example: 

######  code

```
    $elasticPool = "elasticPoolName";
    $DBname = "WEMDB_1_Obj";    
    $sqlServerCred = New-Object System.Management.Automation.PSCredential("name", $passwd);
    $cfg = New-Object Citrix.WEM.SDK.Configuration.Database.SDKNewDatabaseConfigurationOnCloud;
    $cfg.DatabaseServerInstance = "[Server\Instance]";
    $cfg.SqlServerCredential = $$sqlServerCred;
    $cfg.DatabaseName = $DBname;   
    $cfg.ElasticPool = $elasticPool;
    
    New-WemDatabaseOnCloud -Configuration $cfg;
```

Create a new database instance on the remote SQL Server (10.111.12.145) by using a single configuration object to connect to the server and to configure the database.











---
#### Property Commandlets.NewWemDatabaseOnCloud.ElasticPool

Elastic Pool of the WEM database to create.





---
#### Property Commandlets.NewWemDatabaseOnCloud.VuemUserSqlPassword

Specific password for the WEM vuemUser SQL user account. Leave empty to create a default password.





---
#### Property Commandlets.NewWemDatabaseOnCloud.Configuration

Configuration set save settings in.





---
## Type Commandlets.UpdateWemDatabase

Update an existing WEM database.

The Update-WemDatabase cmdlet updates an existing Workspace Environment Management (WEM) database instance on the SQL server.

##### Example: 

######  code

```
Update-WemDatabase -DatabaseServerInstance "NK_SQL" -DatabaseName "WEM_DB"
```

Update an existing database to the latest version by using Windows authentication.







##### Example: 

######  code

```
    $password = ConvertTo-SecureString "[Password]" -AsPlainText -Force; 
    $sqlServerCred = New-Object System.Management.Automation.PSCredential("sa", $password);
    Update-WemDatabase -DatabaseServerInstance "NK_SQL" -DatabaseName "WEM_DB" -SqlServerCredential $sqlServerCred;
```

Update an existing database to the latest version by using SQL Server authentication.







##### Example: 

######  code

```
    $password = ConvertTo-SecureString "[Password]" -AsPlainText -Force; 
    $sqlServerCred = New-Object System.Management.Automation.PSCredential("sa", $password);
    Update-WemDatabase -DatabaseServerInstance "NK_SQL" -DatabaseName "WEM_DB" -SqlServerCredential $sqlServerCred -WindowsAccount "[Domain]\[UserName]";
```

Update an existing database to the latest version by using SQL Server authentication. You can add extra database users by using the "WindowsAccount" attribute.







##### Example: 

######  code

```
    $cfg_obj = New-Object Citrix.WEM.SDK.Configuration.Database.SDKDatabaseConfiguration
    $cfg_obj.DatabaseServerInstance = "10.10.10.10";
    $cfg_obj.DatabaseName = "WEM_DB";
    $cfg_obj.WindowsAccount = "[Domain]\[UserName]";
    Update-WemDatabase -Configuration $cfg_obj;
```

Update an existing database instance on the remote SQL Server (10.10.10.10) by using a single configuration object to connect to the server and to configure the database.







New-WemDatabase





---
#### Property Commandlets.UpdateWemDatabase.WindowsAccount

Windows account granted access to WEM database.





---
#### Property Commandlets.UpdateWemDatabase.Configuration

Configuration set.





---
## Type SDKDatabaseConfiguration

 SDK Database Configuration object. 



---
#### Property SDKDatabaseConfiguration.SqlServerCredential

 PSCredential for connecting to the SQL instance for database creation. Leave empty to use Windows Authentication for current user. 



---
#### Property SDKDatabaseConfiguration.DatabaseServerInstance

 SQL Server on which the database will be hosted (serveraddress,port\instancename). 



---
#### Property SDKDatabaseConfiguration.DatabaseName

 Name of the WEM database to create or update. 



---
## Type SDKNewDatabaseConfiguration

 SDK new database Configuration object. 



---
#### Property SDKNewDatabaseConfiguration.WindowsAccount

 Windows account granted access to WEM database. 



---
#### Property SDKNewDatabaseConfiguration.DataFilePath

 Path to the .mdf file location on the SQL Server. Leave empty to auto-populate the Data file field with the correct path of the SQL being used. If auto-population fails, the path of the SQL Server 2008 R2 is used by default. 



---
#### Property SDKNewDatabaseConfiguration.LogFilePath

 Path to the .ldf file location on the SQL Server. Leave empty to auto-populate the Log file field with the correct path of the SQL being used. If auto-population fails, the path of the SQL Server 2008 R2 is used by default. 



---
#### Property SDKNewDatabaseConfiguration.DefaultAdministratorsGroup

 Default group of WEM administrators with Full Access to the Administration Console. 



---
#### Property SDKNewDatabaseConfiguration.VuemUserSqlPassword

 Specific password for the WEM vuemUser SQL user account. Leave empty to create a default password. 



---
#### Property SDKNewDatabaseConfiguration.CommandTimeout

 Timeout period for connection attempts to the WEM database. After this time an error message is displayed. Leave empty to use default timeout of 300 seconds. 



---
## Type SDKNewDatabaseConfigurationOnCloud

 Configuration new database class 



---
#### Property SDKNewDatabaseConfigurationOnCloud.VuemUserSqlPassword

 Specific password for the WEM vuemUser SQL user account. Leave empty to create a default password. 



---
#### Property SDKNewDatabaseConfigurationOnCloud.ElasticPool

 ELASTIC POOL of the WEM database to join. 



---
## Type SDKUpdateDatabaseConfiguration

 Configuration update database class 



---
#### Property SDKUpdateDatabaseConfiguration.WindowsAccount

 Windows account granted access to WEM database. 



---


