---
title: Chocolatey
description: The Package Manager for Windows
published: true
date: 2020-11-18T10:36:58.322Z
tags: chocolatey
editor: markdown
dateCreated: 2020-06-04T19:41:04.170Z
---

# Overview
---
- HomePage
  - https://chocolatey.org/

- Packages:
  - https://chocolatey.org/packages
---

## Installation:

In PowerShell as Administrator:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force;
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072;
iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
---
### Usage
- Chocolatey commands always begin with:
```
choco
```
---
- Search all choco packages:
```
choco search <packagename>
```
---
- Installation of a Package:
```
choco install <packagename>
```
---
- Create your own package:
```
choco pack
```
---
- Upgrade all choco packages:
```
choco upgrade all
```
---

## Install Script

```powershell
Enter here your script
```

## Template Script
This script `includes()` all my 'basic' applications:

```powershell
# Installation of Choco:
Set-ExecutionPolicy Bypass -Scope Process -Force;
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072;
iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

# Installing the following packages:
Choco install `
git Heroku mongodb vscode 7zip.install discord nextcloud-client `
gimp firefox googlechrome notepadplusplus.install nodejs.install `
foxitreader putty.install dotnetfx winscp.install powershell-core `
microsoft-windows-terminal rocketchat logitechgaming postman `
microsoft-teams.install  microsoft-office-deployment
````