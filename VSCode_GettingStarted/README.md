# To Install

- .NET Core 3.1: https://dotnet.microsoft.com/download/dotnet-core/3.1

- Visual Studio Code: https://code.visualstudio.com/

- Install extensions for Visual Studio Code:
    - C# for Visual Studio Code (powered by OmniSharp)
    - vscode-icons
    - Visual Studio IntelliCode
    - NuGet Package Manager
    - GitLens
    - Live Share

# Getting Started with C#

- Open Visual Studio in the solution folder

- Open the terminal

![Open Terminal](https://github.com/quervernetzt/wcis/blob/master/VSCode_GettingStarted/resources/open-terminal.png)

- Create a new solution
    - `dotnet new sln -n "vscodeintro"`

- Create two new projects within the solution
    - `dotnet new console -n "project1"`
    - `dotnet new console -n "project2"`

- Update SLN to reference the projects
    - `dotnet sln vscodeintro.sln add ./project1/project1.csproj`
    - `dotnet sln vscodeintro.sln add ./project2/project2.csproj`


# Set the solution up for debugging

- Close VS Code and restart on the solution level

- After a short time you are asked to add required assets -> click yes
    - This will add the following assets

![Required Assets](https://github.com/quervernetzt/wcis/blob/master/VSCode_GettingStarted/resources/required-assets.png)

- Go to `tasks.json` and edit it like the following

```
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build1",
            "command": "dotnet",
            "type": "process",
            "args": [
                "build",
                "${workspaceFolder}/project1/project1.csproj",
                "/property:GenerateFullPaths=true",
                "/consoleloggerparameters:NoSummary"
            ],
            "problemMatcher": "$msCompile"
        },
        {
            "label": "build2",
            "command": "dotnet",
            "type": "process",
            "args": [
                "build",
                "${workspaceFolder}/project2/project2.csproj",
                "/property:GenerateFullPaths=true",
                "/consoleloggerparameters:NoSummary"
            ],
            "problemMatcher": "$msCompile"
        }
    ]
}
```

- Go to `launch.json` and edit it like the following

```
{
    // Use IntelliSense to find out which attributes exist for C# debugging
    // Use hover for the description of the existing attributes
    // For further information visit https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger-launchjson.md
    "version": "0.2.0",
    "configurations": [
        {
            "name": "project1",
            "type": "coreclr",
            "request": "launch",
            "preLaunchTask": "build1",
            // If you have changed target frameworks, make sure to update the program path.
            "program": "${workspaceFolder}/project1/bin/Debug/netcoreapp3.1/project1.dll",
            "args": [],
            "cwd": "${workspaceFolder}/project1",
            // For more information about the 'console' field, see https://aka.ms/VSCode-CS-LaunchJson-Console
            "console": "externalTerminal",
            "stopAtEntry": false
        },
        {
            "name": "project2",
            "type": "coreclr",
            "request": "launch",
            "preLaunchTask": "build2",
            // If you have changed target frameworks, make sure to update the program path.
            "program": "${workspaceFolder}/project2/bin/Debug/netcoreapp3.1/project2.dll",
            "args": [],
            "cwd": "${workspaceFolder}/project2",
            // For more information about the 'console' field, see https://aka.ms/VSCode-CS-LaunchJson-Console
            "console": "externalTerminal",
            "stopAtEntry": false
        }
    ]
}
```

# Work with the projects

- Go to `.\project1\Programs.cs` and replace `Console.WriteLine("Hello World!");` with

```
Console.WriteLine("Hello World1!");
Console.ReadKey();
```

- Do the same for `project2`

- Go to `Debug and Run`, select each project and run it

![Debug](https://github.com/quervernetzt/wcis/blob/master/VSCode_GettingStarted/resources/debug.png)


# Add NuGet packages

- Via the terminal
    - Move to the project folder
    - Enter `dotnet add package <packageName>`

- Via the extension
    - Open the command palette
    - Enter `NuGet` and follow the options

- Then run `dotnet restore`

# Resource

[1] [.NET Core command-line interface (CLI) tools](https://docs.microsoft.com/en-us/dotnet/core/tools/?tabs=netcore2x)