---
title: "CompTIA Security+: Architecture and Design"
date: 2024-06-10
tags: ["CompTIA", "Certification", Security+]
image : "/posts/Security+_pt1.webp"
Description: "Part two of my notes for the CompTIA Security+ Certification covering Architecture and Design concepts."
---
*Note: Much of the below information is summarized from Christopher Rees' Security+ training course hosted on Pluralsight. Much credit goes to Chris' expertise! Check out his courses in the sources*

Continuing with my notes from studying for the CompTIA Security+ exam. The exam breaks down its curriculum into several sections, and this portion of my notes covers the "Architecture and Design" content.
Please keep in mind these are only my notes, and should not be used as the sole resource to study for the Security+ certification. Additionally, since taking the exam, a new version has been published, meaning some of the below content may be out of date/missing important details.

- [Architecture and Design](#architecture-and-design)
  - [Enterprise Security Concepts](#enterprise-security-concepts)
    - [Definitions](#definitions)
    - [Types of Data to Secure](#types-of-data-to-secure)
  - [Virtualization and Cloud Computing](#virtualization-and-cloud-computing)
    - [Definitions](#definitions-1)
    - [Type of Clouds](#type-of-clouds)
    - [Types of Virtualized Servers](#types-of-virtualized-servers)
    - [Steps to Avoid VM Sprawl](#steps-to-avoid-vm-sprawl)
  - [Implementing Secure Application Development, Deployment, and Automation](#implementing-secure-application-development-deployment-and-automation)
    - [Definitions](#definitions-2)
    - [Environments](#environments)
    - [Secure Coding Techniques](#secure-coding-techniques)
  - [Authentication and Authorization Methods](#authentication-and-authorization-methods)
    - [Definitions](#definitions-3)
    - [Efficacy Rates](#efficacy-rates)
  - [Cybersecurity Resilience](#cybersecurity-resilience)
    - [Definitions](#definitions-4)
    - [Backup Types](#backup-types)
  - [Security Implications of Embedded and Specialized Systems](#security-implications-of-embedded-and-specialized-systems)
    - [Definitions](#definitions-5)
  - [Physical Security Controls](#physical-security-controls)
    - [Definitions](#definitions-6)
    - [Data Destruction](#data-destruction)
  - [Cryptographic Concepts](#cryptographic-concepts)
    - [Definitions](#definitions-7)
    - [Common Use Cases](#common-use-cases)
    - [Cryptographic Methods and Design](#cryptographic-methods-and-design)
    - [Homomorphic Encryption](#homomorphic-encryption)
  - [Sources](#sources)

# Architecture and Design
## Enterprise Security Concepts
### Definitions
- **Configuration Management**: the management and control of configurations for an information system with the goal of enabling security and managing risk
    - The method of determining what's normal
- **Standardization**: the more standardized things are, the easier they are to maintain, deploy and troubleshoot
- **Data Loss Prevention (DLP)**: detects potential reaches and exfiltration of data
- **Data Masking**: hiding/obfuscating data from people who should not have access to it (partial access)
    - **IP Address Masking**: enabling private IP addresses on a network to allow them to connect to the internet, but restricting non-members of the private network from seeing IPs within
- **Tokenization**: replacing sensitive data with non-sensitive equivalent
    - Can be single use, multiple use, cryptographic, or non-cryptographic, reversible, irreversible, etc.
    - **High-Value Tokens (HVTs)**: used to replace things like primary account numbers on credit card transactions, but to specific devices
    - **Low-Value Tokens (LVTs)**: can serve similar functions as HVTs, but needs the underlying tokenization system to match it back to the actual PAN
- **Digital Rights Management (DRM)**: suite of tools designed to limit how/where content can be accessed
- **Trusted Platform Module (TPM)**: a hardware chip embedded on a computer's motherboard used to store cryptographic keys used for encryption
- **Hardware Security Module (HSM)**: similar to a TPM but removable/external devices that can be added later
- **Cloud Access Security Broker (CASP)**: ensures policies are enforced when accessing cloud-based assets
    - Placed between the company/consumer and the cloud provider
- **Honeypot**: computers or hosts that are set up specifically to become targets of attacks
- **Honeyfile**: similar to a honeypot but applies to individual files designed to entice bad actors and monitor their activities
- **Honeynet**: similar to a honeypot but larger in scale applying to an entire network setup
- **DNS Sinkhole**: DNS server that supplies false results
### Types of Data to Secure
- **Data At-Rest**: data sitting on a hard drive/removable media
    - Local to the computer or remotely on SAN or NAS storage
- **Data In-Transit**: data that is being sent over a wired or wireless network
    - VPN connection will encrypt the data while in transit (wired or wireless)
- **Data In-Use**: data not "at rest" and only on one particular node on a network
    - Could be memory resident,temp space, etc.

## Virtualization and Cloud Computing
### Definitions
- **The Cloud**: storage external to a company's data center accessible from an outside network
- **Cloud Computing**: the virtualization of infrastructure, platform, and services
- **Multi-tenant**: where many users can use the same set of resources
- **Infrastructure as a Service (IaaS)**: allows for distribution and consumption of resources as a service. Leverages automation and self-service, enabling a customer to select their own hardware/software configurations and provision their own infrastructure
    - Multiple users can utilize the same infrastructure (multi-tenant)
    - Allows for elastic scaling as needs and demands increase/decrease
- **Platform as a Service (PaaS)**: environment comprised on computational resources (test/dev environments) that can be easily created and configured
    - Avoids having to order/acquire rack/stack hardware, configure network, IP addresses, load balancers, VLANS, install software, etc.
    - Test environments can be quickly created, expand as needed, run tests, report, and tear down on-demand
- **Software as a Service (SaaS)**: applications that are provided on demand (no setup, installation, or configuration required)
- **Managed Service Provider (MSP)**: deliver services either on-prem at customer site, in the MSP's data center, or in a third-party data center
- **Managed Security Service Provider (MSSP)**: provide outsourced monitoring and management of security devices and systems (usually 24/7 monitoring) 
- **Fog Computing**: extends cloud computing to the network edge
    - Compromised of compute, network, and storage
    - **Edge Computing**: puts resources close to where the data is created
- **Virtual Desktop Infrastructure (VDI)**: centralized hosting and management of desktop images (users can access their desktop from the server)
    - **Application Streaming**: applications are packaged and streamed to hosts (each application has its own computing environment)
    - **Terminal Services**: applications run on the server and displayed to hosts (users received graphic updates, mouse/keyboard events, etc.)
- **Virtualization**: taking the capabilities and "personality" of a physical device and converting to a virtual representation
    - Can perform the *same functions* as its physical counterpart
- **Microservice**: treats each function of an application as an independent service that can be altered, updated, or taken down without affecting the rest of the application
- **Infrastructure as Code (IAC)**: methodology to create repeatable processes for deploying infrastructure
- **Software Defined Networking (SDN)**: reducing routers/switches to "dumb devices" with intelligence handled by a centralized controller suite with a wholistic view of the network and programmatic tuning based on activity, workloads, etc.
- **Software Defined Visibility**: "visibility fabric" that can be in-line or out of band and monitor the entire network to proactively respond to events and adjust traffic, shut down ports, log/alert, capture traffic decrypt/inspect SSL, etc.
- **Serverless Architecture**: only the code is managed/deployed and can scale at the individual call level (pay only for the times the function is called vs. paying for an application to always be on and waiting for requests)
- **Transit Gateway**: connects Virtual Private Clouds (VPCs) with on-premise networks
    - Controls how traffic is routed among all connected networks (hub and spoke architecture)
- **VM Sprawl**: a large number of virtual machines on a network without proper IT management
- **VM Escape**: attack that allows an attacker to escape out of their VM and access resources on the host
### Type of Clouds
- **Private**: you manage and maintain all resources
- **Public**: cloud provider manages resources
- **Hybrid**: public and private mix (starts internally usually)
- **Community**: resources are shared among several groups
### Types of Virtualized Servers
- **Type 1**: host runs on bare metal server and guests run on the host (ex: VMware)
- **Type 2**: host runs on top of OS and guests run inside of host (Virtual Box)
- **Container Based**: has the application/binaries run on top of the OS itself without needing a hypervisor (shares OS Kernel)
### Steps to Avoid VM Sprawl
- Define virtual machine policy
- Create standard VM templates
- Implement lifecycle management
- Routinely audit

## Implementing Secure Application Development, Deployment, and Automation
### Definitions
- **Integrity Management**: open source alternative that creates a measured runtime environment to prevent sophisticated or targeted persistent attacks
    - Creates a list of components that need to load
    - Anchors that list to the TPM chip to prevent tampering
- **Security Automation**: automating the process of implementing rules, enforcing policies, and making changes based on triggers or policy violations
- **Continuous Integration**: merging developer updates continuously (daily) to avoid integration challenges
- **Continuous Delivery**: extension of continuous integration, automation of the release process in addition to automated testing
- **Continuous Deployment**: automates the continuous delivery process where all changes that pass all stages of a pipeline are automatically released to the customer
- **Software Diversity**: creating functionally equivalent, but internally different variants of a program
### Environments
- **Development**: initiation and requirements gathering
- **Test**: can take different forms and can be integrated throughout all phases, typically prior to, or "lower than" staging
- **Staging**: a "production-like" environment to test installation, configuration, and migration scripts
- **Production**: fully functioning live environment
### Secure Coding Techniques
- **Proper Error Handling**: making sure errors don't crash the system, allow for elevated privileges or expose unintended information
- **Proper Input Validation**: sanitize data to mitigate XSS and XSRF
- **Normalization**: ensure database integrity and optimization of data
- **Stored Procedures**: utilize vetted, secure procedures vs writing new code on the fly
- **Code Signing**: ensure validated, trusted code is used and mitigate risk from unsigned code being allowed to run
- **Encryption**: encrypting the data mitigates the risk of compromise should the computers or drives housing the data be lost or stolen
- **Obfuscation/Camouflage**: masking the data to avoid detection by static code analysis
- **Code Reuse/Dead Code**: code that can be used for some future use, project, etc. Typically better to write clean code that can be minimally modified/refactored in the future
- **Server-Side vs. Client-Side**: taking into account where validation, input sanitization, etc. occurs and ways those controls could be bypassed
- **Memory Management**: ensure code calls and managed memory properly to avoid heap and buffer overrun errors
- **Third Party Libraries & SDKs**: ensure you understand any third party's security requirements, vetting process, where their data is stored, interaction with other apps/data/etc.
- **Data Exposure**: what types of data are exposed if unexpected inputs crash the system or cause an unintended result
- **Stress Testing**: placing load on the system or application to see where the performance and usability breakpoints exist
- **Sandboxing**: isolating the application from other systems to enable testing without impact to other applications, production, etc.
- **Model Verification**: testing to verify the produced product/application aligns with the proposed models

## Authentication and Authorization Methods
### Definitions
- **Directory Services**: provides authorization and authentication
    - **Lightweight Directory Active Protocol (LDAP)**: protocol used to talk to Active Directory
- **Federation**: allowing access to company resources to outside parties
- **Attestation**: used to prove that a system is secure and operates from a secure code base
- **Time-Based One-Time Password (TOTP)**: unique password that uses time-based algorithm to generate the password
- **Hash Message Authentication Code(HMAC)-Based One-Time Password (HOTP)**
- **Token**: authentication mechanism that can identify and authenticate by telling servers/resources what access rights a user possesses to allow or deny access
- **Static Codes**: codes that can be created and stored as backup and/or for one-time use
- **Personal Identification Verification Card (PIV)**: United State Federal smart card that grants cardholders access to federal facilities and information systems
- **Common Access Card**: smart card issued by the Department of Defense enabling general identification mechanism to access computers, signing email, etc.
- **Vein Analysis**: biometric authentication using the vein pattern in a human finger
    - Insert finger into an attester terminal to capture images of veins under the fingers/hand using near-infrared LED light
- **Gait Analysis**: identifying a person based upon their unique walking pattern
- **Identification**: who you are (label such as username, security ID, etc.)
- **Authentication**: proving who you are/the process of validating an identity (username/password combo, biometric data, etc.)
- **Authorization**: permissions (what you're allowed to access once authenticated)
- **Accounting**: tracks the start and stop time of each session (can be used for billing or "showback")
### Efficacy Rates
- **False Acceptance Rate (FAR)**: probability that the system incorrectly authorizes a non-authorized person
- **False Rejection Rate (FRR)**: probability that the system incorrectly rejects access to an authorized person
- **Crossover Error Rate (CER)**: rate where both accept and reject error rates are equal (a good system should have equal FAR and FRR)

## Cybersecurity Resilience
### Definitions
- **Redundant Array of Independent/Inexpensive Disks (RAID)**: fault tolerant array of disks where data is mirrored or spread across multiple disks (parity is used to recreate data in the event of drive failure)
    - RAID 0 (Disk striping): not fault tolerant
    - RAID 1 (Disk mirroring)
    - RAID 5 (Disk striping with parity)
    - RAID 6 (Disk striping with double parity)
    - RAID 10 (Disk striping that is mirrored)
- **Multipath**: a redundancy concept that provides multiple paths from point "A" to point "B"
- **Load Balancer**: devices that will spread the incoming load among multiple pieces of infrastructure
- **Uninterruptible Power Supply (UPS)**: battery backup that provides power in the event of a disruption
- **Dual Supply**: power is supplied by dual feeds independent of one another
- **Managed Power Distribution Units (PDUs)**: provides the ability to monitor and control critical factors such as voltage, current, and power factor
- **Non-Persistence**: prevents people from customizing their desktops, installing unapproved applications, tweaking settings, etc.
- **Snapshots**: allow a user to quickly revert to a known good state or rollback changes in the event of a virus, malware, spyware is installed
- **Live Boot Media**: operating system on USB drive or removable media to allow cleaning of a system, removing malware, etc.
- **High Availability**: two or more systems that are in sync or near-real time
- **Clustering**: multiple servers operating as one
- **Fault Tolerant Hardware**: having redundant components in case one fails, operations can continue
- **Technology Diversity**: utilizing more than one type of technology to accomplish a given task
- **Crypto Diversity**: rotate cryptographic keys; use technology from more than one provider
### Backup Types
- **Differential**: data that has changed since the last full backup
- **Incremental**: data that has changed since the last incremental backup
- **Full**: all data is backed-up each time
- **Snapshot**: point in time copy of the data, that typically maintains pointers to the original data rather than copying the data itself

## Security Implications of Embedded and Specialized Systems
### Definitions
- **Embedded System**: microprocessor-based computer hardware system with software that is designed to perform a dedicated function
    - At its core, it is an integrated circuit designed to carry out computation for real-time operations
- **Supervisory Control and Data Acquisition (SCADA)**: refers to centralized systems which monitor and control entire sites, or complexes of systems spread out over large areas
    - **Remote Terminal Unit (RTU)**: connects to sensors that convert the sensor information into digital data
    - **Programmable Logic Controller (PLC)**: similar to RTUs but more versatile and economical
    - **Human Machine Interface (HMI)**: presents data to a human operator who then acts upon the data
    - **Master Terminal Unit (MTU)**: sends instructions and accepts input from the various RTU or PLC devices
- **Real-Time Operating System (RTO)**: designed to process data with minimal delay or latency, more concerned with deterministic processing of data than with the amount of work that can be performed
- **System on a Chip (SoC)**: integrated circuit (IC) that integrates all component of a computer or other systems onto a single substrate or chip
- **Narrow-band**: small amounts of data transfer, < 10sec latency, with secure mechanism built-in
- **Baseband Radio**: dedicated processors that run RTOs and control radio functions (except Wi-Fi and Bluetooth)
- **Zigbee**: suite of high-level communication protocols used for PANs
    - Low-power (batter powered), low data rate, low latency, and close proximity wireless ad-hoc network
    - Operates in the industrial, scientific, nd medical (ISM) radio band

## Physical Security Controls
### Definitions
- **Mantraps**: access control via two sets of doors where a person will enter a first set of doors that will close behind them, then then need a guard/automated control to provide access through the second door after authentication
- **Two Person Integrity (TPI)**: control mechanism designed to achieve a high level of security for especially critical material or operations where two people must be present at all times when sensitive material is being handled
    - Two locks on any containers containing sensitive material
    - No one person can possess both keys
- **Air Gap**: method of isolating a computer or network from the internet/external networks
- **Demilitarized Zone (DMZ)**: typically consist of hosts that provide services to users outside of the local (internal) network
- **Protected Distribution Systems (PDS)**: secure conduit for copper or fiber optic cabling with monitors in place to detect any disruption to the PDS
    - Hardened Distribution Systems:
        - Hardened Carrier: conduit is electrical metal tubing, ferrous conduit or pipe that is permanently sealed (welds, expoxy, etc.) and if run underground, are also encased in concrete
        - Alarmed Carrier: fibers within the conduit are used for monitoring acoustic vibrations associated with attempted access which reduces the need for visual inspection/monitoring
        - Continuously Viewed Carrier: conduit is continuously viewed/monitored 24/7/365 and guards will investigate any attempts to disturb the PDS within 15 min of an alert
    - Simple Distribution Systems: cables can be installed in a carrier and made of any material. Access points are monitored by personnel who periodically inspect it and they must be cleared to the highest level of data handled by the PDS
- **Hot and Cold Aisles**: arranging a data center in such a way to maximize efficiency to properly cool server racks while effectively disposing of heat
### Data Destruction
- Non Digital Data Destruction:
    - Burning: documents are incinerated (can be combined with other methods)
    - Shredding: documents are cut into small pieces
        - Long-cut shredders are not considered secure
        - Cross-cut shredders are more secure, but slower and more expensive
    - Pulping: paper is soaked in a solution until it is reduced to a slurry
        - Can be expensive, time-consuming, and difficult to transport
    - Pulverizing: storage media is fed into a pulverizing machine
        - Hydraulic/pneumatic action used to reduce media to loose fibers/shards
- Digital Data Destruction:
    - Degaussing: using AC/DC erasure techniques to render data unrecoverable
        - Hard drives are typically unusable after degaussing as it erases low-level formatting that is only done at the factory at the time of manufacture
    - Purging: removes data remanence so that data cannot be reconstructed by any known means(AKA sanitizing)
        - Considered a step beyond wiping data, and is performed in situations where highly sensitive data exists
    - Wiping: overwrites data "x" number of times to ensure it is unrecoverable
        - For SSD disk sanitation, resets the NAND and marks all blocks as empty

## Cryptographic Concepts
### Definitions
- **Cryptography**: the practice and study of hiding information
- **Cryptanalysis**: discovering some weakness or insecurity in a cryptographic scheme
- **Encryption**: the method of transforming data (plaintext) into an unreadable format
- **Plaintext**: the (readable) format of data before being encrypted
- **Ciphertext**: the "scrambled" format of data after being encrypted
- **Decryption**: the method od turning cipher text back into plaintext
- **Encryption Algorithm**: a set of rules or procedures that defines how to encrypt and decrypt data (AKA encryption cipher)
- **Key**: a value used in the encryption process to encrypt and decrypt (AKA cryptovariable)
- **Digital Signatures**: asymmetric encryption using public-key/private-key (PKI)
- **Key Stretching**: pseudorandom function applied to a password or passphrase
    - Password-Based Key Derivation Function 2 (PBKDF2)
    - Salt for randomness
    - Bcrypt
- **Out-of-Band Key Exchange**: transmitting a key via manual means (in-person, telephone, courier, etc.) so that it is not sent over the network
- **In-band Key Exchange**: transmitting a key over the network as the communication session is established
    - Created in real time and typically discarded once the session is over
- **Elliptic Curve Cryptography (ECC)**: asymmetric encryption using algebraic structure of elliptic curves
    - Makes strong encryption using a smaller key size with less resources
- **Perfect Forward Secrecy**: session keys that are derived from a set of long-term keys, yet discreet in nature
    - If a long term key is compromised it doesn't compromise the session key or the data it protects
- **Ephemeral Key**: temporary key that is used once (can be used to derive an additional key to be used for subsequent communication)
- **Cipher Modes**: algorithms or methods used to encrypt data
    - **Counter Mode (CTR)**: random 64-bit block as first Initialization Vector (IV). Increments a specified number of each subsequent block of plaintext
    - **Galois/Counter Mode (GCM)**: used with symmetric key block ciphers and is very efficient
- **Blockchain**: immutable, decentralized digital ledger that is distributed among a network of many computers. Once a transaction is recorded, it can't be altered or removed
    - **Block**: batch of transactions with a cryptographic hash of the prior block, timestamp, and other info
- **Block Cipher**: encrypts in fixed length chunks (blocks) of data at a time
- **Stream Cipher**: encrypts one bit at a time using a pseudorandom cipher digit stream (keystream)
- **Session Keys**: single-use symmetric key used for encrypting all communication in one communication session
    - Can use an asymmetric key to encrypt the session key itself
- **Symmetric Encryption**: uses the *same* key to encrypt and decrypt a piece of data (AKA shared/secret key encryption)
- **Asymmetric Encryption**: uses a two key (Public/Private Key) system
    - **Key Pair**: one key for encryption, the other fo decryption
- **Lightweight Cryptography**: encryption method that utilizes low computational power or energy consumption
**Kerckhoffs' Principle**: a cryptosystem should be secure even if everything about the system, except the key, is public knowledge
### Common Use Cases
- Low Power Devices: ECC uses low power consumption, making it suited for mobile device security
- Low Latency: symmetric key cryptography is quick and uses the same key for encryption and decryption
- High Resiliency: cryptosystems that are made public, allowing the community to test, vet, and discover vulnerabilities
### Cryptographic Methods and Design
- **Electronic Code Book (ECB)**: the same plaintext will produce the same ciphertext every time. Should only be used for transmitting small amounts of data as patterns are easy to distinguish
- **Cipher Block Chaining Mode (CBC)**: similar to ECB but inserts (via XORing) some of the cipher text created from the previous block of data into the the next block (an IV is used in the first block)
- **Output Feedback Mode (OFB)**: makes a block cipher into a stream cipher as the entire output of the previous block is used as input for the next block's encryption (transmission errors do NOT propagate throughout the encryption process)
- **Cipher Feedback Mode (CFB)**: Same as OFB but transmission errors are allowed to propagate through the encryption process
### Homomorphic Encryption
- **Partially Homomorphic Encryption**: allows select mathematical functions to be performed on encrypted values
    - One operation (addition or multiplication) can be performed an unlimited number of times on the ciphertext
- **Somewhat Homomorphic Encryption**: select mathematical function to be performed (addition or multiplication), but the operations can only be performed a set number of times
- **Fully Homomorphic Encryption**: capable of both addition and multiplication any number of times and makes secure multi-party computation more secure

## Sources
- [Official CompTIA Security+ Site](https://www.comptia.org/certifications/security)
- [Pluralsight Security+ (SYO-601) Course](https://www.pluralsight.com/paths/comptia-security-sy0-601)
- [Christopher Rees Pluralsight Bio](https://www.pluralsight.com/authors/chris-rees)