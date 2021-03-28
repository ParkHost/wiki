---
title: PowerShell
description: 
published: true
date: 2021-03-28T08:41:58.040Z
tags: scripting, windows, microsoft, powershell, automation
editor: markdown
dateCreated: 2020-06-15T20:11:47.768Z
---

![powershell[1].png](/powershell[1].png =125x120){.align-left} is the Windows automation and configuration management framework.
You can use it within the shell or as scripting `.ps1` 

PowerShell is a cross-platform task automation and configuration management framework, consisting of a command-line shell and scripting language.

---
# Requirements

Regular Expresion in Powershell is `powerfull`.

# Commands
## -Match (param)

[Comparison Operators](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-7.1)
```powershell
-match
# icw
$matches
```

## Split-Path
[Split-Path](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/split-path?view=powershell-7)
```powershell
Split-Path
#parameter:
-leaf

# Indicates that this cmdlet returns only the last item or container in the path.
# For example, in the path C:\Test\Logs\Pass1.log, it returns only Pass1.log. 

```

# ConvertTo-HashTable

```powershell
function ConvertTo-HashTable {
    [CmdletBinding()]
    param (
        [Parameter(Mandatory = $true)][PSCustomObject]$psCustomObject
    )
    $output = @{}
    foreach ($note in ($psCustomObject.psobject.Members).Where( { $_.MemberType -eq 'NoteProperty' })) {
        $output.add($note.name, $note.value)
    }
    return $output
}
```

# Unique identify the host
In some use cases you need to identify a host on a unique (static) value.
Following command gives a `4K hash` in Windows 10 **ONLY**

(Get-CimInstance -Namespace root/cimv2/mdm/dmmap -Class MDM_DevDetail_Ext01 -Filter "InstanceID='Ext' AND ParentID='./DevDetail'").DeviceHardwareData
```  

# winUpdate script

```powershell
$ErrorActionPreference = "Stop"

