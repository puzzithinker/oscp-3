<p align="right">
  <a href="/README.md">Home Page</a> |
  <a href="/CheatSheets/3_explore.md">Top of Page</a> |
  <a href="/CheatSheets/3_explore.md#bottom-of-page">Bottom of Page</a>
</p>

# Explore
## Table of Contents
* [Information to Gather for Privilege Escalation](#information-to-gather-for-privilege-escalation)
* [Gathering Information on a Windows System](#gathering-information-on-a-windows-system)
* [Gathering Information on a Linux System](#gathering-information-on-a-linux-system)

## Information to Gather for Privilege Escalation
| Information | Benefit to Privilege Escalation |
| ----------- | ------------------------------- |
| User Context |Establish who you are before working towards who you want to be. |
| Hostname | Discover the system’s role, naming convention, OS, etc. |
| OS Version | Find matching kernel exploits. |
| Kernel Version | Find matching kernel exploits (exploit the core of the OS). |
| System Architecture | Find matching exploits. |
| Processes and Services | Determine which are running under a privilege account and vulnerable to a known exploit and/or configured with weak permissions. |
| Network Information | Identify pivot options to other machines/networks (adapter configs, routes, TCP connections and their process owners), and determine if anti-virus or virtualization software is running. |
| Firewall Status and Rules | Determine if a service blocked remotely is allowed via loopback; find rules that allow any inbound traffic. |
| Scheduled Tasks | Identify automated tasks running under an administrator-context; find file-paths to files with weak permissions. |
| Programs and Patch Levels | Find matching exploits; HotFixId and InstalledOn represent quality of patch mgmt; qfe = quick fix engineering. |
| Readable/Writable Files and Directories | Find credentials and/or files (that run under a privileged account) that can be modified/overwritten: look for files readable and/or writable by “Everyone,” groups you’re part of, etc. |
| Unmounted Drives | Find credentials. | 
| Device Drivers and Kernel Modules | Find matching exploits. |
| AutoElevate Settings and Binaries | Find settings and/or files that run as the file owner when invoked. If AlwaysInstallElevated is enabled, exploit via a malicious .msi file. |

## Gathering Information on a Windows System
```bash
whoami # print my current user context
net user victor # print my group memberships, password policy, etc.   
net user # print other accounts on this system
hostname
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
```

## Gathering Information on a Linux System
```bash
whoami # output shows your current user context
id # print my current user context, uid, and gid
cat /etc/passwd # print other accounts on this system
hostname
cat /etc/issue # print OS version
cat /etc/*-release # print OS version
uname -a # print kernel version and system architecture
```

<p align="right">
  <a href="/README.md">Home Page</a> |
  <a href="/CheatSheets/3_explore.md">Top of Page</a> |
  <a href="/CheatSheets/3_explore.md#bottom-of-page">Bottom of Page</a>
</p>

## Bottom of Page