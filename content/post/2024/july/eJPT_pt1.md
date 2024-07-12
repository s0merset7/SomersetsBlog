---
title: "INE eJPT: Information Gathering and Enumeration"
date: 2024-07-12
tags: ["INE", "Certification", eJPT]
image : "/posts/eJPT.png"
Description: "Part one of my notes for the INE Junior Penetration Tester (eJPT) Certification covering Information Gathering and Enumeration content."
---
*Note: Much of the below information is summarized from Alexis Ahmed's and Josh Mason's eJPT training videos hosted on INE Penetration Testing Student learning path. Much credit goes to their expertise! Check out their training materials in the sources*

INE's Junior Penetration Tester (eJPT) certification is cert designed to be taken by individuals with minimal cybersecurity experience, teaching them everything they need to know about penetration testing in order to get their foot in the door. Having taken and passed the exam, I condensed all of my notes for easy reference and to allow anyone to use them to assist with studying. The exam is a 48hr interactive test during which students must attempt to pentest several virtual environments in a lab setting and as proof answer questions about their exploitation process. The official study material is broken down into sections mirroring the penetration testing process, and this portion of my notes covers the "Introduction", "Information Gathering", and "Enumeration" content.

Please keep in mind these are only my notes, and should not be used as the sole resource to study for the eJPT certification. Much of the necessary material is learned through interactive labs found in the Penetration Testing Student learning path. Additionally, the course constantly updates its material to remain up to current, meaning some of the below content may be out of date/missing important details.


