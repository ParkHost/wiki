---
title: Chocolatey
description: Chocolatey
published: true
date: 2020-06-17T08:56:09.063Z
tags: chocolatey
editor: markdown
---

## Chocolatey
The Package Manager for ***Windows***.


---
- HomePage
  - https://chocolatey.org/

- Packages:
  - https://chocolatey.org/packages
---

### Installation:

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
- Installation of a Package:
```
choco install <packagename>
```
---
- Upgrade all choco packages:
```
choco upgrade all
```
---

### Install Script

```powershell
Enter here your script
```

### Template Script
This script `includes()` all my 'basic' applications:

```powershell
# Installation of Choco:
Set-ExecutionPolicy Bypass -Scope Process -Force;
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072;
iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

# Installing the following packages:
Choco install git Heroku mongodb nuclear vscode 7zip.install gimp firefox googlechrome notepadplusplus.install nodejs.install foxitreader putty.install dotnetfx winscp.install powershell-core microsoft-windows-terminal
````