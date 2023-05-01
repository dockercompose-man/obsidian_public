##### Create Checksum
#MD5 
```powershell
Get-FileHash <filename> -Algorithm MD5 | Select-Object -ExpandProperty Hash
```
#SHA256 
```powershell
Get-FileHash <filename> -Algorithm SHA256 | Select-Object -ExpandProperty Hash
```
#SHA512 
```powershell
Get-FileHash <filename> -Algorithm SHA512 | Select-Object -ExpandProperty Hash
```

##### Check a Checksum
#MD5 
```powershell
(Get-FileHash <filename> -Algorithm MD5).Hash -eq (Get-Content <checksum_file>)
```
#SHA256 
```powershell
(Get-FileHash <filename> -Algorithm SHA256).Hash -eq (Get-Content <checksum_file>)
```
#SHA512 
```powershell
(Get-FileHash <filename> -Algorithm SHA512).Hash -eq (Get-Content <checksum_file>)
```

##### Create Checksum WILDCARD
#MD5 
```powershell
Get-ChildItem -Path "C:\path\to\files\*" | ForEach-Object { Get-FileHash $_.FullName -Algorithm MD5 } | Out-File -FilePath "C:\path\to\checksum\file.md5"
```
OR
```powershell
Get-ChildItem -Path "C:\path\to\files\*.txt" | ForEach-Object { Get-FileHash $_.FullName -Algorithm MD5 } | Out-File -FilePath "C:\path\to\checksum\file.md5"
```
#SHA256 
```powershell
Get-ChildItem -Path "C:\path\to\files\*" | ForEach-Object { Get-FileHash $_.FullName -Algorithm SHA256 } | Out-File -FilePath "C:\path\to\checksum\file.sha256"
```
OR
```powershell
Get-ChildItem -Path "C:\path\to\files\*.txt" | ForEach-Object { Get-FileHash $_.FullName -Algorithm SHA256 } | Out-File -FilePath "C:\path\to\checksum\file.sha256"
```
#SHA512 
```powershell
Get-ChildItem -Path "C:\path\to\files\*" | ForEach-Object { Get-FileHash $_.FullName -Algorithm SHA512 } | Out-File -FilePath "C:\path\to\checksum\file.sha512"
```
OR
```powershell
Get-ChildItem -Path "C:\path\to\files\*.txt" | ForEach-Object { Get-FileHash $_.FullName -Algorithm SHA512 } | Out-File -FilePath "C:\path\to\checksum\file.sha512"
```

##### Check WILDCARD Checksums
#MD5 
```powershell
Get-ChildItem -Path "C:\path\to\files\*" -Recurse | ForEach-Object { If ((Get-FileHash $_.FullName -Algorithm MD5).Hash -ne (Get-Content "C:\path\to\checksum\file.md5" | Where-Object { $_ -match $_.Name })[0].Substring(0, 32)) { Write-Host "$($_.FullName) failed MD5 checksum verification" } }
```
OR
```powershell
Get-ChildItem -Path "C:\path\to\files\*.txt" -Recurse | ForEach-Object { If ((Get-FileHash $_.FullName -Algorithm MD5).Hash -ne (Get-Content "C:\path\to\checksum\file.md5" | Where-Object { $_ -match $_.Name })[0].Substring(0, 32)) { Write-Host "$($_.FullName) failed MD5 checksum verification" } }
```
#SHA256 
```powershell
Get-ChildItem -Path "C:\path\to\files\*" -Recurse | ForEach-Object { If ((Get-FileHash $_.FullName -Algorithm SHA256).Hash -ne (Get-Content "C:\path\to\checksum\file.sha256" | Where-Object { $_ -match $_.Name })[0].Substring(0, 64)) { Write-Host "$($_.FullName) failed SHA256 checksum verification" } }
```
OR
```powershell
Get-ChildItem -Path "C:\path\to\files\*.txt" -Recurse | ForEach-Object { If ((Get-FileHash $_.FullName -Algorithm SHA256).Hash -ne (Get-Content "C:\path\to\checksum\file.sha256" | Where-Object { $_ -match $_.Name })[0].Substring(0, 64)) { Write-Host "$($_.FullName) failed SHA256 checksum verification" } }
```
#SHA512 
```powershell
Get-ChildItem -Path "C:\path\to\files\*" -Recurse | ForEach-Object { If ((Get-FileHash $_.FullName -Algorithm SHA512).Hash -ne (Get-Content "C:\path\to\checksum\file.sha512" | Where-Object { $_ -match $_.Name })[0].Substring(0, 128)) { Write-Host "$($_.FullName) failed SHA512 checksum verification" } }
```
OR
```powershell
Get-ChildItem -Path "C:\path\to\files\*.txt" -Recurse | ForEach-Object { If ((Get-FileHash $_.FullName -Algorithm SHA512).Hash -ne (Get-Content "C:\path\to\checksum\file.sha512" | Where-Object { $_ -match $_.Name })[0].Substring(0, 128)) { Write-Host "$($_.FullName) failed SHA512 checksum verification" } }
```