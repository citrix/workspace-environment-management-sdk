# Citrix.WEM.SDK.Configuration.Client #

#### Property BaseCmdlet.PSDebugMode

Determines whether to display debugging information. Default value is False.





---
#### Property BaseCmdlet.InfrastructureServer

The infrastructure server host name or IP address. Default value is "localhost".





---
#### Property BaseCmdlet.Port

The port used to connect to the infrastructure service. Default value is 8284.





---
## Type ExportAdObject

Exports all AD objects in a specified configuration set.

 The Export-AdObject cmdlet exports all AD objects (user-level and machine-level) in a specified configuration set. 

##### Example: 

######  code

```
    Export-AdObject -InfrastructureServer "10.10.10.10" -FolderName "C:\backup" -SiteId 3
```

Exports all AD objects in the configuration set whose ID is 3 to the folder "C:\backup". The IP address of the remote infrastructure server is “10.10.10.10”.







##### Example: 

######  code

```
    Export-AdObject -FolderName "C:\backup" -SiteName "Default Site"
```

Exports all AD objects (on the local infrastructure server) in "Default Site" to the folder "C:\backup".











---
#### Property ExportAdObject.FolderName

 The name of the folder to which all AD objects are exported. Note: The folder is created automatically if it does not exist. 





---
#### Property ExportAdObject.SiteName

 The name of the configuration set whose AD objects are to be exported. Note: This parameter does not work if the parameter "SiteId" is specified. 





---
#### Property ExportAdObject.SiteId

 The ID of the configuration set whose AD objects are to be exported. 





---
## Type ExportSite

Exports a specified configuration set.

 The Export-WemSite cmdlet exports a WEM configuration set. 

##### Example: 

######  code

```
    Export-WemSite -InfrastructureServer "10.10.10.10" -FolderName "C:\backup-site" -SiteId 3
```

Exports the configuration set whose ID is 3 to the folder "C:\backup-site". The IP address of the remote infrastructure server is "10.10.10.10".







##### Example: 

######  code

```
    Export-WemSite -FolderName "C:\backup-site" -SiteName "Default Site"
```

Exports "Default Site" (on the local infrastructure server) to the folder "C:\backup-site".











---
#### Property ExportSite.FolderName

 The name of the folder to which the configuration set is exported. Note: The folder is created automatically if it does not exist. 





---
#### Property ExportSite.SiteName

 The name of the configuration set to be exported. Note: This parameter does not work if the parameter "SiteId" is specified. 





---
#### Property ExportSite.SiteId

 The ID of the configuration set to be exported. 





---
## Type ImportAdObject

Imports all AD objects to a specified configuration set.

 The Import-AdObject cmdlet imports all AD objects (user-level and machine-level) to a specified configuration set. 

##### Example: 

######  code

```
    Import-AdObject -InfrastructureServer "10.10.10.10" -FolderName "C:\backup" -SiteId 3
```

Imports all AD objects from the folder "C:\backup" to the configuration set whose ID is 3. The IP address of the remote infrastructure server is "10.10.10.10".







##### Example: 

######  code

```
    Import-AdObject -FolderName "C:\backup" -SiteName "Default Site"
```

Imports AD objects from the folder "C:\backup" to "Default Site". By default, this operation is performed on the local infrastructure server unless otherwise specified.











---
#### Property ImportAdObject.FolderName

 The name of the folder from which AD objects are to be imported. 





---
#### Property ImportAdObject.SiteName

 The name of the configuration set to which AD objects are to be imported. Note: This parameter does not work if the parameter "SiteId" is specified. 





---
#### Property ImportAdObject.SiteId

 The ID of the configuration set to which AD objects are to be imported. 





---
## Type ImportSite

Imports a WEM configuration set.

 The Import-WemSite cmdlet imports a WEM configuration set from a folder. 

##### Example: 

######  code

```
    Import-WemSite -InfrastructureServer "10.10.10.10" -FolderName "C:\backup-site"
```

Imports a WEM configuration set from the folder "C:\backup-site". The IP address of the remote infrastructure server is "10.10.10.10".











---
#### Property ImportSite.FolderName

 The name of the folder from which the configuration set is to be imported. 





---
## Type CreateMachineAdObject

Creates a machine-level AD object.

The New-MachineAdObject cmdlet creates a machine-level AD object.

##### Example: 

######  code

