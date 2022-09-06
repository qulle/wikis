# CMD, PowerShell and Bash commands
A living document with useful commands (Windows 10), not intended as a complete command reference.

## Note
This used to be a private repo but i changed it to be public because of ease of access for me. Use it as a reference if you like it but `i am not accountable for what happens when you execute commands in your environment`, use with causion and Google commands that you don't know.

## 1. CMD
### Computer
```
$ ver                         # Display current version number of Windows
$ hostname                    # Show name of host
$ systeminfo                  # Show information about the system
$ msinfo32                    # System information GUI with detailed information about the system
$ dxdiag                      # Used to test DirectX functionality and troubleshoot video- or sound-related hardware problems
$ winver                      # Show information about Windows

$ wmic bios get serialnumber                                                  # Get BIOS serial number of current machine
$ wmic /user:Administrator /node:<remote-computer-name> bios get serialnumber # Get BIOS serial number of remote machine

$ fsutil fsinfo ntfsinfo   C: # Get information about the filesystem (Requires elevated privileges)
$ fsutil fsinfo volumeInfo C: # Get information about the volume     (Requires elevated privileges)
$ fsutil fsinfo driveType  C: # Get drive typ information
$ fsutil fsinfo drives        # List all available drives
$ sfc /scannow                # Check all the system files and look for errors
$ chkdsk /r                   # Scan hard drive for logical or physical errors
$ driverquery                 # Show complete list of installed drivers and history

$ tasklist                    # List all running processes
$ taskkill /pid <PID>         # Stop running process by pid
$ taskkill /pid <PID> /F      # Force stop preccess by pid

$ explorer .                  # Start explorer in the current directory
$ start .                     # Start explorer in the current directory

$ path                        # Display dump of current PATH config
$ ECHO.%PATH:;= & ECHO.%      # Display pretty dump of current PATH config

$ start shell:startup         # Open the Startup folder for current user
$ start shell:common startup  # Open the Startup folder for all users (Not working from CMD, only Win + R)
```

### Programs
```
# Create shortcut to run a program as another user and save credentials
C:\Windows\System32\runas.exe /savecred /user:domain\username "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" 
```

### Files and directories
```
$ type <FILE>                            # Display content of file
$ chcp                                   # Display Console Code Page
$ chcp 65001                             # Set Code Page 65001 => UTF-8
$ chcp 1252                              # Set Code Page 1252  => Windows-1252 Single-byte character encoding of the Latin alphabet
$ chcp 437                               # Set Code Page 437   => Character set of the original IBM PC
$ chcp 850                               # Set Code Page 850   => Latin-1 - Western European languages
$ charmap                                # Check characters of different encodings and fonts installed on your system

$ dir                                    # List files and directories
$ tree                                   # List files and directories in a tree structure
$ tree | more                            # Limit the output by print sections of data | more works with all commands
$ mkdir <NAME>                           # Make directory with given name
$ rmdir <NAME>                           # Remove directory with given name, must be empty
$ rmdir /Q /S <NAME>                     # Remove directory that contains directories and/or files, /Q = quiet, /S = subfolders

$ assoc                                  # Show file associations
$ fc /a file-one.txt file-two.txt        # Compares two files using ascii comparison
$ fc /b file-one.jpg file-two.jpg        # Compares two files using binary comparison
$ fsutil file createnew test.txt 1048576 # Generate file of size 1MB

$ subst                                  # Display list of current virtual drives
$ subst x: C:\Folder\Example             # Map local directory to drive letter
$ subst x: /D                            # Remove mapped drive
```

### Manage Windows user accounts
```
$ net users                              # Display all user accounts
$ net users <ACCOUNT-NAME>               # Detaild information about user account
$ net users <ACCOUNT-NAME> *             # Change password of account
$ net users add <ACCOUNT-NAME>           # Add user account
$ net users remove <ACCOUNT-NAME>        # Remove user account

$ whoami                                 # Show current user
$ whoami /user                           # Show detailed info of current user
$ whoami /groups                         # Show what groups the current user is member of

$ gpupdate                               # Update the domain group policy
$ gpupdate /f                            # Force update the group policy

$ runas /noprofile /user:username@domain "cmd /k whoami /groups"     # Check groups for other user ex. domain admin account
```

