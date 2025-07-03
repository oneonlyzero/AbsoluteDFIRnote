## Windows Log Event ID 

### Security Log: Authentication 

4624 - `User Successful Logon`:	Detect suspicious RDP/network logins and identify the attack starting point	Logged on the target machine, the one you are trying to access	Noisy. You will see hundreds of logon events per minute on loaded servers

4625 - `User Failed Logon`:	Detect brute force, password spraying, or vulnerability scanning	Logged on the target machine, the one you are trying to access	Inconsistent. The logs have lots of caveats that may trick you into the wrong understanding of the event

### Security Log: User Management 

Event ID	Description	Malicious Usage
4720 / 4722 / 4738	A user account was
created / enabled / changed	Attackers might create a backdoor account or even enable an old one to avoid detection 
4725 / 4726	A user account was
disabled / deleted	In some advanced cases, threat actors may disable privileged SOC accounts to slow down their actions
4723 / 4724	A user changed their password /
User's password was reset	Given enough permissions, threat actors might reset the password and then access the required user
4732 / 4733	A user was added to /
removed from a security group	Attackers often add their backdoor accounts to privileged groups like "Administrators"

### Sysmon: System Monitoring 

Event Code	Purpose	Limitations
4688
(Security Log: Process Creation)	Log an event every time a new process is launched, including its command line and parent process details	Disabled by default, you need to enable it by following the official documentation
1
(Sysmon: Process Creation)	Replace 4688 event code and provide more advanced fields like process hash and its signature	Sysmon is an external tool not installed by default. Check out the [Sysmon official page](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)

### Sysmon: Files And Network 

Event ID	Security Log Alternative	Event Purpose
11 / 13
(File Create / Registry Value Set)	4656 for file changes and 4657 for registry changes, both disabled by default	Detect files dropped by malware or its changes to the registry (e.g. for persistence) 
3 / 22
(Network Connection / DNS Query)	No direct alternative, requires additional firewall and DNS configuration	Detect traffic from untrusted processes or to known malicious destinations

### PowerShell Logging 

PowerShell History File
There are at least five methods to monitor PowerShell, each with its own pros and cons. While you can check out the Logless Hunt room and research AMSI and Transcript Logging topics, in this room, we will focus on a simple but effective way to track PowerShell commands - the PowerShell history file:

C:\Users\<USER>\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt






Refference : 

[TryHackMe:Windows Logging for SOC](https://tryhackme.com/room/windowsloggingforsoc)
