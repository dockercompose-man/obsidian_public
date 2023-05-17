##### Creating a new user
```powershell
New-ADUser -Name "<username>" -SamAccountName "<samaccountname>" -AccountPassword (ConvertTo-SecureString "<password>" -AsPlainText -Force) -Enabled $true
```

##### Create a new user WITH a home directory
```powershell
New-ADUser -Name "<username>" -SamAccountName "<samaccountname>" -AccountPassword (ConvertTo-SecureString "<password>" -AsPlainText -Force) -Enabled $true -HomeDrive "H:" -HomeDirectory "\\server\share\<username>"
```

##### Create a home directory AFTER the user was created
```powershell
New-Item -ItemType Directory -Path "\\server\share\<username>"
Set-ADUser -Identity "<username>" -HomeDrive "H:" -HomeDirectory "\\server\share\<username>"
```

##### Deleting a user
```powershell
Remove-ADUser -Identity "<username>"
```

##### Changing a user's password
```bash
Set-ADAccountPassword -Identity "<username>" -NewPassword (ConvertTo-SecureString "<password>" -AsPlainText -Force) -Reset
```

##### Modifying a user's properties
```powershell
Set-ADUser -Identity "<username>" <options>
```

##### Locking a User Account
```powershell
Disable-ADAccount -Identity "<username>"
```

##### Unlocking a User Account
```powershell
Enable-ADAccount -Identity "<username>"
```

##### Remove a User's Password
```powershell
Set-ADAccountPassword -Identity "<username>" -Reset -NewPassword $null
```

##### Changing a User's Default Shell
```powershell
Set-ADUser -Identity "<username>" -Shell "<path_to_shell>"
```
##### Example
```powershell
Set-ADUser -Identity "jdoe" -Shell "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe"
```

##### Changing a User's UID
```powershell
Set-ADUser -Identity "<username>" -Replace @{uidNumber="<new_uid>"}
```
##### Example
```powershell
Set-ADUser -Identity "jdoe" -Replace @{uidNumber="1001"}
```

##### Changing a User's GID
```powershell
Set-ADUser -Identity "<username>" -Replace @{gidNumber="<new_gid>"}
```
##### Example
```powershell
Set-ADUser -Identity "jdoe" -Replace @{gidNumber="1001"}
```

##### Changing a user's Username
```powershell
Rename-ADObject -Identity "CN=<old_username>,<distinguished_name>" -NewName "<new_username>"
```
##### Example
```powershell
Rename-ADObject -Identity "CN=jdoe,OU=Sales,DC=example,DC=com" -NewName "jane"
```

##### Locate files owned by a specific user
```powershell
Get-ChildItem -Path "C:\" -Recurse | Where-Object { $_.PSIsContainer -eq $false -and $_.Owner -eq "<username>" }
```
##### Example
```powershell
Get-ChildItem -Path "C:\" -Recurse | Where-Object { $_.PSIsContainer
```

##### Set a User Expiry Date
```powershell
Set-ADUser -Identity "<username>" -AccountExpirationDate "<date>"
```
##### Example
```powershell
Set-ADUser -Identity "jdoe" -AccountExpirationDate "2023-03-31"
```

##### Disabling Account Expiration of a User
```powershell
Set-ADUser -Identity "<username>" -AccountExpirationDate $null
```
##### Example
```powershell
Set-ADUser -Identity "jdoe" -AccountExpirationDate $null
```

##### View Account Expiry Date
```powershell
Get-ADUser -Identity "<username>" -Properties AccountExpirationDate
```
##### Example
```powershell
Get-ADUser -Identity "jdoe" -Properties AccountExpirationDate
```

##### Archive User's Data (Cygwin, Git Bash, or GNUWin32 must be installed)
```powershell
Compress-Archive -Path "<path to user directory>" -DestinationPath "<path to archive file>.tar.gz"
```
##### Example (Cygwin, Git Bash, or GNUWin32 must be installed)
```powershell
Compress-Archive -Path "C:\Users\jdoe" -DestinationPath "C:\Users\jdoe_archive.tar.gz"
```

##### Archive User's Data (7zip must be installed)
```powershell
& "C:\Program Files\7-Zip\7z.exe" a -ttar -so "<path to user directory>" | & "C:\Program Files\7-Zip\7z.exe" a -tgzip -si "<path to archive file>.tar.gz"
```
##### Example (7zip must be installed)
```powershell
& "C:\Program Files\7-Zip\7z.exe" a -ttar -so "<path to user directory>" | & "C:\Program Files\7-Zip\7z.exe" a -tgzip -si "<path to archive file>.tar.gz"
```

##### Remove a User's Print Jobs
```powershell
Get-PrintJob -PrinterName "printer_name" -UserName "username" | Remove-PrintJob
```

##### Remove a User's Scheduled Tasks
```powershell
Unregister-ScheduledTask -TaskName "task_name" -TaskPath "\path\to\task"
```

##### List All Scheduled Tasks (on Local Computer)
```powershell
Get-ScheduledTask
```

##### List All Scheduled Tasks (on Remote Computer)
```powershell
Get-ScheduledTask -CimSession computer_name
```

##### List All Scheduled Tasks (Filtered based on criteria)
```powershell
Get-ScheduledTask | Where-Object {$_.TaskName -like "*keyword*"}
```

##### Changing User's Ownership (Full Control)
```powershell
$User = 'domain\username'
$Path = 'C:\example\file.txt'
$Acl = Get-Acl $Path
$Ar = New-Object System.Security.AccessControl.FileSystemAccessRule($User,'FullControl','Allow')
$Acl.SetOwner([System.Security.Principal.NTAccount]$User)
$Acl.SetAccessRule($Ar)
Set-Acl $Path $Acl
```
