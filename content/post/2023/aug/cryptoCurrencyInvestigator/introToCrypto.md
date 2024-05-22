---
title: "Introduction to Cryptocurrency Investigations"
date: 2023-08-21
tags: ["Crypto", "Certification"]
image : "/posts/introToCrypto.png"
Description: "Introduction to cryptocurrency investigations including what is crypto and how it works."
---
*Note: Much of the below information is summarized from [Blockchain Intelligence Group's](https://blockchaingroup.io/) Certified Cryptocurrency Investigator [certification training course](https://cryptoinvestigatortraining.com/?). Much credit goes to expertise of everyone at the Blockchain Intelligence Group! Check out their website and partners the sources*

Cryptocurrency investigations are an essential part of modern day criminal investigations. Regardless of the crime committed, cryptocurrency is becoming a growing method of payment for illicit activities. Being that cryptocurrency alone is not illegal with countless real world positive use cases, it is essential that investigators understand how cryptocurrencies operate, both at a technical level real world situations. This post will dive into what cryptocurrency is, how it works, how it's exchanged and regulated, and real world uses of it to better understand crypto as a whole.

## Table of Contents
- [Table of Contents](#table-of-contents)
- [Introduction to Cryptocurrency and Digital Assets](#introduction-to-cryptocurrency-and-digital-assets)
  - [Virtual Currency](#virtual-currency)
  - [Types of Crypto](#types-of-crypto)
  - [How Crypto Works](#how-crypto-works)
    - [Types of Wallets](#types-of-wallets)
    - [Popular Wallets](#popular-wallets)
    - [Popular Exchanges](#popular-exchanges)
  - [Regulating Crypto](#regulating-crypto)
    - [Key Financial Terms and Acronyms](#key-financial-terms-and-acronyms)
- [All About Bitcoin](#all-about-bitcoin)
  - [The Beginning](#the-beginning)
  - [Blockchain Technology](#blockchain-technology)
  - [The Original Bitcoin Fork](#the-original-bitcoin-fork)
  - [Acquiring Bitcoin](#acquiring-bitcoin)
- [Crypto and Crime](#crypto-and-crime)
  - [Laws and Legislation](#laws-and-legislation)
  - [Investigations](#investigations)
- [The Dark Web](#the-dark-web)
- [Sources](#sources)

## Introduction to Cryptocurrency and Digital Assets
- **Fiat Currency**: currency that has been declared as legal tender by a government
    - Typically paper money or coins used to pay for goods
- **Virtual Currency** (AKA Digital Currency): a digital representation of value that can be digitally traded and function as one of the following:
    1. a medium of exchange
    2. a unit of account
    3. a store of value (but does not have legal tender status in any jurisdiction)

### Virtual Currency
- Digital currency is neither issued nor guaranteed by any jurisdiction and only functions by agreement within the community of users of the currency
- There are two types of virtual currency:
1. **Centralized Virtual Currency**: a virtual currency that is backed by a commodity or is issued by a single party who keeps a ledger of the value and balances
    - Ex: hotel points, airline miles, digital rewards, etc.
2. **Decentralized Virtual Currency**: a virtual currency with no central authority where the ledger is maintained by a number of network nodes. Typically cryptocurrencies are held on the blockchain and are continuously updated by thousands of voluntary computer nodes around the world
    - Ex: cryptocurrencies
- **Blockchain**: the ledger for decentralized virtual currencies in which all transactions are confirmed by cryptography and is updated on a frequent basis. Often made up of many network nodes, each of which carry a complete copy of the blockchain
- **Cryptocurrency**: digital assets that are verified on a blockchain using cryptography
    - At it's most basic form, cryptocurrency is just entries in a blockchain/database (or some public ledger) that is nearly impossible to change
- **Trustless Currency**: a currency in which there is no third-party entity maintaining the ledger which is open and accessible to everyone
    - **Trustless Transaction**: the transfer of value between parties that may not know or trust one another

### Types of Crypto
- **Bitcoin**: a peer-to-peer version of electronic cash that allows online payments to be sent directory from one party to another without needing to go through a financial institution
    - The original cryptocurrency created by Satoshi Nakamoto, an unknown inventor
        - Concept was first formed when Satoshi published a white paper entitled "Bitcoin: A Peer-to-Peer Electronic Cash System"
- **Ethereum** (Ether): a coin designed in the hopes of using a blockchain to replace third parties
    - One of the most prevalent coins on the market
    - Designed and used solely on the Ethereum platform by Vitalik Buterin in 2015
    - Implemented to perform functions other than a method of only transferring value
        - Such as transferring mortgages and to keep track of complex financial instruments using smart contracts
    - **Smart Contracts**: contacts that are converted to computer code, stored and replicated on the system, and supervised by the network of computers that run the blockchain
        - AKA self-executing contracts, blockchain contracts, or digital contracts
        - Defines the rules and penalties around the agreement and automatically enforces them
        - Ethereum is sometimes referred to as the worlds first computer for its ability to run applications through smart contracts
- **Monero**: fungible cryptocurrency that has a high level of privacy
    - Based on the CryptoNight proof-of-work has algorithm
    - More difficult to establish links between subsequent transactions
        - As a result, it is commonly used by illicit actions
    - **Fungible**: being interchangeable with other units of currency
- **Zcash**: uses addresses to shield and protect a transaction's sender or receiver
    - Zcash addresses are called "z-addr" or "t-addr"
    - Protects the transaction participants by making transactions either transparent or shielded
        - Making it hard to uncover the identity of potentially illicit transactions
    - Provides a "selective disclosure" option to allow users to prove payment for auditing purposes
- **Dash**: aims to be the most friendly and scalable payments-focuses crypto in the world with instant transaction confirmation, double spend protection, and anonymity equal to physical cash
    - The Dash network is a self-governing, self-funding model driven by incentivized full nodes and a clear roadmap for on-chain scaling up to 400MB blocks using custom-developed open source hardware
    - Based on Bitcoin and compatible with many key Bitcoin ecosystem components
        - Dash's two-tier network structure offers significant improvements in transaction speed, anonymity, and governance
- **Litecoin**: peer-to-peer cryptocurrency and open source software project
    - Nearly identical to Bitcoin
        - Processed faster than Bitcoin with rates of 2.5 minutes for one block (vs Bitcoin's 10 minutes)
    - Uses a script hashing algorithm requiring more complicated and expensive mining devices
- **Tether (USDT)**: a US dollar pegged stablecoin that can be found on Omni, Ethereum, EOS, Tron, Algorand, and OMG blockchains
- **Binance USD**: US dollar stablecoin that operates on its own Blockchain called Binance Chain which powers the BNB Chain ecosystem
- **USD Coin**: a stablecoin fully collateralized by USDC, DAI, and USDT
    - Available on Polygon, Binance, and Avalanche blockchains
- **Terra**: a stablecoin hosted by the Terra network and created by Singapore's Terraform Labs
    - This coin failed in 2022 which lead to a large crypto market crash
- **Alt Coins** (AKA Alternative Coins): term referring to any coins other than Bitcoin
    - Since the beginning of Bitcoin in 2009, there have been many new coins, currently almost 10,000
    - Alt Coins have different traits than Bitcoin
    - **Pump and Dump Scheme**: when an alt coin is designed to get people to invest in that coin so developers can abandon the market and flee with a large cache of investor money
- **Privacy Coins**: crypto coins that offer privacy features like anonymity and untraceability as a part of the core design
    - Examples include Monero, Dash, and Zcash
- **Initial Coin Offerings (ICO)**: when founders of a company will create and sell a proprietary company cryptocurrency to investors in exchange for a more practical means of money (fiat or Bitcoin typically)
    - A lucrative way for tech startups to raise initial capital without worrying about traditional funding regulations
    - Investing in ICOs is inherently risky as the product/service they represent does not yet exist
    - ICO projects are a magnet for cybercriminals
        - They are often vulnerable to attack, each ICO containing an average of five separate vulnerabilities (With 47% of those being medium-high severity)
    - Government regulations have been cracking down on ICOs as they are viewed as investments and should be treated with the same financial scrutiny/regulations as any other investment type
    - **Ethereum Request for Comment (ERC)**: the typical platform chosen by companies using ICOs because:
        1. The Ethereum blockchain has its own scripting language built into it allowing for smart contacts and automation
        2. ERC allows for each creation of decentralized applications (DApps) which removes the requirements of a centralized server in favor of the blockchain
        3. It allows for virtually unlimited coin creation due to being open source (allows for easy forking for modifications)

### How Crypto Works
- **Digital Wallets**: where cryptocurrency is stored, secured with asymmetrical cryptography using key pairs
    - **Public Key**: key to be publicly shared in a transaction and used as the address of the wallet
        - A string of 27-24 alphanumeric characters
            - Typically begin with `1`, `3`, or `bc1` for Bitcoin keys
    - **Private Key**: key known only to the wallet owner that can unlock the wallet and its contents
        - A 128, 256, or 512 bit number represented in 256 or 54 alphanumeric characters
- **Mnemonic Seeds**: a "recovery or reset password" tool in the case the original wallet is lost, seized, or destroyed by using a seemingly random list of words that associate to a wallet software when entered
    - To recover a wallet, one can get a wallet device that is the same type as the original, enter the mnemonic seed, and the original wallet is recovered via cloning the key pairs (similar to a security question recovery)
- There are two types of transaction fees associated with using crypto
    - **Exchange Fees**: a fee incurred by whatever digital currency exchange is in use (usually 1-5%)
    - **Transaction Fees**
- Cryptocurrency has five transactional properties that makes it more beneficial than traditional centralized transaction processes
    1. It's irreversible
    2. It's pseudonymous/highly anonymous
    3. It's fast and global
    4. It's secure
    5. It's permissionless
- Crypto has two unique monetary properties
    1. It has a controlled supply
        - Most cryptocurrencies limit the supply of generated tokens to provide transparency about the monetary supply of the crypto at any point in the future
            - Bitcoin for example decreases supply overtime and will reach a max number in 2140 when 21 million Bitcoins have been mined
    2. It represents tangible value, not debt
        - Normal banks use ledgers that track debts while cryptocurrencies only represent their value

#### Types of Wallets
- **Hot Wallet**: a wallet that is connected to the internet
- **Cold Wallet**: a wallet that is offline, not connected to the internet, or air gapped
- **Mobile Wallet**: a wallet that is stored on a mobile device, primarily phones
    - Easy to use but less secure
    - Examples: Airbitx, Breadwallet, Bitcoin Wallet, Copay, FreeWallet, Jaxx, Mycelium
- **Desktop Wallet**: a wallet stored on a desktop that often can act as a Bitcoin node containing complete Bitcoin Blockchain copies for more complete transactions
    - More secure than mobile wallets as the keys are stored on the hard drive
    - Examples: Electrum, Exodus, Bitcoin Core, Copay, Armory
- **Web Wallet**: where private keys are stored on the server of the website you create your wallet with
    - Examples: Coinbase, Circle, Strongcoin, Xapo
- **Hardware Wallet**: a physical secure hardware non-internet connected device such as a USB Drive or hard drive that stores the keys
    - Require more setup, are less convenient, and cost more money
    - Examples: Trezor, Keepkey, Ledger HW.1, Ledger Nano S.
- **Paper Wallet**: a physical piece of paper that contains the public and private keys to an account
    - Often printed with a QR code for quick scanning and easy recovery
- **Brain Wallet**: when a wallet user has memorized a passphrase that can be entered into an address generator which is encrypted with SHA256 to provide the public and private key
- **Vanity Wallet**: a wallet generated by using a wallet generation application that contains user determined phrases or numbers
    - Can be time intensive and not very common
- **Split/Multisignature Wallet**: when a Bitcoin wallet is split into three or more distinct addresses that all must be present to conduct a transaction
    - More secure and preferred method for storing private keys

#### Popular Wallets
- **Mycelium**: advanced mobile digital wallet for Bitcoin
- **Exodus**: advanced digital wallet for Bitcoin, Ether, Litecoins, Dogecoins, Dash, and other assets
- **Copay**: multi-interface wallet created by Bitpay
- **Jaxx**: multi-currency/interface digital wallet for Ether, Ether Classic, Dash, DAO, Litecoin, REP, Zcash, Rootstock, and Bitcoin
- **Armory**: open source Bitcoin desktop wallet for advanced users
    - Desktop wallets tend to have a full copy of the Bitcoin blockchain running and can be run as a node on the network
- **Trezor**: a small USB device that acts as a hardware Bitcoin wallet often used for storing large amounts of Bitcoin and other currencies
- **Ledger Nano**: a small USB device that acts as a hierarchical, deterministic, multi-signature hardware wallet for Bitcoin and other currencies
- **Green Address**: user-friendly Bitcoin wallet for beginners
- **Blockchain.info**: popular digital wallet that doubles as a way to explore the Bitcoin blockchain

#### Popular Exchanges
- A digital currency exchange are websites that allow you to exchange fiat currency for digital currency
- **Coinbase**: a multi-digital currency exchange doubling as a wallet service holding the key pairs
- **Binance**: global digital assets platform offering a wide range of derivative trading options
    - One of the most popular exchanges, hosting millions of users
- **Netcoins.ca**: online trading site in British Vancouver, Canada known for being the first regulated crypto exchange in Canada

### Regulating Crypto
- The United States currently allows the legal use of cryptocurrencies, but the regulatory framework surrounding crypto is lacking
    - Federal and State agencies have differing opinions on how crypto markets should be regulated
    - The Internal Revenue Service (IRS) defines crypto as property, while the SEC defines crypto/digital assets as securities
        - Other agencies look at crypto as it is and how it's used
    - Common legal processes used to further an international cryptocurrency investigation in the USA include the USA Patriot Act section 314(a)(b), Mutual Legal Assistance Treaty (MLAT), EGMONT Secure Web (ESW), and Customs Mutual Assistance Agreement (CMAA)
- Internationally countries can have very different methods for how to handle cryptocurrency and can be viewed [here](https://www.perkinscoie.com/en/news-insights/digital-currencies-international-actions-and-regulations-2023.html)
- A big challenge with crypto investigations is that they become global/multi-jurisdictional very quickly
    - Establishing partnerships between Law Enforcement Agencies (LEA) is essential

#### Key Financial Terms and Acronyms
- **Anti-Money Laundering (AML)**
- **Bank Secrecy App (BSA)**
    - BSA/AML Compliance outline the efforts of financial institutions to comply with agreed upon global/country/state standards/regulations to detect and counter money laundering
- **Commodity Futures Trading Commission (CFTC)**
- **Currency Transaction Report (CRT)**: typically for transactions over 10k
- **Financial Action Task Force (FATF)**: global standards body established to combat money laundering and terrorist funding
- **Financial Crimes Enforcement Network (FinCEN)**: a bureau of the US Treasury Department. [link](https://www.fincen.gov/)
    - In 2013 FinCEN issued a guidance of virtual currencies that has become the guiding principle in most US federal agencies
    - This report outline what virtual currencies are, ways in which they are used within Money Service Businesses, and what activities are regulated by who
    - In summary, it states if a business exchanges virtual currency for fiat currency, then the Money Service Business regulatory requirements apply to you and your business must be registered with FinCEN
    - The full report can be found [here](https://d3pg1c2bhy6429.cloudfront.net/114038/d6XFAAb0g2T9ZYUmNwzELA_lbS8eHobKLKBOXqiz/scormcontent/assets/9F8zwP3gx6z43KTW_LPm2AVcpIYqICWcI-application-of-fin-cens-regulations-to-persons-administering-exchanging-or-using-virtual-currencies.pdf)
- **Know You Customer (KYC)**: rules defines by the BSA
- **Money Service Business (MSB)**: any business operating in the exchange of money, including fiat currency to virtual currency (or vice versa)
    - The law referring to the failure to register as an MSB is 18USC1960
- **Suspicious Activity Reporting (SAR)**
- **Security Exchange Commission (SEC)**
- **Specified Unlawful Activity (SUA)**
- **Romance Scams (AKA Pig Butchering)**
- **Trade-Based Money Laundering (TBML)**
- **Third Party Money Laundering (3PML)**
- **Virtual Asset Service Providers (VASP)**: AKA Digital Asset Exchanges, are companies trading in or exchanging cryptocurrency

## All About Bitcoin
- A lot of introductory information about Bitcoin can be found above in the [Types of Crypto](#types-of-crypto) section
- **Bitcoin Mining**: the process of confirming and adding transaction records to the blockchain
    - The reward for mining one block is 12.5 Bitcoin, reducing by half every 210,000 blocks
    - Once a block of transactions is confirmed, the miner who completes the process first is rewarded Bitcoin and then adds the confirmed block to the blockchain, which other nodes will confirm and add to their blockchain copy. The steps are as follows:
        1. Get a computer/server with enough storage running the Bitcoin software
            - Once installed, download the Bitcoin Client to establish oneself as a node
        2. Reach consensus with other nodes to get a complete copy of the blockchain
        3. Receive a new transaction that is broadcast to all miners
        4. As a miner, group the new transactions in a block
        5. Solve a complex computational problem to get the hash number of the new block
        6. After solving the hash, the block is "mined" and the blockchain is updated
            - A block is mined every 10 minutes
        7. The block is validated by other nodes by checking the math and ensuring funds within the listed transactions have not already been spent (avoiding the double spending problem)
            - Bitcoin reward is presented to the first node to mine the block, along with any other transaction fees to offer further incentive
        8. Other nodes stop processing the new block, and use the new block's hash value as the "previous hash" value to solve the next block in queue

### The Beginning
- **Genesis Coins**: the first 50 Bitcoins ever mined back in 2009
    - They were assigned to the the Bitcoin address `1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa.` believed to be owned by creator of Bitcoin Satoshi Nakamoto and referred to as the **Genesis Wallet**
        - It is believed that the Bitcoin community will send funds to this wallet as a "good luck" homage to Satoshi
- **satoshis**: one millionth of a Bitcoin, projected to be utilized primarily after all Bitcoins have been mined and further distribution is needed

### Blockchain Technology
- Each block in the blockchain contains about 2000 transactions (one megabyte of transaction data)
    - Each verified block will have a corresponding hash number which points to the next block, creating the chain
    - The more blocks there are, the harder it is to change information
    - If two conflicting separate chains, then the longer chain will always win, becoming the true blockchain
- A validated block must have a SHA256 hash that begins with four zeros
- A block contains six basic pieces of information:
    1. The block number in the chain
    2. **Nonce Value**: a random number needed to get the computed hash to a valid value (beginning with four zeros)
    3. **Coinbase**: a value attributed to a specific user to identity how much money they have, ensuring they don't overspend
    4. Transactions: all of the transaction information for the block (one megabyte) known as tokens
    5. The previous hash value of the preceding block
    6. The current hash value of the selected block

![Blockchain Visualized](../blockchain_visualization.jpg)
- **Blockchain Nodes**: computers/servers that have a current version of the blockchain and push new Bitcoin transactions to other nodes
    - Nodes are connected to one another, establishing a network that pushes data to the whole network ensuring all nodes contain the same updated information
        - Each node in the blockchain updates its own ledger (copy of the blockchain transactions) about every 10 minutes
    - Anyone can run a node so long as you have a computer with Bitcoin software installed and enough storage space (around 145GB and growing)
        - At any point in time there is on average 12,000 nodes running
    - **Lightweight/Partial Node**: does not store the entire blockchain, only what is needed to perform the validation task
        - It relies on a full node to ensure its information is accurate
    - **Full Node**: stores an entire copy of the blockchain, enforces validation, and puts transactions on the blocks
- **The double spend problem**: the problem of how to prevent someone from spending bitcoin multiple times
    - The implemented solution is to use digital signatures applied to transactions which would be recorded in the peer-to-peer network on a blockchain
    - When stored, these transactions use hash-based proof-of-work that create a record that cannot be changed without redoing the proof-of-work
        - **Largest pool of hash power**: the idea that so long as the majority of the hashing power is controlled by nodes that are not cooperating to attack the network, they'll generate the longest chain and outpace attackers
        - **Consensus**: when a network agrees upon a transaction, then adding it to the public blockchain
- **Single Input-Single Output**: when you provide the exact amount of crypto needed for the transaction
- **Single Input-Multi Output**: when extra crypto is provided in a purchase so change is sent back to the spender
    - **Change Address**: the new address created for change of a transaction
        - After January 30, 2013, all Bitcoin transactions will display the change address (if present) as the last output address listed
- **Multi-Input Transaction**: when multiple addresses consisting of smaller amounts are combined to complete a larger purchase

### The Original Bitcoin Fork
- **Forking**: when a blockchain splits to where there are two valid deviations originating from a starting blockchain now following different rules
- On August 1, 2017 the original Bitcoin blockchain split into two separate blockchains:
    1. Bitcoin Core (BTC), AKA Segwit Chain
    2. Bitcoin Cash Chain (BCH): designed to remove the 1 megabyte block size restriction to allow for faster transactions and network speeds

### Acquiring Bitcoin
- **Cryptocurrency Exchange**: exchange fiat currency, wire transfers, debit, credit, or digital currencies for cryptocurrency
    - AKA digital currency exchange
    - Can also be used to exchange one type of cryptocurrency for another
    - Many will operate outside of Western countries to avoid regulatory oversight
    - Examples: Coinbase, Coinmama, Kraken, Netcoins, or Cashapp
- **Bitcoin ATM**: like a traditional ATM but exchanges Bitcoin and cash
    - AKA cryptocurrency kiosks
    - Most perform transfers via QRcodes to/from paper/mobile wallet
    - Some can transfer to/from physical cards and cash
    - Typically have high transaction fees and varying levels of identity information collection
- **Peer-to-peer Cryptocurrency Exchange**: when users trade directly with one another without a third-party
- **BitRank Verified**: a free online tool that scans the blockchain to assess the risk level associated with a certain Bitcoin wallet in the hopes of identifying fraudulent vendors
    - Resource can be found [here](https://bitrankverified.com/home)

## Crypto and Crime
- **Peer to Peer (P2P) Exchange**: typically an online site that connects people with crypto who want fiat currency with people who have fiat and want crypto in order to exchange currency anonymously and without any regulations
    - You can also have a Peer to Peer exchanger who will meet in person to exchange all goods
    - There are several reasons users engage in a P2P exchange:
        1. Desire to buy Bitcoin using different types/anonymous forms of payment
        2. Need a larger amount of Bitcoin very quickly
        3. Avoid "daily limits" set by licensed exchangers
        4. Distrust bank type institutions
        5. Lack a bank account to link to a legitimate exchange
        6. Anonymity: the cost of P2P exchange typically is significantly higher than AML-compliant exchanges as users pay for the anonymity afforded by a P2P exchanger
    - Example P2P sites include PAXFUL and Localbitcoins
- **Tumblers/Mixers**: a process where crypto is sent in order to be obfuscated through many small transactions outputting "cleaned" crypto not traceable to the illegal trades
    - **Coinjoins**: usually illicit cryptocurrency services that exist solely to launder crypto coins to obfuscate the trail
- **Child Exploitation**: the use of a child in any way for economic gain
- **Sexual Exploitation**: the act of employing, using, persuading, inducing, enticing, or coercing a person to engage in sexually explicit conduct
    - Also includes the transportation of a person from one state to another or to a foreign territory, with the intent of engaging the person in sexually explicit conduct
- **Funnel Accounts**: accounts held by a person (nominee) at a financial institution and collects funds from many sources (smugglers), funneling them all into the one account. Funds are bundled with other funnel account holders, removed quickly, and smuggled out of the country/laundered though other means
    - Often used in human trafficking and smuggling operations
- **Exit Schemes**: form of fraud where belief in the success of a nonexistent enterprise is fostered by the payment of quick returns to the first investors from money invested by later investors
    - Similar to a Ponzi scheme and common in ICOs offered with startup businesses

### Laws and Legislation
- **United States Bank Secrecy Act (BSA) regulation 18USC1960**: regulation that requires persons or companies trading in or exchanging cryptocurrency to register as a Money Service Business (MSB)
    - The key element in this registration is that it requires individuals/businesses to comply with Know Your Customer (KYC) standards which enforces gathering identity information
    - When in violation of this regulation, you are acting as an Unlicensed Money Service Business (UMSB)
    - In order for Peer to Peer exchangers to be compliant, they must adhere to all requirements of the BSA and Patriot Act including:
        1. Register with FinCEN as a MSB
        2. Have an AML compliance program
        3. Implement and maintain a KYC program
        4. File applicable reports such as CTRs and SARs

### Investigations
- **De-anonymization**: a data mining strategy used to identify a previously anonymous source by cross-referencing with other sources of data
- **Dual Control**: when at least two authorized officials (typically law enforcement officers) are present when handling evidence in order to preserve the chain of custody
- Key pieces of information needed to be gathered during an investigation:
    1. Blockchain or digital assets being used
    2. Hash/ID of transaction(s)
    3. Transaction inputs/outputs
    4. Quantity of crypto transferred
    5. Associated fees
    6. Any change addresses generated from the transaction
    7. Fiat currency conversion rate at the time of all transfers

## The Dark Web
- **Darknet**: the network that the dark web runs on top of
- **Darkweb**: the website hosting platform within the darknet
- **Freenet**: an anonymous peer-to-peer platform designed to prevent censorship
    - in exchange for the free service, users contribute a portion of their hard-drive to the network with no say on what is stored there
- **Invisible Internet Project (I2P)**: a network within a network called an anonymous overlay network
    - An offshoot of Freenet
    - **Eepsites**: I2P specific sites (like hidden services are to TOR)
    - **Garlic Routing**: a variant of onion routing, where multiple messages are taken and encrypted together in a "clove" to avoid traffic analysis
    - I2P Vulnerabilities:
        - **Sybil Attacks**: when attackers create multiple identities to have a disproportional influence on the how the network operates
        - **Harvesting**: compiling a list of I2P nodes, which is easy to do as each node is constantly searching for other nodes to connect to
- **The Amnesic Incognito Live system (TAILS)**: an operating system that can be used to access the dark web and browse the internet anonymously
    - Main purpose is to circumvent censorship and provide an anonymous internet browsing experience
- **Proxy Server**: a gateway between your local network and a large-scale network (like the internet)
    - These servers intercept connections between the receiver and sender making it difficult for attackers to access the information on a private network
- **Network Address Translation (NAT)**: devices that change the IP address of traffic before it passes to the internet, acting as a "bouncer" or "receptionist"
- There are several types of dark web markets:
    - **Centralized Marketplace**: operate with a centralized server with individual stores all hosted on the same server (like Amazon or eBay)
        - A fee is charged for each transaction and may change based on the individual stores on their site
    - **Decentralized Marketplace**: operate on a more peer-to-peer level (like Craigslist) where the site acts as a meeting place but does not typically charge for transactions/listings
    - **Country Specific Markets**: often in response to sanctions, allow countries to access resources, sell products, and circumvent restrictions without folding to political pressure
- **Encrypted/Secure Messaging**: uses encryption to keep messages between you and the intended recipient. Popular messaging sites include:
    - Telegram
    - Signal
    - WhatsApp (very popular in China)
    - Encrypted Communication Methods include:
        - **i2p-Bote**: an asynchronous email client operating on the I2P network
            - Delayed communication adding anonymity
            - Deletes messages after 100 days
        - **Retoshare**: creates direct connection only with those you wish to communicate to 
        - **Bitmessage** peer-to-peer communication application with strong encryption, able to scramble encrypted messages of users
        - **Protonmail**: an email service built around privacy and encryption that can be run from smart devices and desktops
        - **Signal**: an open source and free messaging system that uses end-to-end encryption
- **Pretty Good Privacy (PGP)**: encryption program used to encrypt/decrypt information (such as text messages, instant messages, emails, data sets, files, and even hard drives)
    - Does not hide a users identity, only the content of what is being shared

## Sources
- [Blockchain Intelligence Group](https://blockchaingroup.io/)
- [Blockchain Intelligence Group's Certified Cryptocurrency Investigator Course](https://cryptoinvestigatortraining.com/?)
- [Anti-Human Trafficking Intelligence Initiative's (ATII) Darkwebathon Event](https://followmoneyfightslavery.org/darkwebathon/)
- [FinCEN Guidance for Handling Virtual Currencies](https://d3pg1c2bhy6429.cloudfront.net/114038/d6XFAAb0g2T9ZYUmNwzELA_lbS8eHobKLKBOXqiz/scormcontent/assets/9F8zwP3gx6z43KTW_LPm2AVcpIYqICWcI-application-of-fin-cens-regulations-to-persons-administering-exchanging-or-using-virtual-currencies.pdf)
- [International Cryptocurrency Regulations](https://www.perkinscoie.com/en/news-insights/digital-currencies-international-actions-and-regulations-2023.html)