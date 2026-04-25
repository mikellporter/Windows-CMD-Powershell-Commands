# Windows CMD Powershell Command List

A quick reference for common Windows CMD and PowerShell commands.

---

## 📁 File & Directory Navigation

### CMD
```cmd
cd                         :: Print current directory
dir                        :: List files in current directory
dir /a                     :: List all files including hidden
cd \path\to\folder         :: Change directory
cd ..                      :: Go up one directory
cd %USERPROFILE%           :: Go to home directory
tree                       :: Display directory tree
tree /f                    :: Display directory tree with files
```

### PowerShell
```powershell
Get-Location               # Print current directory (alias: pwd)
Get-ChildItem              # List files (aliases: ls, dir)
Get-ChildItem -Force       # List all files including hidden
Set-Location C:\path\      # Change directory (alias: cd)
```

---

## 📄 File Operations

### CMD
```cmd
type filename.txt          :: Print file contents to terminal
copy file.txt C:\path\     :: Copy a file
copy /y file.txt C:\path\  :: Copy without confirmation prompt
xcopy folder\ C:\path\ /e  :: Copy folder recursively
move file.txt C:\path\     :: Move or rename a file
del file.txt               :: Delete a file
del /f /q file.txt         :: Force delete without prompt
rmdir folder               :: Remove an empty directory
rmdir /s /q folder         :: Remove folder and all contents
ren oldname.txt newname.txt :: Rename a file
echo. > newfile.txt        :: Create a new empty file
mkdir new_folder           :: Create a new directory
mkdir a\b\c                :: Create nested directories
```

### PowerShell
```powershell
New-Item file.txt -ItemType File        # Create a new file
New-Item folder -ItemType Directory     # Create a new directory
Copy-Item file.txt C:\path\             # Copy a file
Copy-Item folder\ C:\path\ -Recurse    # Copy folder recursively
Move-Item file.txt C:\path\            # Move or rename a file
Remove-Item file.txt                    # Delete a file
Remove-Item folder -Recurse -Force     # Delete folder and contents
Rename-Item old.txt new.txt            # Rename a file
```

---

## 📖 Viewing & Editing Files

### CMD
```cmd
type file.txt              :: Print file contents (CMD)
more file.txt              :: View file with paging (CMD)
notepad file.txt           :: Open in Notepad GUI
```

### Powershell
```powershell
Get-Content file.txt               # Print file contents (alias: cat)
Get-Content file.txt -Tail 20      # Show last 20 lines
Get-Content file.txt -Head 20      # Show first 20 lines
Get-Content -Wait logfile.log      # Follow a log in real time
Set-Content file.txt "text"        # Write text to a file
Add-Content file.txt "more text"   # Append text to a file
```

---

## 🔍 Search & Find

### CMD
```cmd
dir /s /b "file.txt"               :: Search for a file by name
findstr "search_term" file.txt     :: Search for text in a file
findstr /s /i "term" *.txt         :: Search recursively, case-insensitive
where python                       :: Find the path of a command
```

### PowerShell
```powershell
Get-ChildItem -Recurse -Filter "*.log"          # Find files by name
Select-String "search_term" file.txt            # Search text in a file
Select-String -Path "*.txt" -Pattern "term"     # Search across files
Get-Command python                              # Find path of a command
```

---

## 🔐 Permissions & User Context

### CMD
```cmd
whoami                             :: Show current user
runas /user:Administrator cmd      :: Run command as administrator
icacls file.txt                    :: View file permissions
icacls file.txt /grant User:F      :: Grant full control to a user
attrib +h file.txt                 :: Hide a file
attrib -h file.txt                 :: Unhide a file
attrib +r file.txt                 :: Make a file read-only
```

### Powershell
```powershell
whoami                                          # Show current user
Start-Process cmd -Verb RunAs                   # Open CMD as Administrator
Get-Acl file.txt                                # View file permissions
Set-Acl file.txt $acl                           # Set file permissions
```

---

## 📦 Package Management

### Winget (Windows Package Manager)

