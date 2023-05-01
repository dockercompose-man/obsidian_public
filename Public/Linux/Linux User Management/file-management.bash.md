#### **Checksums**

##### Create Checksums (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
#MD5
```bash
md5sum <filename>
```
#SHA256
```bash
sha256sum <filename>
```
#SHA512
```bash
sha512sum <filename>
```
##### Check Checksums (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
#MD5 
```bash
md5sum -c <checksum_file>
```
#SHA256 
```bash
sha256sum -c <checksum_file>
```
#SHA512 
```bash
sha512sum -c <checksum_file>
```

##### Create Checksums WILDCARD (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
#MD5 
```bash
md5sum /path/to/files/* > /path/to/checksum/file.md5
```
OR
```bash
md5sum /path/to/files/*.txt > /path/to/checksum/file.md5
```
#SHA256 
```bash
sha256sum /path/to/files/* > /path/to/checksum/file.sha256
```
OR
```bash
sha256sum /path/to/files/*.txt > /path/to/checksum/file.sha256
```
#SHA512 
```bash
sha512sum /path/to/files/* > /path/to/checksum/file.sha512
```
OR
```bash
sha512sum /path/to/files/*.txt > /path/to/checksum/file.sha512
```

##### Check WILDCARD Checksums (Debian/Ubuntu, OpenSUSE, RHEL/Oracle/Rocky 9)
#MD5 
```powershell
find /path/to/directory -name "filename_pattern*" -type f -exec md5sum {} \;
```
OR
```powershell
find /path/to/directory -name "filename_pattern*.txt" -type f -exec md5sum {} \;
```
#SHA256 
```powershell
find /path/to/directory -name "filename_pattern*" -type f -exec sha256sum {} \;
```
OR
```powershell
find /path/to/directory -name "filename_pattern*.txt" -type f -exec sha256sum {} \;
```
#SHA512 
```powershell
find /path/to/directory -name "filename_pattern*" -type f -exec sha512sum {} \;
```
OR
```powershell
find /path/to/directory -name "filename_pattern*.txt" -type f -exec sha512sum {} \;
```

##### Finding Files in the Linux File System
```bash
find path -name “filename”
```
##### Example
```bash
find / -name “*.log”
```

##### Using Locate
```bash
locate filename
```
##### Using Which
```bash
which ls
```
##### Using Whereis
```bash
whereis -b ls
```
##### Using Type
```bash
type cat
```
##### Using -a return all instances of the specified command in the file system
```bash
type -a ip
```