#set variables:
[string]$category_names # = "Security Updates" , "Critical Updates" | Comma seperated
[string] $state # = "Searched" | options: "Searched", "Downloaded", "Installed" 
[array] $blacklist # = "kb12345" , "kb54321" | Comma seperated
[array] $whitelist # = "kb12345" , "kb54321" | Comma seperated
[int] $freezeTime # = 2 | integer (cooldown period between publish date of )
# creating result object
$result = @{
  changed          = $false
  updates          = @{}
  filtered_updates = @{}
}
# Start windows Update service
if ((Get-Service -Name wuauserv).StartType -ne 'Automatic' -or (Get-Service -Name wuauserv).Status -ne 'Running') {
  try {
    Get-Service -Name wuauserv | Set-Service -StartupType Automatic -Status Running
  }
  catch {
    return "Windows Update Service not running"
  }
}
$session = New-Object -ComObject Microsoft.Update.Session
$searcher = $session.CreateUpdateSearcher()
$search_result = $searcher.Search("IsInstalled = 0")        
$updates_to_install = New-Object -ComObject Microsoft.Update.UpdateColl         
foreach ($update in $search_result.Updates) {
  try {
    $update_info = @{
      title       = $update.Title
      Description = $update.Description
      publishdate = $update.LastDeploymentChangeTime.DateTime
      kb          = $update.KBArticleIDs[0]
      id          = $update.Identity.UpdateId
      installed   = $update.IsInstalled
      categories  = @($update.Categories | ForEach-Object { $_.Name })
    }
  }
  catch {
    # Workaround if a non-KB 'update' has been found
    title         = $update.Title
    Description   = $update.Description
    publisheddate = $update.LastDeploymentChangeTime.DateTime
    id            = $update.Identity.UpdateId
    installed     = $update.IsInstalled
    categories    = @($update.Categories | ForEach-Object { $_.Name })
  }
  # validate freeze period
  if ($freezeTime) {
    $daydifferent = ((Get-Date) - $update.LastDeploymentChangeTime).TotalDays
    if ($daydifferent -le $freezeTime) {
      $update_info.filtered_reason = "freeze period"
      $result.filtered_updates[$update_info.id] = $update_info
      break
    }
  }
  # validate update against blacklist/whitelist/post_category_names/hidden
  $whitelist_match = $false
  foreach ($whitelist_entry in $whitelist.split(",").Trim()) {
    if ($update_info.title -imatch $whitelist_entry) {
      $whitelist_match = $true
      break
    }
    foreach ($kb in $update_info.kb) {
      if ("KB$kb" -imatch $whitelist_entry) {
        $whitelist_match = $true
        break
      }
    }
  }
  if ($whitelist.Length -gt 0 -and -not $whitelist_match) {
  	write-host "checking whitelist"
    $update_info.filtered_reason = "whitelist"
    $result.filtered_updates[$update_info.id] = $update_info
    continue
  }
  
  $blacklist_match = $false
  if ($blacklist.Length -gt 1 ) {
  	write-host "checking blacklist $blacklist"
    foreach ($blacklist_entry in $blacklist.split(",").Trim()) {
      if ($update_info.title -imatch $blacklist_entry) {
        $blacklist_match = $true
        break
      }
      foreach ($kb in $update_info.kb) {
        if ("KB$kb" -imatch $blacklist_entry) {
          $blacklist_match = $true
          break
        }
      }
    }
  }
  if ($blacklist_match) {
    $update_info.filtered_reason = "blacklist"
    $result.filtered_updates[$update_info.id] = $update_info
    continue
  }
  if ($update.IsHidden) {
    $update_info.filtered_reason = "skip_hidden"
    $result.filtered_updates[$update_info.id] = $update_info
    continue
  }
  $category_match = $false
  foreach ($match_cat in $category_names.split(",").Trim()) {
    write-host "match_cat is: "$match_cat
    if ($update_info.categories -ieq $match_cat) {
      $category_match = $true
      #DEBUG: write-host "match_cat is: "$match_cat
      break
    }
  }
  if ($category_names.Length -gt 0 -and -not $category_match) {
    write-host "checking category $($category_names)"
    $update_info.filtered_reason = "category_names"
    $result.filtered_updates[$update_info.id] = $update_info
    continue
  }
  if (-not $update.EulaAccepted) {
    try {
      $update.AcceptEula()
    }
    catch {
      $result.failed = $true
      $result.msg = "Failed to accept EULA for update $($update_info.id) - $($update_info.title)"
      return ConvertTo-Json -InputObject $result -Depth 99
    }
  }
  if ($update_info.Count -gt 0) {
    $updates_to_install.Add($update) > $null
  }
  else {
    $result.msg = "No updates found"
    return ConvertTo-Json -InputObject $result -Depth 99
  }
  $result.updates[$update_info.id] = $update_info
}
$result.reboot_required = (New-Object -ComObject Microsoft.Update.SystemInfo).RebootRequired
$result.found_update_count = $updates_to_install.Count
$result.installed_update_count = 0

