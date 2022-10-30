# Windows Terminal Configurations
A living document containing my Windows Terminal config.

## Note
This used to be a private repo but i changed it to be public because of ease of access for me. Use it as a reference if you like it but `i am not accountable for what happens when you execute commands in your environment`, use with causion and Google commands that you don't know.

## Windows Terminal JSON
```json
{
    "$help": "https://aka.ms/terminal-documentation",
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "actions": [
        {
            "command": "paste",
            "keys": "ctrl+v"
        },
        {
            "command": "copy",
            "keys": "ctrl+c"
        },
        {
            "command": {
                "action": "splitPane",
                "split": "down",
                "splitMode": "duplicate"
            },
            "keys": "alt+shift+h"
        },
        {
            "command": {
                "action": "splitPane",
                "split": "right",
                "splitMode": "duplicate"
            },
            "keys": "alt+shift+v"
        },
        {
            "command": "closePane",
            "keys": "alt+shift+w"
        },
        {
            "command": "newTab",
            "keys": "ctrl+t"
        },
        {
            "command": "closeTab",
            "keys": "ctrl+shift+t"
        }
    ],
    "copyFormatting": "none",
    "copyOnSelect": false,
    "defaultProfile": "{14ad203f-52cc-4110-90d6-d96e0f41b64d}",
    "profiles": {
        "defaults": {
            "backgroundImageStretchMode": "uniformToFill",
            "colorScheme": "Qulle",
            "cursorShape": "filledBox",
            "font": {
                "face": "Cascadia Code PL",
                "size": 14
            },
            "opacity": 100,
            "useAcrylic": true,
            "startingDirectory": "%USERPROFILE%"
        },
        "list": [
            {
                "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                "hidden": false,
                "name": "Windows PowerShell"
            },
            {
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "hidden": false,
                "name": "Command Prompt"
            },
            {
                "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
                "hidden": false,
                "name": "Azure Cloud Shell",
                "source": "Windows.Terminal.Azure"
            },
            {
                "commandline": "C:/Program Files/Git/bin/bash.exe --login",
                "guid": "{14ad203f-52cc-4110-90d6-d96e0f41b64d}",
                "icon": "%SystemDrive%\\Program Files\\Git\\mingw64\\share\\git\\git-for-windows.ico",
                "name": "Git Bash"
            },
            {
                "guid": "{c6eaf9f4-32a7-5fdc-b5cf-066e8a4b1e40}",
                "hidden": false,
                "name": "Ubuntu-18.04",
                "source": "Windows.Terminal.Wsl"
            },
            {
                "commandline": "cmd.exe /k \"C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\Community\\Common7\\Tools\\VsDevCmd.bat\"",
                "cursorColor": "#EBCB8B",
                "guid": "{876c122b-32d8-4e72-a746-3b00f929744a}",
                "hidden": false,
                "icon": "C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\Community\\Common7\\Tools\\developer-console.png",
                "name": "Windows Developer Console"
            },
            {
                "guid": "{4ca3f36a-954b-5f17-a131-52dc5790981e}",
                "hidden": false,
                "name": "Ubuntu 18.04.5 on Windows",
                "source": "CanonicalGroupLimited.Ubuntu18.04onWindows_79rhkp1fndgsc"
            },
            {
                "guid": "{3a2240ca-36ff-5c25-af25-5f0ef99a4f77}",
                "hidden": false,
                "name": "Developer Command Prompt for VS 2022",
                "source": "Windows.Terminal.VisualStudio"
            },
            {
                "guid": "{cefd7af5-b4ce-56d6-a8f5-39d320521b69}",
                "hidden": false,
                "name": "Developer PowerShell for VS 2022",
                "source": "Windows.Terminal.VisualStudio"
            }
        ]
    },
    "schemes": [
        {
            "name": "Qulle",
            "black": "#222222",
            "red": "#e66363",
            "green": "#8add34",
            "yellow": "#e6d463",
            "blue": "#63c7e2",
            "purple": "#5b9ccf",
            "cyan": "#1ecfbe",
            "white": "#02c5e0",
            "brightBlack": "#ffffff",
            "brightRed": "#c4556f",
            "brightGreen": "#beffa8",
            "brightYellow": "#d0ccca",
            "brightBlue": "#7ab0d2",
            "brightPurple": "#c5a7d9",
            "brightCyan": "#8cdfe0",
            "brightWhite": "#e0e0e0",
            "background": "#2d3336",
            "foreground": "#63c7e2",
            "selectionBackground": "#63c7e2",
            "cursorColor": "#63c7e2"
        },
        {
            "name": "Dracula",
            "background": "#131C28",
            "black": "#21222C",
            "blue": "#BD93F9",
            "brightBlack": "#6272A4",
            "brightBlue": "#D6ACFF",
            "brightCyan": "#A4FFFF",
            "brightGreen": "#69FF94",
            "brightPurple": "#FF92DF",
            "brightRed": "#FF6E6E",
            "brightWhite": "#F8F8F2",
            "brightYellow": "#FFFFA5",
            "cursorColor": "#EBCB8B",
            "cyan": "#8BCAFD",
            "foreground": "#F8F8F2",
            "green": "#50FA7B",
            "purple": "#FF79C6",
            "red": "#FF5555",
            "selectionBackground": "#FFFFFF",
            "white": "#F8F8F2",
            "yellow": "#FFB86C"
        }
    ]
}
```
