# Citrix.WEM.SDK.Configuration.InfrastructureService #

#### Property Commandlets.BaseInfrastructureServiceConfigurationCommand.InfrastructureServer

Remote infrastructure service machine name or IP address.





---
#### Property Commandlets.BaseInfrastructureServiceConfigurationCommand.InfrastructureServerCredential

PSCredential that will be used on the remote machine for getting data.





---
#### Property Commandlets.BaseInfrastructureServiceConfigurationCommand.PSDebugMode

Enable verbose logging of the infrastructure service. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
## Type Commandlets.GetWemInfrastructureServiceConfiguration

Gets the current infrastructure service configuration.

 The Get-WemInfrastructureServiceConfiguration cmdlet gets the current infrastructure service configuration from the local or remote infrastructure server machine. Remote machines can be either in the same domain, or can be in a multi-forest domain environment. 

 --To return the current configuration on the local infrastructure server, run the cmdlet without the InfrastructureServer parameter and without the InfrastructureServerCredential parameter. All the following parameter values are applied. 

 --To return the current configuration from a remote server in the same domain, you must specify the InfrastructureServer parameter. 

 --To return the current configuration from a remote server in a multi forest Active Directory environment, you must specify the InfrastructureServer parameter (to identify the target machine) and the InfrastructureServerCredential parameter(to provide access credentials). 

##### Example: Get the current configuration of the infrastructure service from the local machine: 



######  code

```
    Get-WemInfrastructureServiceConfiguration
```





##### Example: Get the current configuration of the Infrastructure service from the remote machine in the same domain by using Windows authentication: 





######  code

```
    Get-WemInfrastructureServiceConfiguration –InfrastructureServer “[Server]”
```





##### Example: Get the current configuration of the infrastructure service from a remote machine in a multi-forest trusted environment. For authentication, this cmdlet uses the PSCredential type object: 



######  code

```
    $passwd = ConvertTo-SecureString "[Password]" -AsPlainText -Force; 
    $cred = New-Object System.Management.Automation.PSCredential ("[Domain\UserName]", $passwd)
    Get-WemInfrastructureServiceConfiguration –InfrastructureServer “[Server]” –InfrastructureServiceAccountCredentials $cred
```





Set-WemInfrastructureServiceConfiguration





---
## Type Commandlets.SetWemInfrastructureServiceConfiguration

 Sets the infrastructure service configuration on a local or remote infrastructure server machine.

 The Set-WemInfrastructureServiceConfiguration cmdlet sets the infrastructure service configuration on a local or remote infrastructure server machine. Remote machines can be either in the same domain, or can be in a multi-forest domain environment. You can set the full configuration, or a subset of it. 

 --To return the current configuration on the local infrastructure server, run the cmdlet without the InfrastructureServer parameter and without the InfrastructureServerCredential parameter. All the following parameter values are applied. 

 --To set the current configuration to a remote server in the same domain, you must specify the InfrastructureServer parameter. 

 --To set the current configuration to a remote server in a multi forest Active Directory environment, you must specify the InfrastructureServer parameter (to identify the target machine) and the InfrastructureServerCredential parameter(to provide access credentials). 

##### Example: Set one single configuration option (DatabaseName) on the local machine: 



######  code

```
    Set-WemInfrastructureServiceConfiguration -DatabaseName "WEM_DB";
```





##### Example: Set multiple configuration options (DatabaseName, MonitoringPort and EnableDebug) on the local machine:



######  code

```
    $Enable = [Norskale.Utilities.Common.SwitchState]::Enable;
    Set-WemInfrastructureServiceConfiguration -DatabaseName "WEM_DB" -MonitoringPort 8084 -DebugMode $Enable;
```





##### Example: Set multiple configuration options (DatabaseName, MonitoringPort and EnableDebug) on the remote machine in the same domain (Windows authentication):



######  code

