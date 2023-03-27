# PowerShell
A living document with useful commands (Windows 10), not intended as a complete command reference.

## Note
This used to be a private repo but i changed it to be public because of ease of access for me. Use it as a reference if you like it but `i am not accountable for what happens when you execute commands in your environment`. Use with causion and Google commands that you don't know.

## About
PowerShell uses a verb-noun pair for the names of cmdlets and for their derived dotNET classes. The verb part of the name identifies the action that the cmdlet performs. The noun part of the name identifies the entity on which the action is performed.

## Aliases
PowerShell can execute commands like `dir` `ls` etc. This is because of aliases. Known commands from CMD and Bash have been made available to speed up common tasks and makes it easier for people coming from other shells. Display all aliases with this command.
```
C:\> Get-Alias                                          # Alias for this is GAL
C:\> Get-Alias *ec*                                     # Get aliases containing ec (echo, select)
```

## Cmdlets
How to work with the shell when building, piping and executing commands etc.
```
C:\> Get-Command                                        # List all commands
C:\> Get-Command *printer*                              # List all commands containing printer

C:\> Get-ChildItem                                      # Singel command
C:\> Get-ChildItem | Select-Object Name                 # Piping output to Select-Object and only selects Name property
C:\> Get-ChildItem | Select-Object -First 1             # Select the first item that is returned
C:\> Get-ChildItem | Select-Object -Index 0             # Select the first item by its index (Same as above)
C:\> Get-ChildItem | Select-Object *                    # Select all properties on the object

C:\> Get-ChildItem | Get-Member                         # Return properties and methods for given object
C:\> Get-ChildItem | Select-Object Name | Get-Member    # Return methods for Name property

C:\> (Get-ChildItem | Select-Object -First 1).Name      # Return pure property without table format
```

## Help Pages
```
C:\> Get-Help Select-Object                             # Get documentation about given command
C:\> Get-Help Select-Object -Full                       # Get full documentation about given command
C:\> Get-Help *printer*                                 # List all documentation containing printer
C:\> Update-Help                                        # Updated the documentation, (requires admin privileges)
```

## Output Formatting
```
C:\> Get-ChildItem | Format-Table                       # Format as table (default)
C:\> Get-ChildItem | Format-Wide                        # Wide format without table headers
C:\> Get-ChildItem | Format-List                        # Detailed output with more properties
C:\> Get-ChildItem | Format-List *                      # Detailed output with all properties
```

## Output Redirecting
```
C:\> Get-ChildItem > .\directory.txt                    # Redirecting using common stream
C:\> Get-ChildItem | Out-File .\directory.txt           # Redirecting using Out-
C:\> Get-ChildItem | Out-GridView                       # Detailed GUI output with filter options
```

## Handling Files
```
C:\> New-Item .\file.txt                                # Create new document with name file.txt
C:\> New-Item -ItemType Directory folder                # Create new directory with name folder
C:\> Move-Item .\file.txt .\Desktop\                    # Move file to new location
C:\> Copy-Item .\file.txt .\Desktop\                    # Copy file to new location
C:\> Remove-Item .\file.txt                             # Remove file
C:\> Remove-Item .\folder                               # Remove folder
```

## Date
```
C:\> (Get-Date).ToString("yyyy-MM-dd HH:mm:ss.FFF")     # Get timestamp with format 2023-03-27 09:40:21.443
```

## Profiles and Execution Policies
```
C:\> $profile                                           # Get current users profile
C:\> $profile | Get-Object *                            # Get all profiles
C:\> notepad $profile                                   # Opens profile-file to edit, might need to create file and/or full path

C:\> Get-ExecutionPolicy -List                          # List the different profiles available for restricting execution
C:\> Set-ExecutionPolicy Restricted                     # Sets the executionpolicy for the LocalMachine (requires admin privileges)
C:\> Set-ExecutionPolicy Restricted -Scope CurrentUser  # Sets the executionpolicy for the CurrentUser (requires admin privileges)
```

## Variables and Types
```
C:\> Get-TypeData                                                  # Get all datatypes
C:\> Get-TypeData *ip*                                             # Get all datatypes containing ip
C:\> Get-Process                                                   # Get all running proccesses
C:\> Get-Process | Select-Object -First 1                          # Get first item in processes
C:\> (Get-Process | Select-Object -First 1).GetType()              # Get the type of the first item (Process)
C:\> (Get-Process | Select-Object -First 1).GetType().FullName     # Get the full namespace of the type

C:\> $email = [MailAddress]"john.doe@gmail.com"                    # Casting given data to datatype of MailAddress
C:\> $email.GetType()                                              # Get type of variable
```

## PSDrives
Creates temporary and persistent drives that are mapped to or associated with a location in a data store. 
```
C:\> Get-PSDrive                                                   # Get all PSDrive contexts
C:\> Set-Location Variable:                                        # Changing to the PSDrive Variable as context
C:\> Set-Location C:                                               # Changing to the PSDrive C disk as context

C:\> $Env:windir                                                   # Access a variable inside the PSDrive Env
```

## Computer
```
C:\> Get-Variable                                                                 # View all predefined variables
C:\> Get-ChildItem Env:                                                           # View all environment variables in the current PowerShell session

C:\> Get-CimInstance -ClassName win32_operationsystem | Get-Member                # Get all properties and methods
C:\> Get-CimInstance -ClassName win32_operatingsystem | Format-List -Property *   # Get all system properties with current values
C:\> (Get-CimInstance -ClassName win32_operatingsystem).Lastbootuptime            # Get timestamp when computer was started
```

## Power Management
```
C:\> powercfg /batteryreport /output "C:\battery-report.html"                     # Generate battery report
```

## Create new Global Unique Identifier (GUID)
```
C:\> [Guid]::NewGuid()
```

## Export Installed Programs
```
C:\> Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*,HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName, DisplayVersion, Publisher, InstallDate | Format-Table -AutoSize > $Profile\..\..\InstalledPrograms.txt
```

## Disable NetworkAdapter PowerManagement
```
C:\> Get-NetAdapterAdvancedProperty                                                            # Get NetAdapters
C:\> $WiFiAdapter = Get-NetAdapter -Physical -name "Wi-Fi" | Get-NetAdapterPowerManagement     # Get Adapter by name
C:\> $WiFiAdapter.AllowComputerToTurnOffDevice = 'Disabled'                                    # Set powersave mode to disabled
C:\> $WiFiAdapter | Set-NetworkAdapterPowerManagement                                          # Set changes to the adapter

C:\> $WiFiAdapter | Format-List -Property *              # To list all properties on variable
C:\> $WiFiAdapter.GetType()                              # Useful to check datatype, some pipe operations might not return what you expected Array vs Object
```

## Networking
```
C:\> Get-DnsClientCache # Display the contents of the DNS Resolver Cache (CMD command available)

C:\> netsh wlan show networks                            # Display visible networks
C:\> netsh wlan show networks mode=bssid                 # Display visible networks and access points
C:\> netsh wlan show interfaces                          # Display interfaces
C:\> netsh wlan show profiles                            # Display profiles for interfaces

C:\> Test-NetConnection                                  # Test Ping connectivity
C:\> Test-NetConnection -InformationLevel "Detailed"     # Test Ping connectivity with detailed information
C:\> Test-NetConnection -Port 80                         # Test TCP connectivity on port 80
C:\> Test-NetConnection <hostname/ip> -Port 80           # Test TCP connectivity on port 80 for specified host
```
