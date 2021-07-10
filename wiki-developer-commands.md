# Useful commands to know when coding.

## C#
### View compiled C# IL code
Compiling csharp code produces IL (CIL) code. The following command opens an application that can display the compiled IL (CIL) code. Note, might require a developer command prompt to find the command. 
```
$ ildasm
```

### Compiling using terminal CSC
```
$ csc program.cs
```

### Dotnet commands
```
$ dotnet new webapi -n <NAME>                # Create a new webapi project
$ dotnet build                               # Build the project
$ dotnet run                                 # Run the project
$ dotnet add package <NAME>                  # Add dependencies to the project

$ dotnet ef migrations add <NAME>            # Create a migration when changes have been made in the models
$ dotnet ef migrations remove                # If the migration scripts are not to your satisfaction, undo and fix before add once again
$ dotnet ef database update                  # Perform migrations to the database

$ dotnet tool install --global dotnet-ef     # Command to install the EF tools
$ dotnet tool update --global dotnet-ef      # Command to update the EF tools
```

## C++
### Compiling using terminal CL
```
$ cl /EHsc /std:c++17 program.cpp
```

## NPM
### Installing angular
```
$ npm install -g @angular/cli@latest         # Install latest version of Angular CLI
$ npm uninstall -g @angular/cli              # Uninstall Angular CLI
```
