# CMD, PowerShell and Bash commands
A living document with useful commands (Windows 10), not intended as a complete command reference.

## Note
This used to be a private repo but i changed it to be public because of ease of access for me. Use it as a reference if you like it but `i am not accountable for what happens when you execute commands in your environment`, use with causion and Google commands that you don't know.

## 1. CMD
### Computer
```
C:\> ver                         # Display current version number of Windows
C:\> hostname                    # Show name of host
C:\> systeminfo                  # Show information about the system
C:\> msinfo32                    # System information GUI with detailed information about the system
C:\> dxdiag                      # Used to test DirectX functionality and troubleshoot video- or sound-related hardware problems
C:\> winver                      # Show information about Windows

C:\> wmic bios get serialnumber                                                  # Get BIOS serial number of current machine
C:\> wmic /user:Administrator /node:<remote-computer-name> bios get serialnumber # Get BIOS serial number of remote machine

C:\> fsutil fsinfo ntfsinfo   C: # Get information about the filesystem (Requires elevated privileges)
C:\> fsutil fsinfo volumeInfo C: # Get information about the volume     (Requires elevated privileges)
C:\> fsutil fsinfo driveType  C: # Get drive typ information
C:\> fsutil fsinfo drives        # List all available drives
C:\> chkdsk /r                   # Scan hard drive for logical or physical errors
C:\> driverquery                 # Show complete list of installed drivers and history
C:\> sfc /scannow                # Scan for and restore corrupted Windows system files against known references
C:\> dism /Online /Cleanup-Image /RestoreHealth # Restore and download known system file references (src /scannow is often executed after this)

C:\> tasklist                    # List all running processes
C:\> taskkill /pid <PID>         # Stop running process by pid
C:\> taskkill /pid <PID> /F      # Force stop preccess by pid

C:\> explorer .                  # Start explorer in the current directory
C:\> start .                     # Start explorer in the current directory

C:\> path                        # Display dump of current PATH config
C:\> ECHO.%PATH:;= & ECHO.%      # Display pretty dump of current PATH config

C:\> start shell:startup         # Open the Startup folder for current user
C:\> start shell:common startup  # Open the Startup folder for all users (Not working from CMD, only Win + R)
```

### Programs
```
# Create shortcut to run a program as another user and save credentials
C:\Windows\System32\runas.exe /savecred /user:domain\username "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" 
```

### Files and directories
```
C:\> type <FILE>                            # Display content of file
C:\> chcp                                   # Display Console Code Page
C:\> chcp 65001                             # Set Code Page 65001 => UTF-8
C:\> chcp 1252                              # Set Code Page 1252  => Windows-1252 Single-byte character encoding of the Latin alphabet
C:\> chcp 437                               # Set Code Page 437   => Character set of the original IBM PC
C:\> chcp 850                               # Set Code Page 850   => Latin-1 - Western European languages
C:\> charmap                                # Check characters of different encodings and fonts installed on your system

C:\> dir                                    # List files and directories
C:\> tree                                   # List files and directories in a tree structure
C:\> tree | more                            # Limit the output by print sections of data | more works with all commands
C:\> mkdir <NAME>                           # Make directory with given name
C:\> rmdir <NAME>                           # Remove directory with given name, must be empty
C:\> rmdir /Q /S <NAME>                     # Remove directory that contains directories and/or files, /Q = quiet, /S = subfolders

C:\> assoc                                  # Show file associations
C:\> fc /a file-one.txt file-two.txt        # Compares two files using ascii comparison
C:\> fc /b file-one.jpg file-two.jpg        # Compares two files using binary comparison
C:\> fsutil file createnew test.txt 1048576 # Generate file of size 1MB

C:\> subst                                  # Display list of current virtual drives
C:\> subst x: C:\Folder\Example             # Map local directory to drive letter
C:\> subst x: /D                            # Remove mapped drive
```

### Manage Windows user accounts
```
C:\> net users                              # Display all user accounts
C:\> net users <ACCOUNT-NAME>               # Detaild information about user account
C:\> net users <ACCOUNT-NAME> *             # Change password of account
C:\> net users add <ACCOUNT-NAME>           # Add user account
C:\> net users remove <ACCOUNT-NAME>        # Remove user account

C:\> whoami                                 # Show current user
C:\> whoami /user                           # Show detailed info of current user
C:\> whoami /groups                         # Show what groups the current user is member of

C:\> gpupdate                               # Update the domain group policy
C:\> gpupdate /f                            # Force update the group policy
C:\> gpresult /Scope User /v                # List current policies for current user
C:\> gpresult /Scope Computer /v            # List current policies for this machine

C:\> runas /noprofile /user:username@domain "cmd /k whoami /groups"     # Check groups for other user ex. domain admin account
```

