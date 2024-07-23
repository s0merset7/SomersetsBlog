---
title: "INE eJPT: Introduction to Attacks"
date: 2024-07-23
tags: ["INE", "Certification", eJPT]
image : "/posts/eJPT.png"
Description: "Part two of my notes for the INE Junior Penetration Tester (eJPT) Certification covering Introduction to Attacks."
---
*Note: Much of the below information is summarized from Alexis Ahmed's and Josh Mason's eJPT training videos hosted on INE Penetration Testing Student learning path. Much credit goes to their expertise! Check out their training materials in the sources*

Continuing with my notes from studying for the INE Junior Penetration Tester (eJPT) exam. The exam breaks down its curriculum into several sections, and this portion of my notes covers the "Introduction to Attacks" content.

Please keep in mind these are only my notes, and should not be used as the sole resource to study for the eJPT certification. Much of the necessary material is learned through interactive labs found in the Penetration Testing Student learning path. Additionally, the course constantly updates its material to remain up to current, meaning some of the below content may be out of date/missing important details.

# INE Junior Penetration Tester (eJPT) Notes
- [INE Junior Penetration Tester (eJPT) Notes](#ine-junior-penetration-tester-ejpt-notes)
  - [Introduction to Attacks](#introduction-to-attacks)
    - [Windows](#windows)
      - [Frequently Exploited Windows Services:](#frequently-exploited-windows-services)
        - [Microsoft IIS and WebDAV (Web Distributed Authoring \& Versioning)](#microsoft-iis-and-webdav-web-distributed-authoring--versioning)
        - [SMB/CIFS (Server Message Block Protocol)](#smbcifs-server-message-block-protocol)
        - [RDP](#rdp)
        - [WinRM](#winrm)
      - [Privilege Escalation](#privilege-escalation)
        - [Windows Kernel](#windows-kernel)
        - [User Account Control](#user-account-control)
        - [Access Token Impersonation](#access-token-impersonation)
      - [Alternate Data Streams](#alternate-data-streams)
      - [Credential Dumping](#credential-dumping)
    - [Linux](#linux)
      - [Apache Web Server](#apache-web-server)
      - [SSH (Secure Shell)](#ssh-secure-shell)
      - [FTP (File Transfer Protocol)](#ftp-file-transfer-protocol)
      - [SAMBA](#samba)
      - [Kernel Exploitation](#kernel-exploitation)
      - [Password Cracking](#password-cracking)
      - [Tools](#tools)
  - [Sources](#sources)
 
## Introduction to Attacks
### Windows
- Types of Windows Vulnerabilities:
  - **Information Disclosure**: vulnerability that allows an attacker to access confidential data
  - **Buffer Overflows**: caused by a programming error, allows attackers to write data to a buffer and overrun the allocated buffer, consequently writing data to allocated memory addresses
  - **Remote Code Execution**: vulnerability that allows an attacker to remotely execute code on the target system
  - **Privilege Escalation**: vulnerability that allows an attacker to elevate their privileges after initial compromise
  - **Denial of Service (DOS)**: vulnerability that allows an attacker to consume a system/host's resources (CPU, RAM, Network, etc) consequently preventing the system from functioning normally

#### Frequently Exploited Windows Services:
##### Microsoft IIS and WebDAV (Web Distributed Authoring & Versioning)
- **Microsoft IIS (Internet Information Services)**
  - Proprietary web server software developed by Microsoft that runs on Windows
  - TCP ports 80,443
  - Can be used to host websites/web apps and provides admins with a robust GUI for management
  - USes to host both static and dynamic web pages developed in ASP.NET and PHP
  - Supports the following executable file extensions
    - .asp, .aspx, .config, .php

- **WebDAV (Web Distributed Authoring & Versioning)**
  - HTTP extension that allows clients to update, delete, move, and copy files on a wbe server
    - It is used to enable a web server to act as a file server
  - TCP ports 80,443 (on top of Microsoft IIS)
  - In order to connect to a WebDAV server, one needs to provide legitimate credentials as WebDAV implements authentication in the form of a user/pass

- **Exploitation**
  1. Identify whether WebDAV is configured to run on the IIS web server
  2. Perform a brute-force attack on the server to identify credentials for authentication
  3. Authenticate with the WebDAV server to upload a malicious .asp payload use to execute arbitrary commands/obtain a reverse shell
  - Tools:
    - **DAV Test**: used to scan, authenticate, and exploit a WebDAV server
      - Usage: `davtest -<flags>`
    - **Cadaver**: supports file upload, download, on-screen display, in-place editing, namespace operations, collection creation/deletion, property manipulation, and resource locking on WebDAV servers
      - Usage: `cadaver <vulnerable_url>`
      - To find provided webshells, search `ls /user/share/webshells/`
  
##### SMB/CIFS (Server Message Block Protocol)
- Network file sharing protocol that is used to facilitate the sharing of files and peripherals between computers on a local network
- TCP port 445 (originally ran on top of NetBIOS on port 139)
- **SAMBA**: the open source Linux implementation of AMB that allows Windows systems to access Linux shares/devices
- Uses two levels of authentication (both a challenge response authentication system):
  - **User Authentication**: users must provide a username/password in order to authenticate with the SMB server in order to access a share
  - **Share Authentication**: users must provide a password in order to access a restricted share
- **PsExec**: a lightweight telnet-replacement developed by Microsoft that allows a user to execute processes on remote windows systems using any user's credentials
  - PsExec authentication is (performed bia SMB)
  - PsExec utility can be used to authenticate with the target system legitimately and run arbitrary commands/launch a remote command prompt
  - Very similar to RDP, however commands are sent via CMD vs controlling the remote system via GUI
- **Exploitation**:
  1. Identify legitimate user accounts and their respective passwords/password hashes
    - Can be performed many ways but commonly achieved by performing an SMB login brute-force attack
    - Can narrow down brute-force attacks to only include common Windows user accounts (ex: Administrator)
  2. With credentials, can authenticate with the target system via PsExec and execute arbitrary system commands/obtain a reverse shell
  - Tools:
    - `psexec.py`: python script to install a reverse shell to gain access to an SMB server with proper credentials
      - Usage: `psexec.py <username>@<IP_address> <desired_name_of_executable>.exe`
  - **EternalBlue Exploit (MS17-010/CVE-2017-0144)**: collection of windows vulnerabilities and exploits that allow attackers to remotely execute arbitrary code and gain access to a Windows system and consequently the network that the target system is a part of
    - Takes advantage of a vulnerability in the Windows SMBv1 protocol that allows attackers to send specially crafted packets that consequently facilitate the execution of arbitrary commands
 
##### RDP
- **RDP (Remote Desktop Protocol)**: proprietary GUI remote access protocol developed by Microsoft and is used to remotely authenticate and interact with a Windows system
- Uses TCP port 3389 by default but can be configured to run on any other TCP port
- RDP authentication requires a legitimate user account on the target system as well as the user's password in clear-text
- RDP brute-force attacks can be used to identify legitimate user credentials that can then be used to gain remote access to the target system
- Tools:
  - **X-Free RDP**: CLI tool to connect to an RDP session
    - Usage: `xfreerdp /u:<username> /p:<password> /v:<IP_Address>:<port_number>` 
- **BlueKeep (CVE-2019-0708)**: RDP vulnerability in Windows that could potentially allow attackers to remotely execute arbitrary code and gain access to a Windows system/network
  - The exploit takes advantage of a vulnerability in the RDP protocol that allows attackers to gain access to a chunk of kernel memory which gives arbitrary code execution at the system level without authentication


##### WinRM
- **WinRM (Windows Remote Management Protocol)**: Windows remote management protocol that cna be used to facilitate remote access with Windows systems
- TCP ports 5986,443
- Implemented into Windows to assist system administrators by allowing:
  - Remote access and interaction with Windows hosts on a local network
  - Remote access and command execution on Windows systems
  - Manage and configure Windows systems remotely
- **Exploitation**
  - WinRM implements access control and security for communication between systems through various forms of authentication
  - `crackmapexec` can be used to perform a brute-force attack in order to identify users and passwords, leading to command execution on a target system
  - Utilize a ruby script called "evil-winrm" to obtain a command shell session on the target system
- Tools:
  - **Evil WinRM**: a ruby script used to create a shell over WinRM for an attacker
    - Usage: `evil-winrm.rb -u <username> -p '<password>' -i <IP_Address>` 

#### Privilege Escalation

##### Windows Kernel
- **Kernel**: a computer program that is the core of an operating system and has complete control over every resource and hardware on a system
  - Acts as a translation layer between hardware and software and facilitates communication between the two layers
- **Windows NT**: the kernel that comes pre-packaged with all versions of Microsoft Windows and operates as a traditional kernel with a few exceptions based on user design philosophy
  - Consists of two main modes of operation that determine access to system resources and hardware
    - **User Mode**: programs and services running in user mode have limited access to system resources and functionality
    - **Kernel Mode**: kernel mode has unrestricted access to system resources and functionality with the added functionality of managing devices and system memory

##### User Account Control
- **UAC (User Account Control)**: a Windows security feature (introduced in Windows Vista) that is used to prevent unauthorized changes from being made to the operating system
  - Used to ensure changes to the operating system require approval from the administrator or a user account that is part of the local administrators group
  - A non-privileged user attempting to execute a program with elevated privileges will be prompted with the UAC credential prompt
    - While a privileges user would be prompted with a consent prompt

##### Access Token Impersonation
- **Windows Access Token**: a core element of the authentication process on Windows and are created and managed by the Local Security Authority Subsystem Service (LSASS)
  - Responsible for identifying and describing the security context of a process/thread running on a system
  - Generated by the winlogon.exe process every time a user authenticates successfully and includes the identity and privileges of the user account associated with the thread/process
    - Token is then attached to the userinit.exe process which then all child processes started by a user will inherit a cop of the access token from their creator and will run under the privileges of the same access token
  - Access tokens are categorized based on the varying security levels assigned to them
    - **Impersonate-Level**: tokens created as a direct result of a non-interactive login on Windows, typically through specific system services or domain logons
      - Can be used to impersonate a token on the local system and not on any external systems that utilize the token
    - **Delegate-Level**: tokens are typically created through an interactive login on Windows, primarily through a traditional login or through remote access protocols such as RDP
      - Pose the largest threat as they can impersonate tokens on any system
- Windows Privileges Required for Impersonation Attack:
  - **SeAssignPrimaryToken**: allows a user to impersonate tokens
  - **SeCreateToken**: allows a user to create an arbitrary token with administrative privileges
  - **SeImpersonatePrivilege**: allows a user to create a process under the security context of another user typically with administrative privileges

#### Alternate Data Streams
- **Alternate Data Streams (ADS)**: a New Technology File System (NTFS) file attribute and was designed to provide compatibility with the MacOS HFS (Hierarchical File System)
- Any file created on an NTFS formatted drive will have two different forks/streams
  - **Data Stream**: default stream that contains the data of the file
  - **Resource Stream**: typically contains the metadata of the file
- ADS can be used to fide malicious code/executables in legitimate files to evade detection
  - Done by storing the malicious code/executable in the files attribute resource stream (metadata) of a legitimate file
  - Usually used to evade basic signature based Anti-Virus and static scanning tools

#### Credential Dumping
- Windows OS stores hashed user account passwords locally in the Security Accounts Manager (SAM) database
- Authentication and verification of user credentials is facilitated by the Local Security Authority (LSA)
- Windows versions up to Windows Server 2003 use LM and NTLM hashes, Windows Vista onwards only utilizes NTLM
- **SAM (Security Accoun Manager)**: a database file responsible for managing user accounts and passwords on Windows
  - All account passwords stored in the SAM database are hashed
  - The SAM database file cannot be copied while the operating system is running
  - Windows NT kernel keeps the SAM database file locked, forcing hackers to utilize in-memory techniques and tools to dump SAM hashes from teh LSASS process
  - Modern Windows versions encrypt the SAM database with a syskey
- **LM (LanMan) Hash**: the default hashing algorithm implemented in Windows operating systems prior to NT4.0
  - Used to hash user passwords using the following process:
    - Password is broken into two seven-character chunks
    - All characters are converted to uppercase
    - Each chunk is hashed separately with the DES algorithm
  - Considered to be a weak protocol and easily cracked as the password hash does not include salts
- **NTLM (NTHash)**: a collection of authentication protocols utilized in Windows to facilitate authentication between computers
  - Process involves using a valid username and password to authenticate successfully
  - Used in Windows Vista onwards (LM is disabled)
  - When a user account is created, it is encrypted using the MD4 hashing algorithm, while the original password is disposed of
  - Improves on LM by:
    - Does not split the hash into two chunks
    - Case sensitive
    - Allows the use of symbols/unicode characters
- **Unattended Windows Setup**: capability to automatically configure multiple Windows setups on different devices by deploying a custom configuration file
  - The utility will typically utilize one of the following config files that contain user account and system config info
    - `C:\Windows\Panther\Unattend.xml`
    - `C:\Windows\Panther\Autounattend.xml`
  - The passwords to these files may be base64 encoded
- **Mimicatz**: A Windows post-exploitation tool allowing for the extraction of clear-text passwords, hashes, and kerberos tickets from memory
  - Can be used to extract hashes from the lsass.exe process memory where hashes are cached
- **Pass-The-Hash**: an exploitation technique that involves capturing or harvesting NTLM hashes/clear-text passwords and utilizing them to authenticate with the target legitimately
  - Allows attackers to obtain access to the target system via legitimate credentials as opposed to obtaining access via service exploitation

### Linux
#### Apache Web Server
- A free an open source cross-platform web server released under the Apache License 2.0
- Accounts for over 80% of web servers globally
- TCP ports 80/443
- **Shellshock (CVE-2014-6271)**: a family of vulnerabilities in the Bash shell that allows an attacker to execute remote arbitrary commands via Bash, consequently allowing the attacker to obtain remote access to the target system via a reverse shell
  - Caused by a vulnerability in Bash when Bash mistakenly executes trailing commands after a series of characters
  - Affects only Linux (Windows does not utilize Bash)
  - Apache web servers configured to run CGI (Common Gateway Interface) or .sh scripts are also vulnerable
  - For execution, an input vector/script that allows for Bash communication must be located
#### SSH (Secure Shell)
- A cryptographic remote access protocol that is used to remotely access and control systems over an unsecured network
- Developed as a secure successor to telnet
- Authentication is either username and password or key based authentication
- TCP port 22 (can be configured to run on any open TCP port)
#### FTP (File Transfer Protocol)
- A protocol used to facilitate file sharing between a server and client/clients (and vice-versa)
- Frequently used as a means of transferring files to and from the directory of a web server
- Authentication requires a username and password combination
- May be configured to allow anonymous access allowing unauthenticated access
- TCP port 21
#### SAMBA
- Samba is the Linux implementation of SMB, and allows Windows systems to access linux shares and devices
- Authentication uses username and password
- TCP port 445
#### Kernel Exploitation
- Typically target vulnerabilities in the Linux kernel to execute arbitrary code
  - With the goal of running privileged system commands or obtaining a system shell
- Process differs based on Kernel version and distribution
#### Password Cracking
- The `passwd` file gives information in regard to the hashing algorithm being used and the password has
  - This can be determined by viewing the number after the username encapsulated by the dollar symbol ($)
- `$1` = MD5
- `$2` = Blowfish
- `$3` = SHA-256
- `$6` = SHA-512

#### Tools
- `crackmapexec`: swiss army tool for penetration testing
- `searchsploit`: tool to search for known exploits
- `Linux-Exploit-Suggester`: tool designed to assist in detecting security deficiencies in a Linux Kernel
  - Using heuristics methods will assess the exposure of the given kernel on every publicly known kernel exploit

## Sources
- [Official INE Site](https://ine.com/)
- [INE eJPT Study Course](https://my.ine.com/CyberSecurity/learning-paths/61f88d91-79ff-4d8f-af68-873883dbbd8c/penetration-testing-student)