```
    $Enable = [Norskale.Utilities.Common.SwitchState]::Enable;
    Set-WemInfrastructureServiceConfiguration -InfrastructureServer "[Server]" -DatabaseName "WEM_DB" -MonitoringPort 8084 -DebugMode $Enable;
```





##### Example: Set multiple configuration options (DatabaseName, MonitoringPort) on the remote machine (in multi-forest trust domain environments):



######  code

```
    $passwd = ConvertTo-SecureString "[Password]" -AsPlainText -Force; 
    $cred = New-Object System.Management.Automation.PSCredential("[Domain]\[UserName]", $passwd);
    Set-WemInfrastructureServiceConfiguration -InfrastructureServer "[Server]" -InfrastructureServiceAccountCredential $cred -DatabaseName "WEM_DB" -MonitoringPort 8084;
```





##### Example: Configure the infrastructure service via one configuration object. This approach also can be provided for configuring local and remote machine (in the same domain or in multi-forest trust domain environments): 



######  code

```
    $Enable = [Norskale.Utilities.Common.SwitchState]::Enable;
    $Disable = [Norskale.Utilities.Common.SwitchState]::Disable;
    $config = New-Object Citrix.WEM.SDK.Configuration.InfrastructureService.SDKInfrastructureServiceConfiguration
    $config.DatabaseServerInstance = "SQLServer_machine";                   
    $config.DatabaseName = "WEM_DB";
    $config.AdminServicePort = 8284;
    $config.DebugMode = $Disable;
    $config.SendGoogleAnalytics = $Enable
    ...
    Set-WemInfrastructureServiceConfiguration -Configuration $config
```



 Warning! If you use single configuration object you have to keep in mind that you must configure all required properties in the configuration object. Other ways infrastructure service will be configured by default empty values. 



Get-WemInfrastructureServiceConfiguration





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.DebugMode

Enable WEM debug mode. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.SendGoogleAnalytics

Enable collection of statistics. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.UseCacheEvenIfOnline

Enable infrastructure service to always reading site settings from its cache. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.DatabaseServerInstance

SQL Server instance on which the WEM database is hosted. (serveraddress,port\instancename).





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.DatabaseName

WEM database name.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.DatabaseFailoverServerInstance

Database failover server instance.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.SetSqlUserSpecificPassword

Allow vuemUser SQL user account password to be set. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.SqlUserSpecificPassword

vuemUser SQL user account password.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.AdminServicePort

Administration port for administration console to connect to the infrastructure service.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.AgentServicePort

Agent service port for agent to connect to the infrastructure server.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.AgentSyncPort

Cache synchronization port for agent cache synchronization process to connect to the infrastructure service.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.MonitoringPort

WEM monitoring port.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.InfrastructureServiceAccountCredential

PSCredential for running the infrastructure service.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.EnableInfrastructureServiceAccountCredential

Use Windows authentication for infrastructure service database connection. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.CacheRefreshDelay

Time (in minutes) before the infrastructure service refreshes its cache.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.SQLCheckDelay

Time (in seconds) between each infrastructure service attempt to poll the SQL server. 





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.InfrastructureServiceSQLConnectionTimeout

Time (in seconds) which the infrastructure service waits when trying to establish a connection with the SQL server.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.EnableScheduledMaintenance

Enable deletion of old statistics records from the database at periodic intervals. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.StatisticsRetentionPeriod

Retention period for user and agent statistics (in days).





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.SystemMonitoringRetentionPeriod

Retention period for system optimization statistics (in days).





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.AgentRegistrationsRetentionPeriod

Retention period for agent registration logs (in days).





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.DatabaseMaintenanceExecutionTime

The time at which the database maintenance action is performed (HH:MM).





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.GlobalLicenseServerOverride

Override any Citrix License Server information already in the WEM database. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.LicenseServerName

Citrix License Server name.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.LicenseServerPort

Citrix License Server port.