### Networking
```
C:\> ipconfig                   # Basic network interfaces
C:\> ipconfig /all              # Detailed network interfaces
C:\> ipconfig /renew
C:\> ipconfig /renew6
C:\> ipconfig /release
C:\> ipconfig /release6
C:\> ipconfig /displaydns       # Display the contents of the DNS Resolver Cache (PowerShell command available)
C:\> ipcinfig /flushdns         # Purges the DNS Resolver cache

C:\> getmac                     # Get mac addresses for the installed media devices
C:\> arp -a                     # Display ARP (address resolution protocol) cache
C:\> arp -d                     # Clear ARP cache

C:\> nslookup google.com        # Name server lookup, display IP for domain

C:\> ping <HOST/IP>
C:\> ping <HOST/IP> -t          # Continuous ping

C:\> tracert <HOST/IP>          # Trace route to destination
C:\> pathping <HOST/IP>         # Combines tracert and ping

C:\> netsh wlan show wlanreport # Generate network HTML report

C:\> nbtstat                    # Utility to display stats and current connections using NetBios over TCP/IP
C:\> netstat -a                 # Display network connections
C:\> netstat -b                 # Display network connections and processes (requires admin privileges)

C:\> net use s: \\network.unit\directory /persistent:Yes     # Map network drives to drive letter
C:\> net use s: /delete                                      # Remove mapped drive
```

### Open EXE files
```
C:\> mrt                    # Starts the Microsoft Malicious Software Removal Tool
C:\> regedit                # Starts register editor
C:\> mstsc                  # Starts remote desktop client
```

### Open CPL files
```
C:\> control appwiz.cpl           # Add and remove programs
C:\> control inetcpl.cpl          # Internet settings
C:\> control wscui.cpl            # Security and Maintenance
C:\> control firewall.cpl         # Windows Defender Firewall Control Panel DLL Launching Stub
C:\> control hdwwiz.cpl           # Device manager
C:\> control sysdm.cpl            # System properties, environment variable
C:\> control access.cpl           # Accessibility Options
C:\> control timedate.cpl         # Date and Time Properties
C:\> control desk.cpl             # Display Properties
C:\> control joy.cpl              # Joystick Properties
C:\> control main.cpl             # Mouse Properties
C:\> control ncpa.cpl             # Network Connections
C:\> control ncpl.cpl             # Network Properties
C:\> control telephon.cpl         # Phone and Modem options
C:\> control powercfg.cpl         # Power Management
C:\> control intl.cpl             # Regional settings
C:\> control mmsys.cpl sounds     # Sound Properties
C:\> control mmsys.cpl            # Sounds and Audio Device Properties
C:\> control nusrmgr.cpl          # User settings
```

### Open MSC files
```
C:\> start certmgr.msc            # Certificate Manager
C:\> start ciadv.msc              # Indexing Service
C:\> start compmgmt.msc           # Computer management
C:\> start devmgmt.msc            # Device Manager
C:\> start dfrg.msc               # Defragment
C:\> start diskmgmt.msc           # Disk Management
C:\> start fsmgmt.msc             # Folder Sharing Management
C:\> start eventvwr.msc           # Event Viewer
C:\> start gpedit.msc             # Group Policy
C:\> start iis.msc                # Internet Information Services
C:\> start lusrmgr.msc            # Local Users and Groups
C:\> start mscorcfg.msc           # Net configurations
C:\> start ntmsmgr.msc            # Removable Storage
C:\> start perfmon.msc            # Performance Manager
C:\> start secpol.msc             # Local Security Policy
C:\> start services.msc           # System Services
C:\> start wmimgmt.msc            # Windows Management 
```

### Windows enviroment path variables
```
%AllUsersProfile%                                           # Open the All User's Profile C:\ProgramData
%AppData%                                                   # Opens AppData folder C:\Users\{username}\AppData\Roaming
%CommonProgramFiles%                                        # C:\Program Files\Common Files
%CommonProgramFiles(x86)%                                   # C:\Program Files (x86)\Common Files
%HomeDrive%                                                 # Opens your home drive C:\
%LocalAppData%                                              # Opens local AppData folder C:\Users\{username}\AppData\Local
%ProgramData%                                               # C:\ProgramData
%ProgramFiles%                                              # C:\Program Files or C:\Program Files (x86)
%ProgramFiles(x86)%                                         # C:\Program Files (x86)
%Public%                                                    # C:\Users\Public
%SystemDrive%                                               # C:
%SystemRoot%                                                # Opens Windows folder C:\Windows
%Temp%                                                      # Opens temporary file Folder C:\Users\{Username}\AppData\Local\Temp
%UserProfile%                                               # Opens your user's profile C:\Users\{username}
%AppData%\Microsoft\Windows\Start Menu\Programs\Startup     # Opens Windows 10 Startup location for program shortcuts
```