### CMD
```cmd
winget search package_name         :: Search for a package
winget install package_name        :: Install a package
winget upgrade package_name        :: Upgrade a specific package
winget upgrade --all               :: Upgrade all installed packages
winget uninstall package_name      :: Uninstall a package
winget list                        :: List installed packages
```

### Chocolatey

### CMD
```cmd
choco search package_name          :: Search for a package
choco install package_name -y      :: Install a package
choco upgrade package_name         :: Upgrade a package
choco uninstall package_name       :: Uninstall a package
choco list --local-only            :: List installed packages
```

### Scoop

### CMD
```cmd
scoop search package_name          :: Search for a package
scoop install package_name         :: Install a package
scoop update package_name          :: Update a package
scoop uninstall package_name       :: Uninstall a package
scoop list                         :: List installed packages
```

---

## 🖥️ System Info & Monitoring

### CMD
```cmd
systeminfo                         :: Display detailed system info
hostname                           :: Show computer name
ver                                :: Show Windows version
winver                             :: Open Windows version popup
tasklist                           :: List all running processes
tasklist | findstr "chrome"        :: Filter process list
taskkill /PID 1234 /F              :: Force kill a process by PID
taskkill /IM chrome.exe /F         :: Force kill a process by name
wmic cpu get name                  :: Show CPU info
wmic memorychip get capacity       :: Show RAM info
```

### Powershell
```powershell
Get-ComputerInfo                            # Full system information
Get-Process                                 # List running processes
Get-Process chrome                          # Filter by process name
Stop-Process -Id 1234 -Force               # Kill a process by PID
Stop-Process -Name chrome -Force           # Kill a process by name
Get-WmiObject Win32_Processor              # CPU info
Get-WmiObject Win32_PhysicalMemory         # RAM info
Get-WmiObject Win32_OperatingSystem        # OS info
```

---

## 🌐 Networking

### CMD
```cmd
ipconfig                           :: Show IP address info
ipconfig /all                      :: Show full network details
ipconfig /flushdns                 :: Flush DNS cache
ping google.com                    :: Test network connectivity
ping -t google.com                 :: Continuous ping (Ctrl+C to stop)
tracert google.com                 :: Trace route to a host
nslookup google.com                :: DNS lookup
netstat -an                        :: Show all active connections
netstat -b                         :: Show connections with process names
curl https://example.com           :: Fetch a URL (Win10+)
```

### Powershell
```powershell
Get-NetIPAddress                            # Show IP addresses
Test-Connection google.com                  # Ping a host
Invoke-WebRequest https://example.com       # Fetch a URL (alias: curl)
Invoke-WebRequest -Uri URL -OutFile file    # Download a file
Resolve-DnsName google.com                  # DNS lookup
Get-NetTCPConnection                        # Show TCP connections
```

---

## 🗜️ Compression & Archives

### Powershell
```powershell
# ZIP
Compress-Archive -Path folder\ -DestinationPath archive.zip     # Create a zip
Expand-Archive archive.zip -DestinationPath C:\path\            # Extract a zip
Compress-Archive -Path * -DestinationPath out.zip -Update       # Update a zip

# TAR (Windows 10 1803+)
tar -czvf archive.tar.gz folder\       # Create .tar.gz archive
tar -xzvf archive.tar.gz              # Extract .tar.gz archive
```

---

## 👤 User Management

### CMD
```cmd
net user                               :: List all users
net user username                      :: Show user details
net user username password /add        :: Add a new user
net user username /delete              :: Delete a user
net localgroup administrators          :: List admin group members
net localgroup administrators username /add    :: Add user to admins
```

### Powershell
```powershell
Get-LocalUser                          # List local users
New-LocalUser "username" -Password ... # Create a new user
Remove-LocalUser "username"            # Delete a user
Get-LocalGroup                         # List local groups
Add-LocalGroupMember -Group "Administrators" -Member "username"
```

---

## 🔧 Disk & Storage

### CMD
```cmd
diskpart                               :: Open disk partition tool
chkdsk C: /f                           :: Check and fix disk errors
chkdsk C: /r                           :: Locate bad sectors and recover data
sfc /scannow                           :: Scan and repair system files
defrag C: /u /v                        :: Defragment C: drive
format D: /fs:NTFS                     :: Format a drive as NTFS
```

