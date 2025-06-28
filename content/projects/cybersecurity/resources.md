---
date: 2025-06-23
title: "Resources"
description: "This is a collection resources I have for varying things in cybersecurity"
tags: ["Cybersecurity", "resources"]
type: "post"
---

# Red Team

## Pentesting

## Malware Development

### **General**

[Evading Antivirus Detection in C (with Dahvid Schloss) - John Hammond](https://youtu.be/izf8ptPVh2g?si=w5uVqyza3E678Csp)

**Description:** An interesting talk John Hammond had with Dahvid Schloss for his insight on Malware development

[Youtube - Crow](https://www.youtube.com/@crr0ww)

**Description:** A good channel I found to learn about some good hands-on info about creating malware

[0xPat Blog](https://0xpat.github.io/Malware_development_part_1/)

**Description:** A good blog I found about creating malware and some techniques to avoid detection

[thecyberidiots - Dahvid Schloss Company's blog - "Fun with PowerShell – Executing commands with DNS requests"](https://www.thecyberidiots.com/post/fun-with-powershell-executing-commands-with-dns-requests)

**Description:** This is an old blog, talking 2022, but still interesting talking about using DNS queries through PowerShell to send data to a C2 server

[LOTS - Living Off Trusted Sites Project](https://lots-project.com/)

**Description:** A list of trusted sites that malware may abuse to keep persistence and stay hidden

[Hijacklibs Project](https://hijacklibs.net/)

**Description:** A list of DLLs that can be used to hijack more privileged programs in your environment to gain priv escalation

[LOLBAS - Living Off The Land Binaries, Scripts and Libraries Project](https://lolbas-project.github.io/#)

**Description:** A list of trusted binaries that normally exist in a windows or linux environments that can be abused to stay stealthy. My favorite project :\)

[Win32 API Documentation](https://learn.microsoft.com/en-us/windows/win32/api/)

**Description:** The good old documentation on how to use the Win32 API (Application Programming Interface). Want to make malware? Know how to read this and know what info you want from it. 

### Topics to Think About

- DNS Queries
    - Using DNS queries to send data to C2
    - Bypassing typical traffic hall monitors
- Process injection 
    - Crow explains this in his videos
- DLL hijacking
- Living off The Land Binaries, Scripts, and Libraries
- Avoiding Analysis and sandboxes
    - As a malware dev you want to avoid someone analyzing your code. Can't make it too easy!
    - Techniques
        - Seeing if the mouse is moving 
        - Nesting code
        - Sleeping
            - Not with just sleep commands but with other things like counting prime numbers
        - Check resources
            - RAM
            - Disk space
            - CPU
- Persistence methods
- Research 
    - Remember there are other bad doing the same thing you are. Learn from them! *cough* For good of course

## Binary Exploitation


### Tools

- pwn-dbg - [Documentation](https://pwndbg.re/pwndbg/latest/features/)

### Topics to Think About

- Types of vulns
    - Buffer overflow
    - Stack overflow
    - Integer overflow
    - Format string
- Return Oriented Programming (ROP)
- Protections
    - RELRO
    - NX
    - Stack Canary
    - ASLR
- Automation 
    - You hate boring stuff right? Make it do everything for you!

# Blue Team

## Reversing

**Rule of Thumb:** Does the code look wonky decompiled? Try a decompiler that is specific to that coding language. You'll probably get better results

## Forensics

### Tools

- FTK imager
    - Memory dumps! Get your memory dumps!
- Volatility 
    - Rummage through mem dumps with this

# Automation

[Automate the Boring Stuff with Python](https://automatetheboringstuff.com/#toc)

**Description:** The good to for learning how to automate digital workflows for beginners. It teaches the important stuff of python to get you started.
