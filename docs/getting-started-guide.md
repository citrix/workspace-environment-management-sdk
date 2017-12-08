# Getting started with the SDK

## Using the PowerShell modules

### Installation

The PowerShell modules are installed automatically when you install the Workspace Environment Management infrastructure services.

### Permissions

To use the PowerShell modules, in addition to the privileges required to use the local GUI utilities, you need the following:

* Microsoft Windows PowerShell version 3.0 or later installed on your machine
* Privileges to run PS scripts on the machine
* Access to the target machine
* Privileges for configuring registry, windows services, folders security properties and databases on the target machines. (When these machines are remote, you need these privileges on the remote machine.)

### To access and run the cmdlets

Start a shell in PowerShell.

### Using scripts

You can write your own scripts and include Workspace Environment Management PowerShell cmdlets.

To use PowerShell cmdlets within scripts, set the execution policy in PowerShell. For more information about PowerShell execution policy, see your Microsoft documentation.

>**Note**: Filepaths&#8212;If you use **New-WemDatabase**, ensure that the filepaths you specify for the DataFilePath and LogFilePath properties are valid and fully formed.