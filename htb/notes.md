# Notes on machines

## SMB

**Microsoft DS** is the name given to port 445 which is used by SMB (Server Message Block). SMB is a network protocol used mainly in Windows networks for sharing ressources (e.g. files or printers) over a network. It can also be used to remotely execute commands.

The Transport layer protocol that Microsoft SMB Protocol is
most often used with is NetBIOS over TCP/IP (NBT).

An SMB-enabled storage on the network is called a share .

At a user level,
SMB clients are required to provide a username/password combination to see or interact with the contents
of the SMB share.

`smbclient -L {IP}`

Shares:

ADMIN$ - Administrative shares are hidden network shares created by the Windows NT family of
operating systems that allow system administrators to have remote access to every disk volume on a
network-connected system. These shares may not be permanently deleted but may be disabled.

C$ - Administrative share for the C:\ disk volume. This is where the operating system is hosted.

IPC$ - The inter-process communication share. Used for inter-process communication via named
pipes and is not part of the file system.

WorkShares - Custom share.

## Ports

Scan all ports

`nmap -p- -sV {IP}`

`nmap -p- --min-rate=1000 -sV {target_IP}`

Check ports definition

[https://www.speedguide.net/port.php?port=5357](https://www.speedguide.net/port.php?port=5357)

3389 - use `xfreerdp`

## Nmap

`nmap -sC {IP}`

- default scripts + versions

## RDP

### xfreerdp

to solve dependency issues

`sudo apt-get install aptitude`

Install the package using `aptitude`

`xfreerdp /v:{IP} /cert:ignore /u:Administrator`

## Directory bruteforcing

`gobuster dir -e -u http://10.129.25.247 -w /usr/share/wordlists/dirb/common.txt`
gobuster dir -x .php -e -u http://10.129.25.247 -w /usr/share/wordlists/dirb/common.txt

## Questions to ask

- What services listen on what ports?
- Which TCP ports are open on the machine?
- How to interact with {service} Linux?

## Connecting to Mongo

`./mongo mongodb://10.129.228.30:27017`

## Rsync

`rsync -avz --list-only /home {IP}`

Get rsync modules
`rsync rsync://10.129.228.37/`

Get files of a module
`rsync rsync://10.129.228.37/[module_name]`

Copy the file
`rsync -aiv {IP}::{module_name}/path/to/file ~`

## FTP

```
ftp ${IP}
login: anonymous

ftp> help
```

## How To

1. See what services are available using nmap.
2. Try to access the service on the web if there is a webserver.
3. Try to connect to the services.

## File Inclusion vulnerability

OS: Windows

[Windows New Technology LAN Manager (NTLM)](https://www.crowdstrike.com/cybersecurity-101/ntlm-windows-new-technology-lan-manager/) is a suite of security protocols offered by Microsoft to authenticate users’ identity and protect the integrity and confidentiality of their activity. At its core, NTLM is a single sign on (SSO) tool that relies on a challenge-response protocol to confirm the user without requiring them to submit a password.

[How it works](https://www.ionos.com/digitalguide/server/know-how/ntlm-nt-lan-manager/)

[File Inclusion Windows WordList](https://github.com/carlospolop/Auto_Wordlists/blob/main/wordlists/file_inclusion_windows.txt)

One of the most common files that a penetration tester
might attempt to access on a Windows machine to verify LFI is the hosts file,
`WINDOWS\System32\drivers\etc\hosts` (this file aids in the local translation of host names to IP
addresses).
