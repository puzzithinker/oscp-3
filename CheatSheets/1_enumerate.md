<p align="right">
  <a href="/README.md">Home Page</a> |
  <a href="/CheatSheets/1_enumerate.md#">Top of Page</a> |
  <a href="/CheatSheets/1_enumerate.md#bottom-of-page">Bottom of Page</a>
</p>

# Enumerate
## Table of Contents
* [Priority of Work](#priority-of-work)
* [Nmap](#nmap)
* [FTP](#ftp)
* [NFS](#nfs)
* [SMTP](#smtp)
* [SMB](#smb)

## Priority of Work
|Priority|Protocol|Port|Provides|
|--------|--------|----|--------|
|1       |TCP     |80  |Code execution|
|2       |SMB     |445 |Credentials|
|3       |NFS     |    |Credentials|
|4       |RPC     |135 ||
|5       |SSH     |22  |Shell access|
|6       |POP3    |110 ||

## Nmap
```bash
mkdir nmap
sudo nmap $TARGET -sS -sU --min-rate 1000 -oA nmap/$TARGET-initial
sudo nmap $TARGET -sS -sU -p- --min-rate 1000 -oA nmap/$TARGET-complete
sudo nmap $TARGET -sS -sU -p$PORTS -oA nmap/$TARGET-versions
```

## FTP
**TCP Port 21**
```bash
ftp $TARGET
# anonymous
# password
pwd

ls
get file.exe

binary
put reverse-shell.exe

exit
```

## NFS
**TCP Port 111**
```bash
sudo nmap $TARGET -p111 --script-nfs* 
showmount -e $TARGET 

sudo mkdir /mnt/FOO
sudo mount //$TARGET:/$SHARE /mnt/FOO

sudo adduser demo
sudo sed -i -e 's/1001/5050/g' /etc/passwd
cat /mnt/FOO/loot.txt
```

## SMTP
**TCP Port 25**
Manual enumeration
```bash
telnet $TARGET 25
HELO
VRFY root
QUIT
```

Automated enumeration via Nmap.
```bash
sudo nmap $TARGET -p25 --script smtp-commands -oN scans/$NAME-nmap-script-smtp-commands
sudo nmap $TARGET -p25 --script smtp-enum-users -oN scans/$NAME-nmap-script-smtp-enum-users
```

Automated SMTP user enumeration via smtp-user-enum.
```bash
smtp-user-enum -M VRFY -U /usr/share/wordlists/metasploit/unix_users.txt -t $TARGET
```

## POP3 
TCP Port 110
```bash
telnet $TARGET 110
USER root
PASS root
RETR 1
QUIT
```

## RPC
TCP Port 135
```bash
rpcclient -U '' $TARGET
netshareenum # print the real file-path of shares; good for accurate RCE
```

## SMB
**TCP Port 445**
SMBClient
```bash
smbclient -L //$TARGET/ # list shares
```

Impacket SMB Client
```bash
impacket-smbclient ''@$TARGET
use IPC$
```

SMBMap
```bash
smbmap -H $TARGET
```

smbget
```bash
smbget -R smb://$TARGET/$SHARE
```

<p align="right">
  <a href="/README.md">Home Page</a> |
  <a href="/CheatSheets/1_enumerate.md#">Top of Page</a> |
  <a href="/CheatSheets/1_enumerate.md#bottom-of-page">Bottom of Page</a>
</p>

## Bottom of Page