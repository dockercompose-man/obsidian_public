##### Change User's Primary Group
```powershell
Set-LocalUser -Name <username> -PrimaryGroup <groupname>
```
##### Example
```powershell
Set-LocalUser -Name jdoe -PrimaryGroup finance
```

##### Add User to Secondary Group
```powershell
Add-ADGroupMember -Identity <groupname> -Members <username>
```
##### Example
```powershell
Add-ADGroupMember -Identity finance -Members jdoe
```

##### Change a Group's Ownership
```powershell
Get-ChildItem <path to file or directory> | ForEach-Object { $_.Group = "<groupname>"; $_ | Set-Acl }
```
##### Example
```powershell
Get-ChildItem C:\Users\example.txt | ForEach-Object { $_.Group = "finance"; $_ | Set-Acl }
```

##### View what Groups a User belongs to
```powershell
Get-ADPrincipalGroupMembership -Identity "<username>" | Select-Object Name
```
##### EXAMPLE
```powershell
Get-ADPrincipalGroupMembership -Identity "jdoe" | Select-Object Name
```

##### View if a User Exists on the System
```powershell
Get-ADUser -Identity "jdoe"
```

##### List All Users on the System
```powershell
Get-ADUser -Filter * | Select-Object -ExpandProperty Name
```
