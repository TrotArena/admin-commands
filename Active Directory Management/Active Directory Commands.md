# System Information and Hardware Details

**Description:**
Retrieve essential system information and hardware details with a single command. Discover your computer's hostname, operating system name, total physical memory, system boot time, system uptime, logical disk information (including free space), and CPU specifications. Gain valuable insights into your system's configuration and performance effortlessly.

## Command:
```shell
systeminfo | findstr /C:"Host Name" /C:"OS Name" /C:"Total Physical Memory" /C:"System Boot Time" /C:"System Up Time" & wmic logicaldisk get caption,description,freespace,size & wmic cpu get name, maxclockspeed & ipconfig /all | findstr /C:"DNS Servers" /C:"NetBIOS over Tcpip" /C:"IPv4 Address" /C:"Subnet Mask" /C:"DHCP Enabled" /C:"Autoconfiguration Enabled" /C:"Connection-specific DNS Suffix" & whoami
```
### Check for Windows Updates
```
wuauclt /detectnow
```
### Check Disk Utility
```
chkdsk C: /f
```
### System File Checker
```
sfc /scannow
```
### Restart or Shutdown the Computer
```
shutdown /r /t 0
```
### Control Panel
```
control
```
### Task Manager
```
taskmgr
```
### Command Prompt as Administrator
```
runas /user:Administrator cmd
```
### Windows Firewall Settings
```
firewall.cpl
```
### File Explorer (Open Current Directory)
```
start .
```
### Notepad (Open a Text File)
```
notepad filename.txt
```
### Add User to Administrator Group
```
net localgroup administrators username /add
```
### Find Files or Directories Containing a Specific Term
```
dir C:\ /s /b | findstr /i "search_term"
```
### Find Path of Specific Process by Name
```
wmic process where "name='process_name'" get executablepath
```