### Networking
```
$ ipconfig                 # Basic network interfaces
$ ipconfig /all            # Detailed network interfaces
$ ipconfig /renew
$ ipconfig /renew6
$ ipconfig /release
$ ipconfig /release6
$ ipconfig /displaydns     # Display the contents of the DNS Resolver Cache (PowerShell command available)
$ ipcinfig /flushdns       # Purges the DNS Resolver cache

$ getmac                   # Get mac addresses for the installed media devices
$ arp -a                   # Display ARP (address resolution protocol) cache
$ arp -d                   # Clear ARP cache

$ nslookup google.com      # Name server lookup, display IP for domain

$ ping <HOST/IP>
$ ping <HOST/IP> -t        # Continuous ping

$ tracert <HOST/IP>        # Trace route to destination
$ pathping <HOST/IP>       # Combines tracert and ping

$ nbtstat                  # Utility to display stats and current connections using NetBios over TCP/IP
$ netstat -a               # Display network connections
$ netstat -b               # Display network connections and processes (requires admin privileges)

$ net use s: \\network.unit\directory /persistent:Yes     # Map network drives to drive letter
$ net use s: /delete                                      # Remove mapped drive
```

### Open EXE files
```
$ start regedit                # Starts register editor
$ start mstsc.exe              # Starts remote desktop client
```

### Open CPL files
```
$ control appwiz.cpl           # Add and remove programs
$ control inetcpl.cpl          # Internet settings
$ control wscui.cpl            # Security and Maintenance
$ control firewall.cpl         # Windows Defender Firewall Control Panel DLL Launching Stub
$ control hdwwiz.cpl           # Device manager
$ control sysdm.cpl            # System properties, environment variable
$ control access.cpl           # Accessibility Options
$ control timedate.cpl         # Date and Time Properties
$ control desk.cpl             # Display Properties
$ control joy.cpl              # Joystick Properties
$ control main.cpl             # Mouse Properties
$ control ncpa.cpl             # Network Connections
$ control ncpl.cpl             # Network Properties
$ control telephon.cpl         # Phone and Modem options
$ control powercfg.cpl         # Power Management
$ control intl.cpl             # Regional settings
$ control mmsys.cpl sounds     # Sound Properties
$ control mmsys.cpl            # Sounds and Audio Device Properties
$ control nusrmgr.cpl          # User settings
```

### Open MSC files
```
$ start certmgr.msc            # Certificate Manager
$ start ciadv.msc              # Indexing Service
$ start compmgmt.msc           # Computer management
$ start devmgmt.msc            # Device Manager
$ start dfrg.msc               # Defragment
$ start diskmgmt.msc           # Disk Management
$ start fsmgmt.msc             # Folder Sharing Management
$ start eventvwr.msc           # Event Viewer
$ start gpedit.msc             # Group Policy
$ start iis.msc                # Internet Information Services
$ start lusrmgr.msc            # Local Users and Groups
$ start mscorcfg.msc           # Net configurations
$ start ntmsmgr.msc            # Removable Storage
$ start perfmon.msc            # Performance Manager
$ start secpol.msc             # Local Security Policy
$ start services.msc           # System Services
$ start wmimgmt.msc            # Windows Management 
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
### Create new GUID
```
$ [guid]::NewGuid()
```

### Script execution policy
```
$ Get-ExecutionPolicy -List                            # List the different profiles available for restricting execution
$ Set-ExecutionPolicy Restricted                       # Sets the executionpolicy for the LocalMachine (requires admin privileges)
$ Set-ExecutionPolicy Restricted -Scope CurrentUser    # Sets the executionpolicy for the CurrentUser (requires admin privileges)
```

### Disable NetworkAdapter PowerManagement
```
$ $WiFiAdapter = Get-NetAdapter -Physical -name "Wi-Fi" | Get-NetAdapterPowerManagement     # Get Adapter by name
$ $WiFiAdapter.AllowComputerToTurnOffDevice = 'Disabled'                                    # Set powersave mode to disabled
$ $WiFiAdapter | Set-NetworkAdapterPowerManagement                                          # Set changes to the adapter

$ $WiFiAdapter | Format-List -Property '*'     # To list all properties on variable
$ $WiFiAdapter.getType()                       # Useful to check datatype, some pipe operations might not return what you expected Array vs Object
```

### Networking
```
$ Get-DnsClientCache # Display the contents of the DNS Resolver Cache (CMD command available)
```

### Set startup path through profile
```
$ notepad $profile
Set-Location C:\Users\<USERNAME>\Documents\ # Add line to the profile-file in notepad
```

## 3. Bash
### Misc
```
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
$ ls -la                           # List all (inc. hidden) files in list format
$ cd                               # Change directory

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
$ ifconfig                         # Used for displaying current network configuration information

$ curl -L google.com               # Makes Get request downloading the content for the resource (index.html)
```

### Custom aliases in .bashrc
```
alias w++17='g++ -std=c++17 -Wall -Wextra -Wpedantic' # Full example: https://github.com/qulle/wikis/edit/main/wiki-bashrc.md
```
