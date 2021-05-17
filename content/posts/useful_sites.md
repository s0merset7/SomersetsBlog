---
title: "Useful Websites"
description: ""
date: 2021-05-16T18:44:00-07:00
lastmod: 2021-05-16T18:44:00-07:00
cover: ""
coverAlt: ""
toc: false
tags: []
draft: false
---
<style>
	main {
    margin: 90px auto;
    padding: 0 15px;
    max-width: 70%;
	}
</style>

There are hundreds of websites out there with useful information and helpful tools that can be used while hacking, so I decided to create a list of helpful websites for different aspects of hacking as I come along them. I will make sure to update this list as I come across more, so make sure to check back regularly!

## Information Gathering
### DNS Reconnaissance
* [**DNSDumpster**](https://dnsdumpster.com/): will provide a visual breakdown of where/what a domain's servers/hosts are located, as well as maps the domain in relation to its hosts/servers
* [**Hunter**](https://hunter.io/): insert a domain and it will return known email addresses connected to the website (you do have to make an account but it is free)
* [**ViewDNS**](https://viewdns.info/): site that allows you to run a variety of tests against domains, IPs, and email addresses such as Whois, IP History, Location Finder, and more
* [**Whoxy**](https://www.whoxy.com/): performs Whois and Reverse Whois lookups, as well as searches for owners, emails, and more (search tool is at the top right of the website, you can ignore the paid options advertised)

### Active Reconnaissance
* [**Exploit Database**](https://www.exploit-db.com/): hopefully you know this one already, but use this to find common vulnerability exploits (CVE) and how to replicate them

## Website Pentesting
* [**HTTP Status Codes**](https://httpstatuses.com/): a simple site that lists all possible HTTP status codes along with what they mean and some specific information you can interpret from them

## Decrypting/Password Attacks
* [**CyberChef**](https://gchq.github.io/CyberChef/): a GitHub project that allows you to use encryption/decryption tools against any given text
* [**Weak Passwords**](http://weakpasswords.net/): website that gives you the current top 50 most common passwords in use

## Privilege Escalation
* [Super helpful blog post](https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/) that walks you through how to do enumeration on a new host with the intention of privilege escalation
* [**Reverse Shell Cheat Sheet**](https://highon.coffee/blog/reverse-shell-cheat-sheet/): cheat sheet that provides the code for how to deploy a reverse shell and the process in different languages

## Reporting
* [**Carbon**](https://carbon.now.sh): nice site that allows you to paste your code and edit it to make it look more readable for reports 