### Powershell
```powershell
Get-Disk                               # List all disks
Get-Partition                          # List partitions
Get-Volume                             # Show volume info and free space
Optimize-Volume -DriveLetter C -Defrag # Defragment C: drive
```

---

## 🕒 Scheduling Tasks

### CMD
```cmd
schtasks /query                        :: List all scheduled tasks
schtasks /run /tn "Task Name"          :: Run a task manually
schtasks /delete /tn "Task Name" /f    :: Delete a scheduled task

:: Create a task to run daily at 2am
schtasks /create /tn "MyTask" /tr "C:\script.bat" /sc daily /st 02:00
```

### Powershell
```powershell
Get-ScheduledTask                      # List all scheduled tasks
Start-ScheduledTask -TaskName "Name"   # Run a task manually
Unregister-ScheduledTask -TaskName "Name" -Confirm:$false  # Delete a task

# Create a task to run daily at 2am
$action = New-ScheduledTaskAction -Execute "C:\script.ps1"
$trigger = New-ScheduledTaskTrigger -Daily -At 2am
Register-ScheduledTask -Action $action -Trigger $trigger -TaskName "MyTask"
```

---

## 🛠️ Environment Variables

### CMD
```cmd
set                                    :: List all environment variables
set PATH                               :: View the PATH variable
set MYVAR=value                        :: Set a variable (current session only)
setx MYVAR "value"                     :: Set a variable permanently (user)
setx MYVAR "value" /m                  :: Set a variable permanently (system)
echo %USERPROFILE%                     :: Print a variable value
```

### Powershell
```powershell
Get-ChildItem Env:                     # List all environment variables
$env:MYVAR                             # Print a variable
$env:MYVAR = "value"                   # Set a variable (current session)
[System.Environment]::SetEnvironmentVariable("MYVAR","value","User")   # Set permanently
```

---

## 📝 Useful Shortcuts & Tricks

### CMD
```cmd
cls                                    :: Clear the terminal
doskey /history                        :: Show command history
F7                                     :: Browse command history interactively
command1 | command2                    :: Pipe output to another command
command > file.txt                     :: Redirect output to a file (overwrite)
command >> file.txt                    :: Redirect output to a file (append)
command 2> errors.txt                  :: Redirect errors to a file
command1 && command2                   :: Run command2 only if command1 succeeds
command1 || command2                   :: Run command2 only if command1 fails
start .                                :: Open current folder in File Explorer
```

### Powershell
```powershell
Clear-Host                             # Clear the terminal (alias: cls, clear)
Get-History                            # Show command history
Invoke-History 5                       # Re-run command #5 from history
$output = command                      # Capture output into a variable
command | Out-File file.txt            # Redirect output to a file
command | Tee-Object file.txt          # Output to screen AND file
```

---

## 🧰 Helpful One-Liners

### Powershell
```powershell
# Show the 10 largest files in current directory
Get-ChildItem -Recurse | Sort-Object Length -Descending | Select-Object -First 10 Name, Length

# Find files modified in the last 7 days
Get-ChildItem -Recurse | Where-Object { $_.LastWriteTime -gt (Get-Date).AddDays(-7) }

# Count lines in a file
(Get-Content file.txt).Count

# Get public IP address
(Invoke-WebRequest -Uri "https://api.ipify.org").Content

# Kill all instances of a process
Get-Process chrome | Stop-Process -Force

# List all installed programs
Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName, DisplayVersion

# Check if a port is open
Test-NetConnection -ComputerName google.com -Port 443

# Restart a Windows service
Restart-Service -Name "wuauserv" -Force
```

---

> 💡 **Tip:** Run `help command` or `command /?` in CMD for usage info. Example: `xcopy /?`
>
> 💡 **Tip:** Run `Get-Help command` in PowerShell for detailed docs. Example: `Get-Help Get-Process`
>
> 💡 **Tip:** PowerShell aliases like `ls`, `cd`, `cat`, `curl`, and `pwd` behave similarly to Linux equivalents — great for cross-platform muscle memory!