```
    $Machine = New-Object Citrix.DeviceMgmt.Agent.Windows.Sdk.MachineModel
    $Machine.Name = "CN=YourComputerName,CN=Computers,DC=domain,DC=local"
    $Machine.Type = "Computer"
    $Machine.Enabled = $True
    $Machine.Priority = 100
    New-MachineAdObject -InfrastructureServer "10.10.10.10" -MachineAdObject $Machine
```

Creates a computer named "YourComputerName" with a priority of 100. The IP address of the remote infrastructure server is "10.10.10.10".







##### Example: 

######  code

```
    $Machine = New-Object Citrix.DeviceMgmt.Agent.Windows.Sdk.MachineModel
    $Machine.Name = "OU=YourOUName,DC=domain,DC=local"
    $Machine.Type = "OU"
    $Machine.Enabled = $False
    $Machine.Priority = 80
    New-MachineAdObject -MachineAdObject $Machine
```

Creates a disabled OU named "YourOUName" with a priority of 80 on the local infrastructure server.











---
#### Property CreateMachineAdObject.MachineAdObject

 The machine-level AD object to be created. Note: Use "distinguished name" or "SID" to specify this machine-level AD object. You do not need to specify the "Id" property when creating this object because the ID is generated automatically.





---
## Type DeleteMachineAdObject

Deletes a machine-level AD object.

The Remove-MachineAdObject cmdlet deletes a machine-level AD object.

##### Example: 

######  code

```
    Remove-MachineAdObject -InfrastructureServer "10.10.10.10" -Id 3
```

Deletes a machine-level AD object whose ID is 3. The IP address of the remote infrastructure server is "10.10.10.10".







##### Example: 

######  code

```
    $Machine = (Get-MachineAdObject) | Where-Object { $_.Name.ToLower().Contains("cn=your-computer-name,") })
    Remove-MachineAdObject -MachineAdObject $Machine.Id
```

Deletes a computer named "your-computer-name" on the local infrastructure server.











---
#### Property DeleteMachineAdObject.Id

 The ID of the machine-level AD object to be deleted. 





---
## Type GetMachineAdObject

Queries machine-level AD objects.

The Get-MachineAdObject cmdlet queries machine-level AD objects.

##### Example: 

######  code

```
    Get-MachineAdObject -InfrastructureServer "10.10.10.10"
```

Queries all machine-level AD objects. The IP address of the remote infrastructure server is "10.10.10.10".







##### Example: 

######  code

```
    Get-MachineAdObject -SiteName "Default Site"
```

Queries all machine-level AD objects in "Default Site" on the local infrastructure server.







##### Example: 

######  code

```
    Get-MachineAdObject -Id 10
```

Queries the machine-level AD object whose ID is 10 on the local infrastructure server.







##### Example: 

######  code

```
    Get-MachineAdObject -Sid "S-1-5-21-1375803180"
```

Queries the machine-level AD object whose SID is "S-1-5-21-1375803180" on the local infrastructure server.











---
#### Property GetMachineAdObject.SiteName

 The name of the configuration set that is used to filter machine-level AD objects. Only the AD objects that belong to this configuration set are to be displayed. If this parameter is not specified, the filtering operation does not work. Note: This parameter does not work if the parameter "SiteId" is specified. 





---
#### Property GetMachineAdObject.SiteId

 The ID of the configuration set that is used to filter machine-level AD objects. Only the AD objects that belong to this configuration set are to be displayed. If this parameter is not specified, the filtering operation does not work. 





---
#### Property GetMachineAdObject.Id

 If this parameter is specified, only the machine-level AD object with the specified ID is to be displayed. 





---
#### Property GetMachineAdObject.Sid

 If this parameter is specified, only the machine-level AD object with the specified SID is to be displayed. 





---
## Type UpdateMachineAdObject

Updates a machine-level AD object.

The Update-MachineAdObject cmdlet updates a machine-level AD object.

##### Example: 

######  code

```
    $Machine = (Get-MachineAdObject -InfrastructureServer "10.10.10.10") | Where-Object { $_.Name.ToLower().Contains("cn=your-computer-name,") }
    $Machine.Enable = $False
    $Machine.Priority += 10
    $Machine.Description = "Modify the description"
    Update-MachineAdObject -InfrastructureServer "10.10.10.10" -MachineAdObject $Machine
```

 Updates a machine whose name is "your-computer-name". The IP address of the remote infrastructure server is “10.10.10.10”. These commands disable the machine status, change the description, and increase the priority by 10. 











