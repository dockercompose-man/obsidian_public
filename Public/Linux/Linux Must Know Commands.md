**env** – displays the environment variables for the currently logged-in user
**echo** – echo a line of text on screen. Ie: echo $PATH
**top** – displays a list of all applications and processes currently running on the system.
**which** – display the full path to a shell command or utility. Ie: which ls
**whoami** – displays the username of the currently logged-in user
**netstat** – displays the status of the network
**route** – view or manipulate the system’s routing table
**ifconfig** – manage network boards installed in the system. Displays network config parameters.
**Uname** – returns information about your Linux System  
 -**s** Linux kernel’s name  
 -**n** System’s Hostname  
 -**r** Linux kernel’s release number  
 -**v** Linux kernel’s version number  
 -**m** System’s hardware architecture (x86_64)  
 -**p** Processor type  
 -**i** Hardware platform  
 -**o** Operating System  
 -**a** ALL of this INFORMATION  
 
**BASH and SHELL**- the full path to the shell executable – bin/bash
**CPU** – the type of CPU installed in the system. (Pentium IV = i686)
**DISPLAY** – the location where your X Windows display should be sent
**ENV** – the name of the file bash read to configure its environment – etc/bash.bash.rc
**EUID** – the user ID (UID) of the current user
**HISTFILE** – the path to the bash command history file - ~/.bash_history
**HISTSIZE** – the number of commands saved in the command history file - 1000
**HOME** – the path to the current user’s home directory
**HOST** and **HOSTNAME** – the hostname of the system
**LOGNAME** – the username of the current user
**MAIL** – the path to the current user’s mailbox file – _var_/spool/mail/username or _var/mail/username_
**MANPATH** – the path to your system’s man program
**OLDPWD** – the path to the prior current directory
**OSTYPE** – the type of operating system currently being run
**PATH** – a list of directories to be searched when running a command from the shell prompt
**PSI** – the characters used to create the shell prompt
**PWD** – the path to the current working directory

#### **MANPAGES** (Manual)
```bash
echo $MANPATH _usr/share/man_
```