# INE Junior Penetration Tester (eJPT) Notes
- [INE Junior Penetration Tester (eJPT) Notes](#ine-junior-penetration-tester-ejpt-notes)
  - [Pentesting Methodology](#pentesting-methodology)
  - [Information Gathering](#information-gathering)
    - [Passive Reconnaissance](#passive-reconnaissance)
    - [Active Reconnaissance](#active-reconnaissance)
    - [Information Gathering Tools](#information-gathering-tools)
  - [Enumeration](#enumeration)
    - [SMB](#smb)
    - [FTP](#ftp)
    - [SSH](#ssh)
    - [HTTPS](#https)
    - [SQL](#sql)
    - [Enumeration Tools](#enumeration-tools)
  - [Sources](#sources)

## Pentesting Methodology
1. Information Gathering
   1. Passive Information Gathering
      - OSINT
   2. Active Information Gathering
      1. Network Mapping
      2. Host Discovery
      3. Port Scanning
      4. Service Detection and Operating System Detection
2. Enumeration
   1. Service and Operating System Enumeration
      1. Service Enumeration
      2. User Enumeration
      3. Share Enumeration
3. Exploitation/Initial Access
   1. Vulnerability Analysis and Threat Modeling
      1. Vulnerability Analysis
      2. Vulnerability Identification
   2. Exploitation
      1. Developing/Modifying Exploits
      2. Service Exploitation
4. Post-Exploitation
   1. Post Exploitation
      1. Local Enumeration
      2. Privilege Exploitation
      3. Credential Access
      4. Persistence
      5. Defense Evasion
      6. Lateral Movement
5. Reporting
   1. Report Writing
   2. Recommendations

## Information Gathering
- **Information Gathering**: the first step of any penetration test involving gathering or collecting information about an individual, company, website or system that you are targeting
  - **Passive Information Gathering**: gathering as much information as possible without actively engaging with the target
  - **Active Information Gathering**: gathering as much information as possible by actively engaging with the target system
    - Requires authorization in order to perform

### Passive Reconnaissance
- **WHOIS**: internet query and response protocol widely used for querying databases that store the registered users or assignees of a particular internet resources such as a domain name, IP address block, or autonomous system
- **Google Dorks/Hacking**: additional search parameters that can be added to a Google search to specify desired search results
  - `site:` specifies that all results should only be from a certain domain
    - Ex: `site:yourDomain.com`
  - `inurl:` specifies that all results must include the word(s) in the full URL
    - Ex: `inurl:forum`
  - `intitle:` specifies that all results must include the word(s) in the website title
    - Ex: `intitle:pottery`
  - `filetype:` specifies that all results must be of a certain file type
    - Ex: `filetype:pdf`
  
### Active Reconnaissance
- **DNS Interrogation**: the process of enumerating DNS records for a specific domain
  - **DNS Zone File**: a file containing records pertinent to a particular domain
- **Network Mapping**: the process of discovering and identifying devices, hosts, and network infrastructure elements within a target network
  - **Host Discovery**: phase to identify live hosts on a network before further exploration and vulnerability assessment
    - **Ping Sweeps (ICMP Echo Requests)**: sending ICMP Echo Requests (ping) to a range of IP addresses to identify live hosts
      - Pros: widley supported, quick method for identification of live hosts
      - Cons: some hosts/firewalls (like Windows) can be configured to block ICMP traffic, can be easily detected
    - **ARP Scanning**: using Address Resolution Protocol (ARP) requests to identify hosts on a local network
    - **TCP SYN Ping (Half-Open Scan)**: sending TCP SYN packets to a specific port (often 80) to check if a host is alive. This technique is stealthier than an ICMP ping
      - Pros: stealthier than ICMP ping, may bypass firewalls that allow outbound connections
      - Cons: some hosts may not respond to to TCP SYN requests, firewalls and security devices can affect results
    - **UDP Ping**: sending UDP packets to a specific port to check if a host is alive
    - **TCP ACK Ping**: sending TCP ACK packets to a specific port to check if a host is alive. This technique expects no response, but if a TCP RST is received, it indicates that the host is alive
    - **SYN-ACK Ping**: sending TCP SYN-ACK packets to a specific port to check if a host is alive. If a TCP RST is received, it indicates the host is alive
  - Identification of Open posts and services
  - Network topology mapping
  - Operating system fingerprinting
  - Service version detection
  - Identifying filtering and security measure

### Information Gathering Tools
- **BuiltWith**: browser plugin that will list all technologies in use on a webpage
- **Wappalyzer**: browser plugin that identified technologies used on a website
- **Whatweb**: CLI tool that will return detected technologies found on a provided URL
  - Usage: `whatweb yourDomain.com`
- **HTTrack**: downloadable tool that allows a user to download an internet website to a local directory, building recursively all directories, getting HTML, images, and other files from the server
  - Found [here](https://wwww.httrack.com)
- **Netcraft**: 3rd party tool that provides an automated lookup of many passive reconnaissance information such as WHOIS, website certificates, technologies used, basic SSl/TLS vulnerability checking, and network information
  - Found [here](netcraft.com)
- **DNSRecon**: a CLI tool based python script that provides the ability to perform DNS record lookups, NS records for one transforms, common SRV record enumeration, and TLD expansion
  - Usage: `dnsrecon -d yourDomain.com`
- **DNS Dumpster**: web based solution to DNS reconnaissance research in a organized UI
  - Found [here](dnsdumpster.com)
- **WAFW00F**: a python based CLI tool used to detect web application firewalls (WAF) active on a given domain
  - Usage: `wafw00f yourDomain.com`
- **Sublist3r**: a python based CLI tool designed to enumerate subdomains of websites using open source intelligence (OSINT)
  - Usage: `sublist3r -d yourDomain.com`
- **The Wayback Machine**: a web based tool that records and stores versions of internet websites throughout time
  - Found [here](web.archive.org)
- **theHarvester**: a python based CLI tool designed to perform both passive and active reconnaissance to gather emails, names, subdomains, IPs, and URLs
  - Usage: `theHarvester -d yourDomain.com`
- **have i been pwned?**: website that can check if an email/password has appeared in a past databreach
  - Found [here](haveibeenpwned.com)
- **DNS Enumerator**: CLI tool designed to perform passive and active DNS recon with features to automatically attempt zone transfers, DNS brute force, and more
  - Usage: `dnsenum yourDomain.com`
- **Network Mapper (nmap)**: open source CLI tool for network exploration and security auditing that can rapidly scan large networks or single hosts
  - Usage: `nmap host`
    - Host Discovery
      - `-sn` no port scan, will stop nmap after host discovery and only print available hosts that have responded to host discovery pings
      - `-Pn` ignores ping probes intended to check if the host is online and instead performs the port scan without checking for host activity first
      - `--send-ip` specify to use ICMP regardless of the detected network
      - `-PS` specify using a TCP SYN scan (default is to send to port 80)
        - `-PS#` customize the port to send the TCP SYN packets to
      - `-PA` specify using a TCP ACK scan (default is to send to port 80)
        - `-PA#` customize the port to send the TCP ACK packets to
      - `-PE` specify using a ICMP echo request scan
      - `-iL targetList.txt` have a newline separated file with a list of targets to scan
    - Port Scanning
      - `--open` scan the network only returning results of open ports
      - `--top-ports #` scan only for the top 'x' amount of common ports
      - `-F` fast scan, only scans the 100 most commonly used ports
      - `-p-` scan the entire port range instead of only the 1000 most commonly used ports
      - `-p` scan the selected port range
        - Ex: `-p 80` only scan port 80; `-p 80,443` only scan ports 80 and 443; `-p 1-100` only scan ports 1 through 100
      - `-sS` stealth scan, ensures a TCP SYN scan is performed without completing a TCP 3-way handshake (no RST packet sent by namp) preventing connection logs from being generated
      - `sT` TCP connects scan (default scan), TCP SYN scan completed and nmap closes and connections (RST packet sent)
      - `-sU` UDP port scan, will perform a UDP port scan instead of the default TCP port scan
      - `-sA` TCP ACK scan, will send ACK packets to ports, typically best for identifying filtered ports
      - `-v` verbose, add output during the scan indicating scan progress and current results
      - `-sV` service version detection, check the version of active port services
        - `--version-intensity #` with a number (higher is more accuracy required) will force nmap to provide a more detailed level of accuracy to the service version detection
      - `-O` operating system detection, check the operating system of the host (accuracy varies)
        - `--osscan-guess` will force nmap to guess what the OS is with percentage accuracy
      - `-sC` default script scan, runs a list of script on open ports to try and find more information
        - `--script=scriptName` specifies which script is desired to be run
        - `--script-help=scriptName` provides a brief description as to what the script does
        - `--script-args arg1,arg2` allows arguments to be included if a script requires them
      - `-A` aggressive scan, combines the `-sV`, `-O`, and `-sC` flags into the scan
    - Timing and Performance
      - Timing Templates `-T#`: changes to the speed that can be modified based on the goal of the scan
        - `T0` paranoid
        - `T1` sneaky
        - `T2` polite
        - `T3` normal
        - `T4` aggressive
        - `T5` insane
      - `--host-timeout #units` changes the amount of time a scan will wait for a host to respond before quitting an attempt
        - Ex: `--host-timeout 5s` timeout after 5 seconds
      - `--scan-delay #units` changes the amount of time to wait between a packet being sent
        - Ex: `--scan-delay 5s` wait 5 seconds between packets being sent
    - Output Modes `-o* filename`: formats that the port scan results can be outputted to
      - `-oN output.txt` normal, copies the results in the same format as when printed to the terminal
      - `-oX output.xml` XML, translates the results into XML format
      - `-oG output.txt` greppable format, translates the results into a mode that is easy to use Grep with
      - `-oA output` all flag, will translate the results into the three above common output formats
    - Detection Evasion
      - `-f` fragmented packets, will fragment packets in an effort to evade IDS and firewalls
        - `-f --mtu #` can set a maximum transmission unit (MTU) for how the packets should be fragmented
      - `-D decoy_IP` can set a decoy IP address for nmap to be sending the packets from
      - `-g #` decoy port number, what to set the source port number to in packets
- **Net Discover**: 
  - Usage: `netdiscover -i interface -r IP_Range`
    - `-i` interface, specify which interface should be used (Ex: eth0)
    - `-r` IP Range, the IP address range to be scanned in CIDR notation
- **FPing**: send ICMP ECHO_REQUEST packets to network hosts (modification of `ping`)
    - Usage: `fping IP_Range`
      - `-a` alive, show targets that are alive
      - `-g` generate target list (if not `-f` is specified), allows a subnet to be specified as the IP_Range in CIDR notation

## Enumeration

### SMB
- **SMB (Server Message Block)**: a Windows implementation of a file share. Typically runs on port 445
  - **CIFS (Common Internet File Sharing System)**: generic term for SMB
  - Helpful `nmap` scripts for enumeration: (all scripts visible by running `ls /usr/share/nmap/script/ | grep "smb"`)
    - `--script smb-protocols` helps find protocols being run on the instance of SMB
    - `--script smb-security-mode` reveals information about the security of the SMB instance (such as authentication levels, message signing, etc)
    - `--script smb-enum-sessions` shows active sessions on the SMB instance
      - `--script smb-enum-sessions --script-args smbusername=<username>,smbpassword=<password>` shows active sessions being checked from the account that the credentials are for
    - `--script smb-enum-shares` lists all shares on the device with access rights and other information
      - `--script smb-enum-shares --script-args smbusername=<username>,smbpassword=<password>` lists all shares on the device with the access rights of the account that the credentials are for
      - `--script smb-enum-shares,smb-ls --script-args smbusername=<username>,smbpassword=<password>` lists all shares along with their directory structure (if user has access)
    - `--script smb-enum-users --script-args smbusername=<username>,smbpassword=<password>` lists all user accounts for the SMB instance along with account info
    - `--script smb-server-stats --script-args smbusername=<username>,smbpassword=<password>` lists information about the server
    - `--script smb-enum-domains --script-args smbusername=<username>,smbpassword=<password>` lists available domains on the SMB instance
    - `--script smb-enum-sessions --script-args smbusername=<username>,smbpassword=<password>` lists all groups and corresponding users on the SMB instance
    - `--script smb-enum-services --script-args smbusername=<username>,smbpassword=<password>` lists all running services on the SMB instance
    - `--script smb-os-discovery` reveals operating system information about the SMB server
- - `net`: Windows CLI tool to connect/disconnect to SMB servers
  - `net use Z: \\<IP_Of_SMB_Server>\C$ <password> /user:<username>` - connect and mount an SMB server located at a given IP address with provided credentials
  - `net use * /delete` - disconnect from any SMB mounted servers currently synched to
- **SMB Map**: python based CLI tool to enumerate SMB servers
  - Ex: `smbmap -u guest -p "" -d . -H <IP_Of_SMB_Server>` - logs into and prints a snapshot of the shares of the SMB server at given address under the guest account with a null password
    - `-u <username>` username field
    - `-p "<password"` password field (leave empty for no password)
    - `-d <directory/mapping>` directory to navigate to and print upon sign-in
    - `-H <IP_Of_SMB_Server>` hostname/IP address of the SMB server to login to
    - `-x "<command>"` runs the listed command upon login
    - `-L` list out the contents of the the SMB server
    - `-r '<drive>'` list the contents of the provided drive (Ex: `-r 'C$` lists the contents of the C-Drive)
    - `--upload '/local/filepath' 'SMB\filepath'` upload a local file to the SMB server (Ex: `--upload '/root/backdoor' 'C$\backdoor'` uploads the local file "backdoor" to the SMB server in the C-Drive)
    - `--download 'SMB\filepath'` download a file from the SMB server (Ex: `--download 'C$\test.txt'` downloads the test.txt file from the SMB C-Drive)
- **SMB Client**: linux CLI command to connect to and retrieve information about a server's SMB configuration
  - Usage: `smbclient <flags>`
    - `-L <IP_Address>` list share information
    - `-N` check for a null session availability
      - `smbclient //<IP_Address>/<Share_Name> -N` sign into the SMB server with a null password
    - `-U <username>` indicate the username to sign in with (password will be prompted) 

### FTP
- **FTP (File Transfer Protocol)**: protocol that allows for remote access and storage of files
- `ftp` CLI command to connect to an FTP server
  - Usage: `ftp <IP_Address>`
- - Helpful `nmap` scripts for enumeration: (all scripts visible by running `ls /usr/share/nmap/script/ | grep "ftp"`)
    - `--script ftp-brute --script-args userdb=<path/to/file>` attempts to brute force passwords given a list of known users in a provided newline separated file
    - `--script ftp-anon` attempts to sign into the FTP server using default anonymous logins

### SSH
- **SSH (Secure Shell)**: used for remote administration by providing remote access to a machine via an encrypted tunnel
- `ssh` CLI command to connect to a server via SSH
    - Usage: `ssh <username>@<IP_Address>`
- Helpful `nmap` scripts for enumeration: (all scripts visible by running `ls /usr/share/nmap/script/ | grep "ssh"`)
    - `--script ssh2-enum-algos` enumerates all algorithms that can be used to create a sign-on key
    - `--script ssh-hostkey --script-args ssh_hostkey=full` attempts to find and present the SSH RSA host key
    - `--script ssh-auth-methods --script-args="ssh.user=<username>"` identifies what (if any) authentication methods are in place for a known user
    - `--script ssh-brute --script-args userdb=<path/to/file>` tries to brute force the password for provided usernames
  
### HTTPS
- **HTTP(S) (HyperText Transfer Protocol (Secure))**: service used to host websites and allow for remote connection to them
- Helpful `nmap` scripts for enumeration: (all scripts visible by running `ls /usr/share/nmap/script/ | grep "http"`)
  - `--script http-enum` enumerates services running on http and common directory listings found on the site
  - `--script http-headers` finds http header information
  - `--script http-methods --script-args http-methods.url-path=/<website_path>/` return allowed methods on that specific page of the website
  - `--script http-webdav-scan --script-args http-webdav-scan.path=/<website_path>/` helps identify webdav installations and enumerate information about them
  - `--script banner` returns the banner for a device connecting to the service for the first time
- **httpie**: CLI tool made to interact with HTTP services in a way similar to curl
  - Usage: `http <IP_Address>`
- **Bowsh**: CLI tool to attempt to render a website in the command line
  - Usage: `browsh --startup-url <website_URL>`
- `wget`: retrieves web files
  - Usage: `wget "<website_URL>"` 

### SQL
- **SQL (Structured Query Language)**: service used to interact with data
- **MySQL**: one of the most common open versions of SQL, often run on Unix/Linux distributions
  - Typically run on port 3306
- Helpful `nmap` scripts for enumeration: (all scripts visible by running `ls /usr/share/nmap/script/ | grep "mysql"`)
    - `--script mysql-empty-password` finds any logons that allow an empty password for authentication
    - `--script mysql-info` provides enumeration info about a mysql service
    - `--script mysql-users --script-args="mysqluser='<username>',mysqlpass='<password>'"` using provided user creds, will sign in and return a list of user accounts on the server
    - `--script mysql-databases --script-args="mysqluser='<username>',mysqlpass='<password>'"` using provided user creds, will sign in and return a list of databases on the server
    - `--script mysql-variables --script-args="mysqluser='<username>',mysqlpass='<password>'"` using provided user creds, will sign in and return a list of variables on the server
    - `--script mysql-audit --script-args="mysql-audit.username='<username>',mysql-audit.password='<password>',mysql-audit.filename='/usr/share/nmap/nselib/data/mysql-cis.audit'"` provides common audit configuration checks and results
    - `--script mysql-dump-hashes --script-args="username='<username>',password='<password>'"` using provided user creds, will sign in and return a list of account password hashes
- `mysql`: CLI tool used to interact with MySQL servers
  - Usage: `mysql -h <IP_Address> `
    - `-h <IP_Address>` indicate the host IP address
    - `-u <username>` username to sign in with (default is "root")
  - Commands to use in the interface:
    - `show databases;` displays a list of all databases on the server
    - `use <database_name>;` changes the database to the selected one
    - `help` display help menu
- **MSSQL (Microsoft SQL)**: most common Microsoft instance of SQL
  - Helpful `nmap` scripts for enumeration: (all scripts visible by running `ls /usr/share/nmap/script/ | grep "ms-sql"`)
    - `--script ms-sql-info` performs basic enumeration on the MSSQL instance
    - `--script ms-sql-ntlm-sql --script-args mssql.instance-port=<port_number>` performs basic enumeration on an NTLM MSSQL instance
    - `--script ms-sql-brute --script-args userdb=<file/path/to/wordlist>,passdb=<file/path/to/wordlist>` attempts to brute force a login from the supplied wordlists
    - `--script ms-sql-empty-password` attempt to login to the MSSQL service with a null password
    - `--script ms-sql-dump-hashes --script-args mssql.username=<username>,mssql.password=<password>` logs in using provided credentials to find and list other user account password hashes
    - `--script ms-sql-xp-cmdshell --script-args mssql.username=<username>,mssql.password=<password>,cmd="<command_to_use>"` logs in using provided credentials and executes the provided command

### Enumeration Tools
- **NMB Lookup**: CLI tool that utilizes NetBIOS information to view configuration settings
  - Usage: `nmblookup <flags>`
    - `-A <IP_Address>` lookup by IP to connect to a server's NetBIOS info and list server connection information
- **RPC Client**: 
  - Usage `rpcclient <flags> <IP_Address>`
    - `-U "<username>"` username field (leave empty string for null session)
    - `-N` no password
  - Commands to use when connected:
    - `?` list all available commands (help)
    - `srvinfo` show server information
    - `enumdomusers` show list of users
    - `lookupnames <username>` show info (SID) of provided user
    - `enumdomgroups` show all domain groups
- **Enumeration for Linux**: enumeration CLI tooling
  - Usage: `enum4linux <flags> <IP_Address>`
    - `-o` operating system information
    - `-U` show a list of users on the server
    - `-S` list all shares
    - `-G` list all domain groups
    - `-i` list if printers are available
    - `-r` list users and SIDs
- **Hydra**: brute force CLI tool
  - Usage: `hydra <flags> <IP_Address> <protocol>` (Ex: `hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.10.10 smb` will try to login to the SMB server at the IP address with the username admin trying passwords found in the rockyou txt file)
    - `-l <username>` login name
    - `-P <path/to/file>` indicate password wordlist 
    - `-L <path/to/file>` indicates login username wordlist
- **Net Cat**: CLI tool to connect to remote hosts
  - Usage: `nc <IP_Address> <Port_Number>`
- **WhatWeb**: CLI tool to help enumerate website information
  - Usage: `whatweb <IP_Address>`
- **Directory Buster**: CLI tool to enumerate directories of a website from a wordlist
  - Usage: `dirb <website_URL> <file/path/to/wordlist>`
- `lynx`: CLI tool to display the text and formatting from a website
  - Usage: `lynx <website_URL>`

## Sources
- [Official INE Site](https://ine.com/)
- [INE eJPT Study Course](https://my.ine.com/CyberSecurity/learning-paths/61f88d91-79ff-4d8f-af68-873883dbbd8c/penetration-testing-student)