## 2. PowerShell
### Computer
```
C:\> Get-CimInstance -ClassName win32_operatingsystem | Format-List -Property *   # Get all system properties
C:\> (Get-CimInstance -ClassName win32_operatingsystem).Lastbootuptime            # Get timestamp when computer was started

C:\> powercfg /batteryreport /output "C:\battery-report.html"                     # Generate battery report
```

### Create new GUID
```
C:\> [guid]::NewGuid()
```

### Script execution policy
```
C:\> Get-ExecutionPolicy -List                            # List the different profiles available for restricting execution
C:\> Set-ExecutionPolicy Restricted                       # Sets the executionpolicy for the LocalMachine (requires admin privileges)
C:\> Set-ExecutionPolicy Restricted -Scope CurrentUser    # Sets the executionpolicy for the CurrentUser (requires admin privileges)
```

### Export list of installed programs to textfile
```
C:\> Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*,HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName, DisplayVersion, Publisher, InstallDate | Format-Table -AutoSize > $Profile\..\..\InstalledPrograms.txt
```

### Disable NetworkAdapter PowerManagement
```
C:\> Get-NetAdapterAdvancedProperty                                                            # Get NetAdapters
C:\> $WiFiAdapter = Get-NetAdapter -Physical -name "Wi-Fi" | Get-NetAdapterPowerManagement     # Get Adapter by name
C:\> $WiFiAdapter.AllowComputerToTurnOffDevice = 'Disabled'                                    # Set powersave mode to disabled
C:\> $WiFiAdapter | Set-NetworkAdapterPowerManagement                                          # Set changes to the adapter

C:\> $WiFiAdapter | Format-List -Property '*'     # To list all properties on variable
C:\> $WiFiAdapter.getType()                       # Useful to check datatype, some pipe operations might not return what you expected Array vs Object
```

### Networking
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

### Set startup path through profile
```
C:\> notepad $profile
Set-Location C:\Users\<USERNAME>\Documents\ # Add line to the profile-file in notepad
```

## 3. Bash
### Misc
```
$ which $SHELL                     # Outputs current shell

$ grep -v <text> file.txt          # Display all rows that does't contains the <text> term
$ grep -r <text> target-directory/ # Recursuvely search for pattern <text> in all files in the specified directory
$ grep -i <text> file.txt          # Case insensitive search

$ history                          # Display command history
$ history | grep git               # Display alla commands that contains the word git
$ history -c                       # Clear all history
```

### Computer
```
$ top                              # Monitor running processes and the resources
```

### Files and directories
```
$ ll                               # List files and directories in list format
$ ls                               # List files and directories
$ ls -la                           # List all (inc. hidden) files in list format, also displays permissions
$ cd                               # Change directory

$ chmod +x script.sh               # Add execute permissions to the file script.sh

$ pwd                              # Print working directory

$ touch file.txt                   # Create file or update timestamp if exists
$ touch -a file.txt                # Update only the access timestamp of the file
$ touch -m file.txt                # Update only the modify time of the file

$ file data.csv                    # Check file encoding information
$ cat file.txt                     # Display content of file
$ cat -n file.txt                  # Display content of file with line numbers 
$ cat -T file.txt                  # Display content of file and mark if tab or spaces

$ mv file.txt child-directory/     # Move file to other directory
$ mv file.txt ~                    # Move file from current directory to home directory
$ mv file.txt file-2.txt           # Rename file by moving it to same location

$ mkdir <name>                     # Create directory
$ rmdir <name>                     # Remove empty directory

$ rm -i *.txt                      # Remove files, prompt user to confirm
$ rm -r                            # Remove directories including files in them
$ rm -f                            # Remove files and directories without prompting the user
$ rm -rf                           # Use with caution
```

### Programs
```
$ which python3                    # Identify and report the location of the provided executable
```

### Networking
```
$ ifconfig                         # Display information about current network configuration
$ curl -L google.com               # Makes Get request downloading the content for the resource (index.html)
```

### Custom aliases in .bashrc
```
alias w++17='g++ -std=c++17 -Wall -Wextra -Wpedantic' # Full example: https://github.com/qulle/wikis/edit/main/wiki-bashrc.md
```
