---
title: CVE-API
description: 
published: true
date: 2020-06-15T20:23:24.397Z
tags: 
editor: undefined
---

> This Project is not maintained and still 'Under Development'.
> Any ideas or feedback are welcome.
{.is-danger}


CVE-API is my own custom API made with the data from:
https://cve.mitre.org/

**CVE.mitre** uses a public github repo which stores all vulnerabilities in json format. [Github Repo](https://github.com/CVEProject/cvelist).

As of writing ((07/06/2020) i have over **140k documents** in the DB).

# Overview

 Website: https://api-cve.now.sh

- Source = [cve.mitre - Github repo](https://github.com/CVEProject/cvelist)
- DB = MongoDB -> [MongoDB](Mongodb.com)
- API = NodeJS - Express -> [Heroku](Heroku.com)
- Front = NodeJS - Vuejs -> [Now.sh](Zeit.co)


> The most of the ***mongo*** commands are further explained [here](/MongoDB) in my mongodb section.
{.is-info}


# Bash script
These are some bash scripts i use to maintain the database.

---
## Import all json files into mongodb
This will import all CVE files into the database
Is needed to run the first time and fill up the database.
This can take up to 45 minutes.

```bash

#!/bin/bash
#Imports all json CVE files into MONGODB

# FILES=find /path/to/cvelist/ -type f -name "*.json"

for f in `find /path/to/cvelist -type f -name "*.json"`
do
        echo "Processing $f file..."
        mongoimport --db testdb --collection CVE --file $f

```
---
## MongoDB sync import
This will get all files that are new/changed and stores them in a .dat file with the current date + time:

> ***Todo:***
> - [ ] If no changes detected skip the proces
> - [ ] If reserved CVE added skipt the proces

----

```bash

#!/bin/bash
#GET ALL CHANGED FILE NAMES

cd /cd/into/your/git_repo && git fetch

CURRENTSHA="$(git rev-parse HEAD)"
NEWSHA="$(git rev-parse FETCH_HEAD)"

FILES="$(git diff --name-only ${CURRENTSHA} ${NEWSHA})"
FILENAME=/path/to/data/_"$(date +%Y%m%d%H%M)".dat

## saves the git diff (FILES) into file (FILENAME)
printf "$FILES" > "$FILENAME"

## Should be only 1 file living in this directory
## After the import the file is moved to 'archive'
DAT=`find /path/to/.dat/file*.dat`

values=`cat $DAT`

cd /path/to/cvelist && git pull

# Foreach json in the .dat file import it to mongodb
for v in $values
do
        echo "Processing $v file..."
        mongoimport --host localhost --collection CVE --upsertFields CVE_data_meta.ID  /path/to/cvelist/$v

done

# Move the .dat to archive
mv $DAT /path/to/archive/

```

-----

## Shows changes since last git pull

```bash
#!/bin/bash
#GET ALL CHANGED FILE NAMES

git fetch

CURRENTSHA="$(git rev-parse HEAD)"
NEWSHA="$(git rev-parse FETCH_HEAD)"

FILES="$(git diff --name-only ${CURRENTSHA} ${NEWSHA})"

echo "${FILES}"
echo "${FILES}" | wc -l

```

# PowerShell Script
This will get all your installed application on a Windows system and sends it to the API.
The API will filter the incoming (JSON) request so it will split into `[ApplicationName] Version`

> This is my test script, it will redirect to localhost -_-'
{.is-warning}

```powershell
$URL = 'http://localhost:3000/input'

$Apps = Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\*, HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | Select DisplayName, DisplayVersion, PSChildName
$json = [PSCustomObject][Ordered]@{ }

$more = @'
[
    {
        "ProductName":  "7-Zip 19.00 (x64)",
        "Version":  "19.00"
    },
    {
        "ProductName": "Microsoft Visual C++ 2013 Redistributable (x86) ",
        "Version":  "12.0.30501.0"
    },
    {
        "ProductName":  "Microsoft Exchange Server 2019",
        "Version":  "update"
    }
]
'@

$json = foreach ($App in $Apps) {
  if ($App.DisplayName -ne $null) {
    [ordered]@{ProductName = "$($App.DisplayName)"
      Version              = "$($App.DisplayVersion)"
    }
  }
  else {
    [ordered]@{ PSChild = "$($App.PSChildName)" 
      Version           = "$($App.DisplayVersion)"
    }
  }
}

$jsontest = @'
[
    {
        "ProductName": "Steam ",
        "Version":  "2.10.91.91"
    }
]
'@

$jsontestmessage = $jsontest

$jsonmessage = ConvertTo-Json $json -Depth 100



$parameters = @{
  "URI"         = $URL
  "Method"      = 'POST'
  "Body"        = $jsontestmessage
  "ContentType" = 'application/json'
}
 
Invoke-RestMethod @parameters


```
  
  

# Ideas
- [ ] Backend with FeatherJS
	- [ ] Mongoose as DB connection..?
- [ ] Update Front-end to VUE 3
- [ ] Automation Scripts to check your systems (Windows 10 / Server)
- [ ] Mail option

----

