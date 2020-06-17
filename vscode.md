---
title: VScode
description: 
published: true
date: 2020-06-11T16:56:25.756Z
tags: 
editor: undefined
---

# Key ShortCuts:

<kbd>F2</kbd> = ~~Renames the 'variable' and everything that is referencing it.~~

# Extensions
- Auto Close Tag
- Auto Rename Tag
- Beautify
- Bracket Pair Colorizer
- Code Spell Checker
- ESLint
- FontSize Shortcuts
- Import Cost
- InstelliSense
- Just Black
- Live Server
- Material Icon Theme
- npm Intellisense
- Path Intellisense
- PowerShell
- Quokka.js
- Seti-Black
- Theme - Seti-Monokai
- Toggle Quotes
- Twig
- Vetur
- vscode-icons


---


# settings
```json
{
    "explorer.openEditors.visible": 0,
    "editor.snippetSuggestions": "top",
    "emmet.showAbbreviationSuggestions": false,
    "editor.multiCursorModifier": "ctrlCmd",
    "editor.formatOnPaste": false,
    "workbench.colorTheme": "Just Black",
    "window.zoomLevel": 0,
    "workbench.iconTheme": "vscode-icons",
    "editor.fontSize": 17,
    "editor.fontLigatures": true,
    "files.autoSave": "onFocusChange",
    "debug.console.fontFamily": "Consolas",
    "editor.tabSize": 2,
    "editor.lineHeight": 0,
    "markdown.preview.fontSize": 36,
    "editor.minimap.enabled": false,
    "eslint.enable": true,
    "eslint.validate": [
        {
            "language": "vue",
            "autoFix": true
        },
        {
            "language": "html",
            "autoFix": true
        },
        {
            "language": "javascript",
            "autoFix": true
        }
    ],
    "workbench.startupEditor": "newUntitledFile",
    "editor.suggestSelection": "first",
    "[javascript]": {
        "editor.defaultFormatter": "HookyQR.beautify"
    },
    "[json]": {
        "editor.defaultFormatter": "vscode.json-language-features"
    },
    "[html]": {
        "editor.defaultFormatter": "HookyQR.beautify"
    },
    "[css]": {
        "editor.defaultFormatter": "HookyQR.beautify"
    },
    "liveshare.featureSet": "insiders",
    "extensions.ignoreRecommendations": false,
    "git.autofetch": true,
    "liveServer.settings.donotShowInfoMsg": true,
    "terminal.integrated.shell.windows": "C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
    "terminal.integrated.fontSize": 13,
    "[jsonc]": {
        "editor.defaultFormatter": "HookyQR.beautify"
    },
}
```