# Bash
A living document with useful commands (Windows 10), not intended as a complete command reference.

## Note
This used to be a private repo but i changed it to be public because of ease of access for me. Use it as a reference if you like it but `i am not accountable for what happens when you execute commands in your environment`, use with causion and Google commands that you don't know.

## Misc
```
$ which $SHELL                     # Outputs current shell

$ grep -v <text> file.txt          # Display all rows that does't contains the <text> term
$ grep -r <text> target-directory/ # Recursuvely search for pattern <text> in all files in the specified directory
$ grep -i <text> file.txt          # Case insensitive search

$ history                          # Display command history
$ history | grep git               # Display alla commands that contains the word git
$ history -c                       # Clear all history
```

## Computer
```
$ top                              # Monitor running processes and the resources
```

## Files and directories
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

## Programs
```
$ which python3                    # Identify and report the location of the provided executable
```

## Networking
```
$ ifconfig                         # Display information about current network configuration
$ curl -L google.com               # Makes Get request downloading the content for the resource (index.html)
```

## Custom aliases in .bashrc
```
alias w++17='g++ -std=c++17 -Wall -Wextra -Wpedantic' # Full example: https://github.com/qulle/wikis/edit/main/wiki-bashrc.md
```
