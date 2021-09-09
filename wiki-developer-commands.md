# Useful commands to know when coding

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

## C++
### Compiling using terminal CL
```
$ cl /EHsc /std:c++17 program.cpp
```

## NPM
### Basic commands
```
$ npm init                                       # Init package.json
$ npm init -y                                    # Init package.json with -y = Yes to all settings.
$ npm instaall                                   # Install all dependencies listed in package.json
```

### Un/Installing Angular
```
$ npm install -g @angular/cli@latest             # Install latest version of Angular CLI
$ npm uninstall -g @angular/cli                  # Uninstall Angular CLI

$ rm -rf node_modules                            # Remove local node_modules directory from project
$ npm uninstall --save-dev @angular/cli          # Uninstall local project version of Angular CLI
$ npm install --save-dev @angular/cli@latest     # Install latest version of Angular CLI locally
$ npm install                                    # Reinstall all other dependencies from package.json
```

### Update packages
```
$ npm outdated                                   # List all outdated packages
$ npm update                                     # Update all outdated packages (minor versions)
$ npm update "react" "react-dom"                 # Update specific outdated packages (minor versions)
$ npm install <packagename>@latest               # Update outdated package (major version)
```

### List packages and search for security updates etc.
```
$ npm list
$ npm audit
$ npm install
```

### List all globally installed packages
```
$ npm ls -g --depth 0                            # List all globally installed packages at a depth of 0.
```
