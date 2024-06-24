---
title: "CompTIA Security+: Operations, Incident Response, Governance, Risk, and Compliance"
date: 2024-06-23
tags: ["CompTIA", "Certification", Security+]
image : "/posts/Security+_pt1.webp"
Description: "Part four of my notes for the CompTIA Security+ Certification covering the Operations and Incident Response and Governance, Risk, and Compliance sections."
---
*Note: Much of the below information is summarized from Christopher Rees' Security+ training course hosted on Pluralsight. Much credit goes to Chris' expertise! Check out his courses in the sources*

Continuing with the final part my notes from studying for the CompTIA Security+ exam. The exam breaks down its curriculum into several sections, and this final portion of my notes covers the "Operations and Incident Response" and "Governance, Risk, and Compliance" content.
Please keep in mind these are only my notes, and should not be used as the sole resource to study for the Security+ certification. Additionally, since taking the exam, a new version has been published, meaning some of the below content may be out of date/missing important details.

- [Operations and Incident Response](#operations-and-incident-response)
  - [Tools to Assess Organizational Security](#tools-to-assess-organizational-security)
    - [Definitions](#definitions)
  - [Policies, Processes, and Procedures for Incident Response](#policies-processes-and-procedures-for-incident-response)
    - [Definitions](#definitions-1)
    - [Phases of Incident Response](#phases-of-incident-response)
    - [Types of Testing and Exercises](#types-of-testing-and-exercises)
    - [Types of Plans](#types-of-plans)
  - [Appropriate Data Sources to Support an Investigation](#appropriate-data-sources-to-support-an-investigation)
    - [Definitions](#definitions-2)
  - [Mitigation Techniques to Secure and Environment](#mitigation-techniques-to-secure-and-environment)
    - [Definition](#definition)
  - [Key Aspects of Digital Forensics](#key-aspects-of-digital-forensics)
    - [Definitions](#definitions-3)
- [Governance, Risk, and Compliance](#governance-risk-and-compliance)
  - [Comparing and Contrasting Types of Controls](#comparing-and-contrasting-types-of-controls)
    - [Definitions](#definitions-4)
  - [Regulations, Standards, and Frameworks that Impact a Security Organization](#regulations-standards-and-frameworks-that-impact-a-security-organization)
    - [Definitions](#definitions-5)
    - [GDPR Data Processing Principles](#gdpr-data-processing-principles)
    - [GDPR Legal Grounds for Processing Data](#gdpr-legal-grounds-for-processing-data)
  - [Sources](#sources)

# Operations and Incident Response
## Tools to Assess Organizational Security
### Definitions
- **Tracert/Traceroute**: network tool to test connectivity between host and target that will show hops along the way and the associated latency with each hop
- **nslookup/dig**: DNS troubleshooting tool for Window, Linux, and Mac OS that can provide a wide range of information on DNS and associated troubleshooting
    - `nslookup` can be used on Windows and Linux while `dig` is Linux an Mac
- **nmap**: open-source network scanner that can discover hosts, services, detect OS type, vulnerabilities, etc.
- **ping/pathping**: network troubleshooting tool to test network connectivity by sending ICMP packets to a host
    - `pathping` combines the features of `ping` and `tracert`
    - PING = Packet Inter-Network Groper
- **hping**: packet crafting tool that can be used to generate network traffic, craft packets (spoofed addresses, ICMP floods, etc.)
- **Netstat**: displays network statistics about TCP/UDP connections, ports, routing tables, and protocol statistics
- **netcat**: network troubleshooting, pentesting, hacking tool that can read from and write to network connections (TCP/UDP)
- **IP Scanner**: a tool that can scan a network, range of IP addresses, discover hosts, test for open ports, troubleshoot connectivity, etc.
- **Address Resolution Protocol (ARP)**: resolves an IP to a MAC address via link-payer protocol
    - **Reverse ARP**: deriving an IP from a MAC address
    - **ARP Spoofing**: malicious user can intercept and reply to ARP requests (ARP cache poisoning)
- **route**: command used to view and manipulate the IP routing table on Windows and Linux hosts
- **curl**: transfers data from or to a server using a variety of protocols
- **The Harvester**: tool for gathering email accounts and subdomain names from public sources
- **sn1per**: automated pentesting tool with extensible scripting features that leverages several other testing/exploit tools to scan hosts and networks
- **scanless**: port scanner that leverages online port scanning services to anonymise scanning a target system
- **Nessus**: commercial vulnerability scanner
- **Cuckoo**: open-source automated malware analysis platform designed to be run in a isolated lab environment
- **Logger**: creates entries in the system log via a provided shell command interface to the syslog system-log module
- **Powershell**: command-line shell and associated scripting language
- **OpenSSL**: software library for applications that secure communications, using an open source implementation of SSL and TLS
- **tcpdump**: CLI packet-capture tool to capture/display packets in real time with options to filter by IP address, port, connection type, protocol type, etc.
- **Wireshark**: GUI packet capture utility, similar to `tcpdump` that can be used to troubleshoot network issues, communications, and eavesdrop on communications
- **tcpreplay**: CLI tool for editing and replaying previously captured packets
- **dd**: CLI tool to copy/clone disks, partitions/files, erase disks, etc.
- **memdump**: dumps either physical or kernel memory to a file (can be done over the network)
- **WinHex**: hex editor for examining files, recovering/searching for files, etc.
- **FTK Imager**: forensic toolkit for acquiring disk images and performing analysis/investigations
- **Autopsy**: forensic toolkit for acquiring disk images and performing analysis/investigations
- **Exploitation Frameworks**: toolsets that can be used offensively or defensively and are often used by pentesters and hackers

## Policies, Processes, and Procedures for Incident Response
### Definitions
- **Cyberthreat Intelligence Frameworks**: focuses attention on the proper areas to ensure follow up, eradication, and mitigation of future threats
    - Common language to communicate internally and externally regarding threat details
- **Diamond Model**: complementary model to the Cyberthreat Kill Chain to track attack groups over time rather than individual attacks
    - For every intrusion event there exists an adversary taking a step towards an intended goal by using a capability over infrastructure against a victim to produce a result
### Phases of Incident Response
1. Preparation
    - Identify Team Members
    - Define Roles and Responsibilities
    - Develop Defense-in-Depth Strategies
2. Detection and Analysis
    - Determine the level of impact
    - Analyze event/log files from IDS and firewalls, routers, switches, directory servers, and other networked systems
    - Determine the true intent of the attack
3. Containment
4. Eradication
    - Disabling affected accounts
    - Shutting down ports and protocols
5. Recovery
    - Recover form backups
    - Coordinate with other sites/locations
6. Document Lessons Learned
### Types of Testing and Exercises
- **Walk-through**: reading through the proposed plan and gather feedback
- **Communications**: ensuring all relevant personnel, vendors, and emergency responders are identified and identify gaps in response times/availability
- **Simulation**: having as close to a real-world scenario with some variability/randomness (AKA table-top exercise)
- **Partial Exercise**: preparing for disaster recovery (can be somewhat intrusive and may disrupt normal operations)
- **Full Exercise**: complete testing of the business continuity and disaster recovery plans (most disruptive to a business)
### Types of Plans
- **Incident Management**: deals with the initial response to an incident
    - Tasks, actions, and priorities
    - Emergency contact details
    - Contact guidelines, internal, media, emergency responder, etc.
- **Business Continuity**: deal with resumption and recovery of business operations once the initial disruption is contained
    - How to begin recovery
    - Location of key personnel/resources
    - Standardized data collection and reporting template, forms, portals, etc.
- **Disaster Recovery**: similar to business continuity but focused on information technology
    - Includes tasks, action lists, order of recovery, etc.
    - Emergency contact info, documentation/references to incident management/command center location
- **Business Resumption**: defines who owns the resumptions process (can be the same/part of the business continuity plan)
    - Process for determining replacement of staff, buildings, infrastructure, services, etc.

## Appropriate Data Sources to Support an Investigation
### Definitions
- **syslog**: developed as a part of a sendmail implementation for collecting system logs (UDP port 514)
- **syslog-ng**: extended syslog functionality with TCP, content-based filtering, database logging features, and TLS encryption
- **rsyslog**: added buffered operation support and Reliable Event Logging Protocol (RELP)
- **journalctl**: Linux command to view systemd, kernel, and journal logs
- **nxlog**: multi-OS log collection/aggregation platform that aggregate, filters, enriches data, and integrates with SIEM software
- **Bandwidth Monitors**: monitor network traffic/bandwidth to identify anomalies, IOCs, data exfiltration, and unusual traffic
- **Metadata**: data that provides information about other data
- **Protocol Analyzers**: packet inspection tools used to troubleshoot network issues, detect/inspect IOCs, decrypt SSL transmission, etc.

## Mitigation Techniques to Secure and Environment
### Definition
- **Application Whitelisting**: a list of applications allowed to be run on a client
    - Blacklisting is a list of applications not allowed to be run on a client
- **Quarantine**: proactively blocking access or the ability to run/execute hosts that don't meet certain criteria or applications/processes that are flagged as suspicious/malicious

## Key Aspects of Digital Forensics
### Definitions
- **Computer Forensics**: analysis of digital data to aid in an investigation or make a determination of criminality
- **Legal Hold**: data that has been identified as material to an investigation
- **Non-Repudiation**: accountability/inability to refute an action, ownership, etc.

# Governance, Risk, and Compliance
## Comparing and Contrasting Types of Controls
### Definitions
- **Deterrent**: systems or signage that is designed to discourage people from doing something
- **Preventative Controls**: designed to keep someone from doing something
- **Detective Controls**: detect activity and initiate some type of action
- **Corrective/Recovery Controls**: used to get a system back to normal
- **Compensating Controls**: provides an alternate solution to a countermeasure that is too difficult or too expensive to implement

## Regulations, Standards, and Frameworks that Impact a Security Organization
### Definitions
- **General Data Protection Regulation (GDPR)**: privacy and security law from the EU in 2018 that imposes obligations onto organizations anywhere, so long as they target or collect data related to people in the EU
    - Provides individuals (data subject) more control over how organizations process, or control the processing of their data
- **Processing**: any operations, whether automated or manual, that is performed on personal data
- **Data Processor**: responsible for the processing of personal data on behalf of data controllers
- **Data Controller**: determine the purpose and the means by which personal data is processed
- **Compliance**: adherence to a set of rules pertaining to people, process, and technology as it relates to policies, standards, regulations, laws, etc.
### GDPR Data Processing Principles
1. Lawfulness, fairness, and transparency
2. Purpose limitation
    - Specified and explicit
3. Data minimization
    - Only what is necessary
4. Accurate and where possible kept up to date
5. Storage limitation
    - Kept only as long as necessary
6. Integrity and confidentiality
    - Data kept secure
### GDPR Legal Grounds for Processing Data
- Consent
- Legitimate Interest
- Contract
- Legal Obligation
- Public Authority
- Vital Interest

## Sources
- [Official CompTIA Security+ Site](https://www.comptia.org/certifications/security)
- [Pluralsight Security+ (SYO-601) Course](https://www.pluralsight.com/paths/comptia-security-sy0-601)
- [Christopher Rees Pluralsight Bio](https://www.pluralsight.com/authors/chris-rees)