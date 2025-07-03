
# COMMON EVENT ID SORT BY CATEGORY THAT COULD HELP DURING WINDOWS LOGGING

### Security Log: Authentication 

4624 - `User Successful Logon`:	Detect suspicious RDP/network logins and identify the attack starting point	Logged on the target machine, the one you are trying to access.

4625 - `User Failed Logon`: Detect brute force, password spraying, or vulnerability scanning	Logged on the target machine, the one you are trying to access	

4648 - `Logon attempt made with explicit credentials`

4634 - `Signal a logoff`

4768 - `Karberos Authentication Ticket (TGT) is requested`

4776 - `When computer attempt to validate the credentials of an account with domain controller`

4740 - `Indicates an account lookout`
 
### Security Log: User Management 

4720 / 4722 / 4738- `A user account was created / enabled / changed`	(Attackers might create a backdoor account or even enable an old one to avoid detection)

4725 / 4726	- `A user account was disabled / deleted`	(In some advanced cases, threat actors may disable privileged SOC accounts to slow down their actions)

4723 / 4724	- `A user changed their password /User's password was reset`	(Given enough permissions, threat actors might reset the password and then access the required user)

4732 / 4733	- `A user was added to /removed from a security group`	(Attackers often add their backdoor accounts to privileged groups like "Administrators")

### Sysmon: System Monitoring 

4688 - `Security Log: Process Creation	Log an event every time a new process is launched, including its command line and parent process details`, Limitation: Disabled by default, you need to enable it by following the official documentation

1 - `Sysmon: Process Creation)	Replace 4688 event code and provide more advanced fields like process hash and its signature`, Limitation: Sysmon is an external tool not installed by default. Check out the [Sysmon official page](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)

15 - `when a named file stream is created, and it generates events that log the hash of the contents of the file to which the stream is assigned (the unnamed stream), as well as the contents of the named stream`, (There a certain malware that their executable or configuration files via browser download, this event is aimed at capturing that based on the browser attaching a Zone.Identifier “mark of the web” stream.

### Sysmon: Files And Network 

11 / 13 - `File Create / Registry Value Set` 	(4656 for file changes and 4657 for registry changes, both disabled by default	Detect files dropped by malware or its changes to the registry (e.g. for persistence))

3 / 22 - `Network Connection / DNS Query`	(No direct alternative, requires additional firewall and DNS configuration	Detect traffic from untrusted processes or to known malicious destinations) 

### PowerShell Logging 

Effective way to log PowerShell command is via : PowerShell History, which can be locate at: 

`C:\Users\<USER>\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt`

More details and info about windows logging: 

Refference : 

[Ulltimate Windows Security](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/default.aspx?i=j)

[TryHackMe:Windows Logging for SOC](https://tryhackme.com/room/windowsloggingforsoc)