##### _**Manpages displays**_
Title  
Name  
Synopsis  
Description  
Author  
Reporting Bugs
Copyright
See Also**
Version Number and Revison Date
**/** = **search** in the manpages

**man -k** = search across all manual page names and descriptions to find a specific keyword.

**man -k “remove empty”**

```bash
man -k remove specific_keyword
```

**apropos** – does basically the same thing, but easier command.
**apropos remove**
```bash
apropos remove specific_keyword
```

##### Adding a path to the path variable
```bash
PATH=$PATH:/var/opt/mydb
```

**## (WARNING)** if you don’t include $PATH in your reassignment, then current directories in your path variable will be erased and replaced by the new path you specify in the command! **(WARNING)**
**##make assignment apply to all shells**
```bash
export variable
```

##### exporting path variables get set to one of the following bash configuration files:
~/.bashrc  
/etc/profile  
~/.bash_profile  
~/.bash_login  
~/.profile

##### Change your shell prompt to display the currently logged-in user, the name of the Linux host, the current time, the full path to the current working directory, and a colon by doing the following:
```bash
PS1=“[\u@\h \t \w]:”.
```

### Working with Aliases

##### View All Aliases on Linux System
```bash
alias
```

##### Create your own Alias
```bash
alias name=”command” example: alias ldir=”ls -l”
```

##### Command to Mount DVD Drive
```bash
alias mntdvd="mount –t iso9660 /dev/sr0 /media/dvd;ls –l /media/dvd"
```

#### Using Redirection and Piping

##### **stdin** – standard input. Represented by the number 0
##### **stdout** – standard output. Represented by the number 1
##### **stderr** – standard error. Represented by the number 2

##### Redirecting Output
```bash
command output>filename_or_device
```

##### tail to output to file lastmessages.log
```bash
tail /var/log/messages 1>lastmessages.log
```

##### if you don’t enter a file descriptor number in the command, the shell will assume that you want to redirect only the stout from the command. Entering the following will achieve the same result.

```bash
tail /var/log/messages > lastmessages.log
```

##### redirect both stderr and stdout to text files at the same time.
```bash
command 1>stout_filename 2> sderr_filename
```

##### send both outputs to ONE file
```bash
command 1>filename 2> &1
```

##### Redirecting Input
```bash
command < input_text_or_file.
```

##### tail var messages, sends text string
```bash
tail < /var/log/messages
```

##### specify a file is to be used as an input with the sort command
```bash
sort < words
```

### Piping Information

##### displays pages one at a time
```bash
cat /var/log/messages | more
```

##### pipes the output of the first command to the input of grep, which then searches for information that matches the specified expression  
```bash
command |grep expression
```

##### search for ifup in the output of cat
```bash
cat /var/log/messages | grep ifup
```

##### adding the more option
```bash
cat /var/log/messages | grep ifup | more
```

##### output and write to file at the same time
```bash
command | tee file_name (output.txt)  ls -l | tee output.txt
```

### Searching Commands

**less** – automatically pauses a long text file one page at a time

**head** – displays the first couple of lines of a text file on screen

**tail** – displays the last couple of lines of a text file on screen.

##### using the -f option to monitor a specific file. Example an on going log file.
```bash
tail -f /var/log/messages
```

### Finding Content within Files

##### Using Grep
```bash
grep search_expression file_name
```
##### Example
```bash
grep vnc /var/log/messages
```

##### find a line in filename.conf that contains the directive “server”
```bash
grep server /etc/filename.conf
```

-**i** ignores case when searching for the text  
-**l** displays only the names of the files that contain the matching text. It doesn’t display the actual matching line of text.  
-**n** displays matching line numbers  
-**v** displays all lines that do not contain the search string  
-**e** same as **egrep** (searches files for **extended** **regular** **expressions**, which are **strings** **consisting** of **metacharacters** and **literals**.

**Literals** are **regular** **letters** A-Z, a-z and **numbers**.

**Metacharacters** are **characters** that **do** **not** **represent** **themselves** but instead **represent** **other** **characters**.

**fgrep – (fixed-string grep)** searches files for lines that match a fixed string. Direct string comparisons to find matching lines of text in the input. Fgrep pattern filename.  

##### searches for the string server in all files in the current directory whose filename has a .c extension  
```bash
fgrep server *.c
```

#### **Finding a particular Text in a Directory**
tail $(fgrep –l 192.168 /etc/*) (tail end of files)  
```bash
tail $(fgrep -l 192.168 /etc/)
```
OR
fgrep -l 192.168 /etc/* (shows filenames)
```bash
fgrep -l 192.168 /etc/
```

```bash
sudo less /etc/group | grep username
```

##### View all entries in your system log that contain the word “kernel” by piping the output from cat to grep.
```bash
cat /var/log/messages | grep kernel
```

##### The output from the preceeding command was probably very long. Pipe the output from cat to grep to more by entering
```bash
cat /var/log/messages | grep kernel | more
```

##### Send the output from the preceding command to the screen and to a file named kernel.txt
```bash
cat /var/log/messages | grep kernel | tee ~/kernel.txt
```

#### Searching through a file with less, head and tail the cat command

**less** - The less _filename_ command can also be used to display the specified text file on screen, much like cat. However, the less command automatically pauses a long text file one page at a time. You can use the SPACEBAR, PAGE UP, PAGE DOWN, and ARROW keys to navigate around the output.

**head** - The head _filename_ command is used to display the first couple of lines of a text file on the screen.

**tail** - The tail _filename_ command is used to display the last couple of lines of a text file onscreen. The tail command is particularly useful when displaying a log file onscreen. When viewing a log file, you usually only need to see the end of the file. You probably don’t care about log entries made several days or weeks ago. You can use tail to see just the last few log entries added to the end of the file.

The **tail** command also includes the –f option, which is very useful. You can use it to monitor the file specified in the command. If new content is added to the end of the file (such as a log file), the new lines will be displayed onscreen.

#### **Using top** (shows limited number of processes)

##### Viewing Running Processes
```bash
top
```
**pressing f displays a list of columns that you can add to the display**
**to add or remove a field press space**

#### **Using ps** (dynamically displays information)
##### View All running Processes
```bash
ps -e
```

##### Display Extended Information
```bash
ps -ef
```

##### Display Extended Information (Long Form)
```bash
ps -efl
```

### **Using free –** displays the amount of free and allocated RAM and swap memory  

##### Display memory statistics  
```bash
free -m
```

##### Display Totals for Each Category of information
```bash
free -mt
```

### **Using pgrep –** grepping the ps command

##### View Name of Processes as well as PID
```bash
pgrep -l -u rtracy
```

**-P** - ppid matches on the specified parent process ID
**-f** - name matches on the specified process name
**-u user_name** – matches on the specified process owner

### Using Nice

##### Set Nice Level
```bash
nice -n nice_level command
```

### Using Renice

##### Set Renice Level
```bash
renice nice_valud PID
```

### Running a program in the background

##### Append the program with an ampersand **&** character to the command
##### Example
```bash
sudo systemctl start [service] &
```

##### View Job status
```bash
jobs
```

##### Switching to foreground
```bash
fg job_ID
```

**Switching to background (First assign a foreground job, press CTRL+Z)**
```bash
bg job_ID
```

##### Keep a Process Running After Logout
###### If you have to leave now but run a script that takes hours… run, then logout
```bash
nohup updatemydb &
```

### Ending a Running Process

### Using kill and killall
##### killall lets you use the process name instead of PID

**SIGHUP** – This kill **signal 1**. **Restarts** the **process**. After a restart, the process will have exactly the same PID that it had before
**SIGINT** – This kill **signal 2**. This signal sends a **CTRL+C** key sequence to the process
**SIGKILL** – This is kill **signal 9**. This is a **brute**-**force** signal that kills the process. May not clean up after itself if this signal is used
**SIGTERM** – This is kill **signal 15**. This signal tells the process to **terminate** **immediately**. This is the **default** **signal** sent by kill if you omit a signal.

### Using pkill – is a cousin of pgrep command

##### Search through All Running Processes for those named “vi” and then send a SIGTERM signal**
```bash
pkill -SIGTERM -f vi
```

### Using the AT daemon
```bash
systemctl start atd
```

**/etc/at.allow** – users listed in this file are allowed to create at jobs
**/etc/at.deny** – users listed in this file are not allowed to create at jobs