---
#### Property UpdateMachineAdObject.MachineAdObject

 The machine-level AD object to be updated. Note: This cmdlet updates the machine-level AD object according to the property "Id". The properties "Sid", "Name", and "Type" are read-only, and they remain unchanged even if you specify values for them. 





---
## Type CreateSite

Creates a configuration set.

The New-WemSite cmdlet creates a WEM configuration set.

##### Example: 

######  code

```
    $Site = New-Object Citrix.DeviceMgmt.Agent.Windows.Sdk.SiteModel
    $Site.Name = "New Configuration Set"
    $Site.Description = "This is a new configuration set created by Powershell SDK"
    New-WemSite -InfrastructureServer "10.10.10.10" -Site $Site
```

Creates a new configuration set named "New Configuration Set". The IP address of the remote infrastructure server is "10.10.10.10".











---
#### Property CreateSite.Site

 The configuration set to be created. Note: You do not need to specify the "Id" property when creating this object because the ID is generated automatically. 





---
## Type DeleteSite

Deletes a configuration set.

The Remove-WemSite cmdlet deletes a WEM configuration set.

##### Example: 

######  code

```
    Remove-WemSite -InfrastructureServer "10.10.10.10" -Id 12
```

Deletes a configuration set whose ID is 12. The IP address of the remote infrastructure server is "10.10.10.10".







##### Example: 

######  code

```
    Remove-WemSite -SiteName "New Configuration Set"
```

 Deletes a configuration set whose name is "New Configuration Set". By default, this operation is performed on the local infrastructure server unless otherwise specified. 











---
#### Property DeleteSite.SiteId

 The ID of the configuration set to be deleted. Note: You cannot delete the built-in configuration set named "Default Site". 





---
#### Property DeleteSite.SiteName

 The name of the configuration set to be deleted. Note: This parameter does not work if the parameter "SiteId" is specified. You cannot delete the built-in configuration set named "Default Site". 





---
## Type GetSite

Queries WEM configuration sets.

The Get-WemSite cmdlet queries WEM configuration sets.

##### Example: 

######  code

```
    Get-WemSite -InfrastructureServer "10.10.10.10"
```

Queries all WEM configuration sets. The IP address of the remote infrastructure server is "10.10.10.10".







##### Example: 

######  code

```
    Get-WemSite -SiteName "Default Site"
```

 Queries the configuration set whose name is "Default Site". By default, this operation is performed on the local infrastructure server unless otherwise specified. 







##### Example: 

######  code

```
    Get-WemSite -SiteId 2
```

Queries the configuration set whose ID is 2 on the local infrastructure server.











---
#### Property GetSite.SiteName

 The name of the configuration set to be queried. All configuration sets are to be displayed if this parameter is not specified. Note: This parameter does not work if the parameter "SiteId" is specified. 





---
#### Property GetSite.SiteId

 The ID of the configuration set to be queried. All configuration sets are to be displayed if this parameter is not specified. 





---
## Type UpdateSite

Updates a WEM configuration set.

The Update-WemSite cmdlet updates a WEM configuration set.

##### Example: 

######  code

```
    $Site = Get-WemSite -InfrastructureServer "10.10.10.10" -SiteName "Default Site"
    $Site.Name = "New Name"
    $Site.Description = "Modify the description"
    Update-WemSite -InfrastructureServer "10.10.10.10" -Site $Site
```

 Updates the name and description of "Default Site". The IP address of the remote infrastructure server is "10.10.10.10". 











---
#### Property UpdateSite.Site

 The configuration set to be updated. Note: This cmdlet updates the configuration set according to the property "Id". 





---
## Type CreateUserAdObject

Creates a user-level AD object.

The New-UserAdObject cmdlet creates a user-level AD object.

##### Example: 

######  code

```
    $User = New-Object Citrix.DeviceMgmt.Agent.Windows.Sdk.UserModel
    $User.Name = "CN=Domain Users,CN=Users,DC=domain,DC=local"
    $User.Type = "Group"
    $User.Enabled = $True
    $User.Priority = 100
    New-UserAdObject -InfrastructureServer "10.10.10.10" -UserAdObject $User
```

Creates a group named "Domain Users" with a priority of 100. The IP address of the remote infrastructure server is "10.10.10.10".







