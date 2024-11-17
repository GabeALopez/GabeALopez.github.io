---
date: 2024-11-11
title: "Red Team Tools"
tags: ["Cybersecurity", "Red Team"]
type: "post"
---

**Hi there, here is a list of red team tools I have used in CTFs:**

## Directory Bruteforcing

- Feroxbuster - Recursive bruteforcing
- FUFF - Very flexible fuzzing tool

## Web Proxies

- Burpsuite - Most popular web proxy
- OWASP ZAP - Opensource alternative to Burpsuite
- Inspect Element - The ghetto web proxy

## Website Finger-Printing Tools

- Whatweb - A command line tool to help identify the backend and frontend of a website
- Wappalyzer - Works similarly to Whatweb but is a browser extension instead

## SQL Injection

- SQLmap - A nice tool to help automate discovering and exploiting SQL injections

## Cryptography

- CyberChef - Website based tool to help analyze and decrypt any encrypted text

## SMB Tools

- Crackmapexec - Post exploitation tool when you have found credentials on an SMB server
  - Also a very helpful enumeration tool
- SMB Client - A local linux tool to use SMB shares
- Enum4linux - Automation tool to enumeration tool
  - **NOTE:** In actual pentests it is advised to not really use this tool as it creates too much noise for the client

## Active Directory

- Blood Hound - A nice enumeration tool when you have an initial shell on a windows machine
  - This tools helps to produce a json file to import into the Blood Hound website so you can find a connection from your current user account to a domain admin
