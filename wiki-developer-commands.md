# Useful commands to know when coding.

## C#
### View compiled C# IL code
Compiling csharp code produces IL (CIL) code. The following command opens an application that can display the compiled IL (CIL) code. Note, might require a developer command prompt to find the command. 
```
$ ildasm
```

### Dotnet commands
```
$ dotnet new webapi -n WebStore              # Create a new webapi project
$ dotnet build                               # Build the API
$ dotnet run                                 # Run the API https://localhost:5001 http://localhost:5000
$ dotnet add package <NAME>                  # Add dependencies to the project
$ dotnet tool install --global dotnet-ef     # Command to install the EF tools
$ dotnet tool update --global dotnet-ef      # Command to update the EF tools
$ dotnet ef migrations add <NAME>            # Create a migration when changes have been made in the models
$ dotnet ef migrations remove                # If the migration scripts are not to your satisfaction, undo and fix before add once again
$ dotnet ef database update                  # Perform migrations to the database
```
