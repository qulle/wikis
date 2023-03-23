# PowerShell
A living document with useful commands (Windows 10), not intended as a complete command reference.

## Note
This used to be a private repo but i changed it to be public because of ease of access for me. Use it as a reference if you like it but `i am not accountable for what happens when you execute commands in your environment`. Use with causion and Google commands that you don't know.

## Computer
```
C:\> Get-CimInstance -ClassName win32_operatingsystem | Format-List -Property *   # Get all system properties
C:\> (Get-CimInstance -ClassName win32_operatingsystem).Lastbootuptime            # Get timestamp when computer was started

C:\> powercfg /batteryreport /output "C:\battery-report.html"                     # Generate battery report
```

## Create new GUID
```
C:\> [guid]::NewGuid()
```

## Script execution policy
```
C:\> Get-ExecutionPolicy -List                            # List the different profiles available for restricting execution
C:\> Set-ExecutionPolicy Restricted                       # Sets the executionpolicy for the LocalMachine (requires admin privileges)
C:\> Set-ExecutionPolicy Restricted -Scope CurrentUser    # Sets the executionpolicy for the CurrentUser (requires admin privileges)
```

## Export list of installed programs to textfile
```
C:\> Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*,HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName, DisplayVersion, Publisher, InstallDate | Format-Table -AutoSize > $Profile\..\..\InstalledPrograms.txt
```

## Disable NetworkAdapter PowerManagement
```
C:\> Get-NetAdapterAdvancedProperty                                                            # Get NetAdapters
C:\> $WiFiAdapter = Get-NetAdapter -Physical -name "Wi-Fi" | Get-NetAdapterPowerManagement     # Get Adapter by name
C:\> $WiFiAdapter.AllowComputerToTurnOffDevice = 'Disabled'                                    # Set powersave mode to disabled
C:\> $WiFiAdapter | Set-NetworkAdapterPowerManagement                                          # Set changes to the adapter

C:\> $WiFiAdapter | Format-List -Property '*'     # To list all properties on variable
C:\> $WiFiAdapter.getType()                       # Useful to check datatype, some pipe operations might not return what you expected Array vs Object
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
C:\> Test-NetConnection <localhost/ip> -Port 80          # Test TCP connectivity on port 80 for specified host
```

## Set startup path through profile
```
C:\> notepad $profile
Set-Location C:\Users\<USERNAME>\Documents\ # Add line to the profile-file in notepad
```
