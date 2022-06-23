# Useful commands to know when coding
A living document with useful developer commands, not intended as a complete language reference.

## C++
### Compiling
```
$ cl /EHsc /std:c++17 program.cpp                            # Windows cl
$ g++ -std=c++17 -Wall -Wextra -Wpedantic program.cpp        # Linux g++
```

## C#
### View compiled C# IL code
Compiling csharp code produces IL (CIL) code. The following command opens an application that can display the compiled IL (CIL) code. Note, might require a developer command prompt to find the command. There is also two other tools for this purpose `ILSpy` and `dnspy`, not installed by default.
```
$ ildasm
```

### Compiling using terminal CSC
```
$ csc program.cs
```

### Checking available C# versions
```
$ csc -langversion:?
```

### Dotnet commands
```
$ dotnet --version                               # Check version of dotnet

$ dotnet new webapi -n <NAME>                    # Create a new webapi project
$ dotnet build                                   # Build the project
$ dotnet run                                     # Run the project
$ dotnet add package <NAME>                      # Add dependencies to the project

$ dotnet ef migrations add <NAME>                # Create a migration when changes have been made in the models
$ dotnet ef migrations remove                    # If the migration scripts are not to your satisfaction, undo and fix before add once again
$ dotnet ef database update                      # Perform migrations to the database

$ dotnet tool install --global dotnet-ef         # Command to install the EF tools
$ dotnet tool update --global dotnet-ef          # Command to update the EF tools

$ dotnet list package                            # List all (nuget) packages that is used in a solution or csproj
$ dotnet list <PROJECT-NAME> package             # List all (nuget) packages in a specific project

$ dotnet list reference                          # List all project references, what csproj:s that knows/uses other csproj:s
$ dotnet list <PROJECT-NAME> reference           # List all project references in a specific project
```

## NPM
```
$ npm init                                       # Init package.json
$ npm init -y                                    # Init package.json with -y = Yes to all settings.
$ npm install                                    # Install all dependencies listed in package.json
$ npm install -g npm@latest                      # Update to latest version of npm

$ npm install -g @angular/cli@latest             # Install latest version of Angular CLI
$ npm uninstall -g @angular/cli                  # Uninstall Angular CLI

$ rm -rf node_modules                            # Remove local node_modules directory from project
$ npm uninstall --save-dev @angular/cli          # Uninstall local project version of Angular CLI
$ npm install --save-dev @angular/cli@latest     # Install latest version of Angular CLI locally
$ npm install                                    # Reinstall all other dependencies from package.json

$ npm outdated                                   # List all outdated packages
$ npm update                                     # Update all outdated packages (minor versions)
$ npm update "react" "react-dom"                 # Update specific outdated packages (minor versions)
$ npm install <packagename>@latest               # Update outdated package (major version)

$ npm list                                       # List all installed packages 
$ npm audit                                      # Audit packages and search for updates
$ npm install                                    # Install all available updates
$ npm install <packagename>@version              # Install specific package available update

$ npm ls -g --depth 0                            # List all globally installed packages at a depth of 0.
```

## NG (CLI)
```
TODO
```
