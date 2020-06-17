---
title: Windows Terminal
description: 
published: true
date: 2020-06-04T19:23:39.157Z
tags: 
editor: undefined
---

# Windows Terminal
## Installation:

- From (Windows) PowerShell (Core) as administrator:
```powershell
choco install microsoft-windows-terminal
```

## background-image:

![Alt Text](https://media.giphy.com/media/gjs3yK6xuIDIzVqryI/giphy.gif)


## Settings:

```json
// To view the default settings, hold "alt" while clicking on the "Settings" button.
// For documentation on these settings, see: https://aka.ms/terminal-documentation

{
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "requestedTheme": "dark",


    "defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
    "closeOnExit": true,

    "wordDelimiters": " |\u2502;/\\",
    "copyOnSelect": true,

    "profiles": {
        "defaults": {
            "backgroundImageStretchMode" : "uniformToFill",
            "background": "#2b2b2b",
            "backgroundImage": "C:/Users/%username%/Documents/Windows Terminal/universe.gif",
            "backgroundImageOpacity" : 0.2,
            "padding": "4, 4, 4, 4",
            "fontFace": "Cascadia Code PL",
            "fontSize": 13,
            "startingDirectory": "%__CD__%"
        },
        "list": [{
                "guid": "{58ad8b0c-3ef8-5f4d-bc6f-13e4c00f2530}",
                "hidden": false,
                "name": "Debian",
                "tabTitle": "Linux: Debian",
                "source": "Windows.Terminal.Wsl",
                "padding": "8, 8, 8, 8",
                "fontFace": "Cascadia Code PL",
                "fontSize": 12
            },
            {
                // Make changes here to the powershell.exe profile
                "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                "name": "Windows PowerShell",
                "tabTitle": "PowerHell",
                "commandline": "powershell.exe",
                "fontFace": "Cascadia Code PL",
                "hidden": false
            },
            {
                // Make changes here to the cmd.exe profile
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "name": "cmd",
                "tabTitle": "OldSkool",
                "commandline": "cmd.exe",
                "hidden": false
            },
            {
                "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
                "hidden": false,
                "name": "Azure Cloud Shell",
                "tabTitle": "Azure Shell",
                "source": "Windows.Terminal.Azure"
            },
            {
                "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
                "hidden": false,
                "name": "PowerShell",
                "tabTitle": "PowerHell Core",
                "source": "Windows.Terminal.PowershellCore"
            }
        ]
    },

    // Add custom color schemes to this array
    "schemes": [],

    // Add any keybinding overrides to this array.
    // To unbind a default keybinding, set the command to "unbound"
    "keybindings": []
}
```