##### Example: 

######  code

```
    $User = New-Object Citrix.DeviceMgmt.Agent.Windows.Sdk.UserModel
    $User.Name = "CN=User1,CN=Users,DC=domain,DC=local"
    $User.Type = "User"
    $User.Enabled = $False
    $User.Priority = 80
    New-UserAdObject -UserAdObject $User
```

Creates a disabled user named "User1" with a priority of 80 on the local infrastructure server.











---
#### Property CreateUserAdObject.UserAdObject

 The user-level AD object to be created. Note: Use "distinguished name" or "SID" to specify this user-level AD object. You do not need to specify the "Id" property when creating this object because the ID is generated automatically.





---
## Type DeleteUserAdObject

Deletes a user-level AD object.

The Remove-UserAdObject cmdlet deletes a user-level AD object.

##### Example: 

######  code

```
    Remove-UserAdObject -InfrastructureServer "10.10.10.10" -Id 12
```

Deletes a user-level AD object whose ID is 12. The IP address of the remote infrastructure server is "10.10.10.10".







##### Example: 

######  code

```
    $User = (Get-UserAdObject) | Where-Object { $_.Name.ToLower().Contains("cn=user1,") })
    Remove-UserAdObject -UserAdObject $User.Id
```

Deletes a user whose name is "user1" on the local infrastructure server.











---
#### Property DeleteUserAdObject.Id

 The ID of the user-level AD object to be deleted. Note: You cannot delete the built-in user-level AD objects (Everyone and BUILTIN\Administrators) using this cmdlet. 





---
## Type GetUserAdObject

Queries user-level AD objects.

The Get-UserAdObject cmdlet queries user-level AD objects.

##### Example: 

######  code

```
    Get-UserAdObject -InfrastructureServer "10.10.10.10"
```

Queries all user-level AD objects. The IP address of the remote infrastructure server is "10.10.10.10".







##### Example: 

######  code

```
    Get-UserAdObject -SiteName "Default Site"
```

Queries all user-level AD objects in "Default Site" on the local infrastructure server.







##### Example: 

######  code

```
    Get-UserAdObject -Id 10
```

Queries the user-level AD object whose ID is 10 on the local infrastructure server.







##### Example: 

######  code

```
    Get-UserAdObject -Sid "S-1-1-0"
```

Queries all user-level AD objects whose SIDs are "S-1-1-0" on the local infrastructure server.











---
#### Property GetUserAdObject.SiteName

 The name of the configuration set that is used to filter user-level AD objects. Only the AD objects that belong to this configuration set are to be displayed. If this parameter is not specified, the filtering operation does not work. Note: This parameter does not work if the parameter "SiteId" is specified. 





---
#### Property GetUserAdObject.SiteId

 The ID of the configuration set that is used to filter user-level AD objects. Only the AD objects that belong to this configuration set are to be displayed. If this parameter is not specified, the filtering operation does not work. 





---
#### Property GetUserAdObject.Id

 If this parameter is specified, only the user-level AD object with the specified ID is to be displayed. 





---
#### Property GetUserAdObject.Sid

 The SID used to filter user-level AD objects. Only the AD objects with the specified SID are to be displayed. If this parameter is not specified, the filtering operation does not work. 





---
## Type UpdateUserAdObject

Updates a user-level AD object.

The Update-UserAdObject cmdlet updates a user-level AD object.

##### Example: 

######  code

```
    $User = (Get-UserAdObject -InfrastructureServer "10.10.10.10") | Where-Object { $_.Name.ToLower().Contains("cn=user1,") }
    $User.Enable = $False
    $User.Priority += 10
    $User.Description = "Modify the description"
    Update-UserAdObject -InfrastructureServer "10.10.10.10" -UserAdObject $User
```

 Updates a user whose name is "user1". The IP address of the remote infrastructure server is “10.10.10.10”. These commands disable the user status, change the description, and increase the priority by 10. 











---
#### Property UpdateUserAdObject.UserAdObject

 The user-level AD object to be updated. Note: This cmdlet updates the user-level AD object according to the property "Id". The properties "Sid", "Name", and "Type" are read-only, and they remain unchanged even if you specify values for them. 





---
#### Property Norskale.Administration.Console.Configuration.IAuthorizationInfo.CurrentAuthorizationLevel

 Current user authorization level. 



---