##### If you want to run the tail /var/log/messages command in the future with at
```bash
tail /var/log/messages > ~/atoutput.txt at the at> prompt
```

##### View Pending AT Jobs
```bash
atq
```

##### Remove Jobs
```bash
atrm job_number
```

### Cron

##### **/etc/cron.hourly  
##### /etc/cron.daily  
##### /etc/cron.weekly  
##### /etc/cron.monthly**

### User Jobs
##### /var/spool/cron/tabs

##### List User’s crontab file
```bash
crontab -l
```

##### Remove a User’s crontab file
```bash
crontab -r
```


### Working with Link Files

**Hard** – a hard link is a file that points directly to the inode of another file. An inode stores basic information about a file in the Linux file system, including it’s size, device, owner and permissions.
**Symbolic** – a symbolic link file also points to another file in the file system. However, a symbolic link has is own inode. You can tell them apart.

##### To create a link file use the ln command
```bash
ln pointee_file pointer_file
```

The **bin** subdirectory of **my** **home** **directory** is **automatically** **added** to the **PATH environment variable** by my bash configuration files. By **placing** the **symbolic** **link** in this directory, I **can** **run** the **/var/opt/myapp** 
**executable** by simply **entering** **myapp** at the shell prompt

### Using Tar
##### **Extracting a tarball (-z** option use **Gzip**, **-x** option tells tar to **extract** the **files** from the decompressed archive file. **-v** option tells tar to operate **verbosely**. **-f** option tells tar the **name** **of** the **file** to extract)
```bash
tar –zxvf pure-ftpd-1.0.29.tar.gz
```