if ($check_mode -or $state -eq "Searched") {
  if ($updates_to_install.Count -gt 0 -and ($state -ne "Searched")) {
    $result.changed = $true
  }
  return ConvertTo-Json -InputObject $result -Depth 99
}
if ($updates_to_install.Count -gt 0) {
  if ($result.reboot_required) {
    $result.failed = $true
    $result.msg = "A reboot is required before more updates can be installed"
    return ConvertTo-Json -InputObject $result -Depth 99
  }
}
else {
  # no updates to install exit here
  $result.msg = "No updates found"
  return ConvertTo-Json -InputObject $result -Depth 99
}
if ($updates_to_install.Count -gt 0) {
  if ($result.reboot_required) {
    $result.failed = $true
    $result.msg = "A reboot is required before more updates can be installed"
    return ConvertTo-Json -InputObject $result -Depth 99
  }
}
else {
  # no updates to install exit here
  return ConvertTo-Json -InputObject $result -Depth 99
}
$update_index = 1
foreach ($update in $updates_to_install) {
  $update_number = "($update_index of $($updates_to_install.Count))"
  if ($update.IsDownloaded) {
    $update_index++
    continue
  }
  try {
    $dl = $session.CreateUpdateDownloader()
  }
  catch {
    $result.failed = $true
    $result.msg = "Failed to create downloader object: $($_.Exception.Message)"
    return ConvertTo-Json -InputObject $result -Depth 99
  }
  try {
    $dl.Updates = New-Object -ComObject Microsoft.Update.UpdateColl
  }
  catch {
    $result.failed = $true
    $result.msg = "Failed to create download collection object: $($_.Exception.Message)"
    return ConvertTo-Json -InputObject $result -Depth 99
  }
  $dl.Updates.Add($update) > $null
  try {
    $download_result = $dl.Download()
  }
  catch {
    $result.failed = $true
    $result.msg = "Failed to download update $update_number $($update.Identity.UpdateId) - $($update.Title): $($_.Exception.Message)"
    return ConvertTo-Json -InputObject $result -Depth 99
  }
  # FUTURE: configurable download retry
  if ($download_result.ResultCode -ne 2) {
    # OperationResultCode orcSucceeded
    $result.failed = $true
    $result.msg = "Failed to download update $update_number $($update.Identity.UpdateId) - $($update.Title): Download Result $($download_result.ResultCode)"
    return ConvertTo-Json -InputObject $result -Depth 99
  }
  $result.changed = $true
  $update_index++
}
# Early exit for download-only
if ($state -eq "Downloaded") {
  $result.failed = $false
  $result.msg = "Downloaded $($updates_to_install.Count) updates"
  return ConvertTo-Json -InputObject $result -Depth 99
}
# install as a batch so the reboot manager will suppress intermediate reboots
try {
  $installer = $session.CreateUpdateInstaller()
}
catch {
  $result.failed = $true
  $result.msg = "Failed to create Update Installer object: $($_.Exception.Message)"
  return ConvertTo-Json -InputObject $result -Depth 99
}
try {
  $installer.Updates = New-Object -ComObject Microsoft.Update.UpdateColl
}
catch {
  $result.failed = $true
  $result.msg = "Failed to create Update Collection object: $($_.Exception.Message)"
  return ConvertTo-Json -InputObject $result -Depth 99
}
foreach ($update in $updates_to_install) {
  $installer.Updates.Add($update) > $null
}
# FUTURE: use BeginInstall w/ progress reporting so we can at least log intermediate install results
if ($update_info.id) {
  try {
    $install_result = $installer.Install() 
  }
  catch {
    $result.failed = $true
    $result.msg = "Failed to install update from Update Collection: $($_.Exception.Message)"
    return ConvertTo-Json -InputObject $result -Depth 99
  }
}
$update_success_count = 0
$update_fail_count = 0
# WU result API requires us to index in to get the install results
$update_index = 0
foreach ($update in $updates_to_install) {
  $update_number = "($($update_index + 1) of $($updates_to_install.Count))"
  try {
    $update_result = $install_result.GetUpdateResult($update_index)
  }
  catch {
    $result.failed = $true
    $result.msg = "Failed to get update result for update $update_number $($update.Identity.UpdateID) - $($update.Title): $($_.Exception.Message)"
    return ConvertTo-Json -InputObject $result -Depth 99
  }
  $update_resultcode = $update_result.ResultCode
  $update_hresult = $update_result.HResult
  $update_index++
  $update_dict = $result.updates[$update.Identity.UpdateID]
  if ($update_resultcode -eq 2) {
    # OperationResultCode onSucceeded
    $update_success_count++
    $update_dict.installed = $true
  }
  else {
    $update_fail_count++
    $update_dict.installed = $false
    $update_dict.failed = $true
    $update_dict.failure_hresult_code = $update_hresult
  }
}
$result.reboot_required = (New-Object -ComObject Microsoft.Update.SystemInfo).RebootRequired
$result.installed_update_count = $update_success_count
$result.failed_update_count = $update_fail_count
if ($updates_success_count -gt 0) {
  $result.changed = $true
}
if ($update_fail_count -gt 0) {
  $result.failed = $true
  $result.msg = "Failed to install one or more updates"
  return ConvertTo-Json -InputObject $result -Depth 99
}
return ConvertTo-Json -InputObject $result -Depth 99
```