---
#### Property Commandlets.SetWemInfrastructureServiceConfiguration.Configuration

Configuration set to save the settings in.





---
## Type SDKInfrastructureServiceConfiguration

SDK Infrastructure service Configuration object.





---
#### Property SDKInfrastructureServiceConfiguration.DebugMode

 Enable WEM debug mode. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter. 



---
#### Property SDKInfrastructureServiceConfiguration.SendGoogleAnalytics

Enable collection of statistics. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property SDKInfrastructureServiceConfiguration.UseCacheEvenIfOnline

Enable infrastructure service to always reading site settings from its cache. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property SDKInfrastructureServiceConfiguration.DatabaseServerInstance

SQL Server instance on which the WEM database is hosted. (serveraddress,port\instancename).





---
#### Property SDKInfrastructureServiceConfiguration.DatabaseName

WEM database name.





---
#### Property SDKInfrastructureServiceConfiguration.DatabaseFailoverServerInstance

Database failover server instance.





---
#### Property SDKInfrastructureServiceConfiguration.SetSqlUserSpecificPassword

Allow vuemUser SQL user account password to be set. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property SDKInfrastructureServiceConfiguration.SqlUserSpecificPassword

vuemUser SQL user account password.





---
#### Property SDKInfrastructureServiceConfiguration.AdminServicePort

Administration port for administration console to connect to the infrastructure service.





---
#### Property SDKInfrastructureServiceConfiguration.AgentServicePort

Agent service port for agent to connect to the infrastructure server.





---
#### Property SDKInfrastructureServiceConfiguration.AgentSyncPort

Cache synchronization port for agent cache synchronization process to connect to the infrastructure service.





---
#### Property SDKInfrastructureServiceConfiguration.MonitoringPort

WEM monitoring port.





---
#### Property SDKInfrastructureServiceConfiguration.InfrastructureServiceAccountCredentialLogin

Login for running the infrastructure service.





---
#### Property SDKInfrastructureServiceConfiguration.InfrastructureServiceAccountCredentialPassword

Password for running the infrastructure service.





---
#### Property SDKInfrastructureServiceConfiguration.EnableInfrastructureServiceAccountCredential

Use Windows authentication for infrastructure service database connection. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property SDKInfrastructureServiceConfiguration.CacheRefreshDelay

Time (in minutes) before the infrastructure service refreshes its cache.





---
#### Property SDKInfrastructureServiceConfiguration.SqlCheckDelay

Time (in seconds) between each infrastructure service attempt to poll the SQL server. 





---
#### Property SDKInfrastructureServiceConfiguration.InfrastructureServiceSQLConnectionTimeout

Time (in seconds) which the infrastructure service waits when trying to establish a connection with the SQL server.





---
#### Property SDKInfrastructureServiceConfiguration.EnableScheduledMaintenance

Enable deletion of old statistics records from the database at periodic intervals. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property SDKInfrastructureServiceConfiguration.StatisticsRetentionPeriod

Retention period for user and agent statistics (in days).





---
#### Property SDKInfrastructureServiceConfiguration.SystemMonitoringRetentionPeriod

Retention period for system optimization statistics (in days).





---
#### Property SDKInfrastructureServiceConfiguration.AgentRegistrationsRetentionPeriod

Retention period for agent registration logs (in days).





---
#### Property SDKInfrastructureServiceConfiguration.DatabaseMaintenanceExecutionTime

The time at which the database maintenance action is performed (HH:MM).





---
#### Property SDKInfrastructureServiceConfiguration.GlobalLicenseServerOverride

Override any Citrix License Server information already in the WEM database. Specify 'None' to leave the current value unchanged. This is equivalent to omitting this parameter.





---
#### Property SDKInfrastructureServiceConfiguration.LicenseServerName

Citrix License Server name.





---
#### Property SDKInfrastructureServiceConfiguration.LicenseServerPort

Citrix License Server port.





---


