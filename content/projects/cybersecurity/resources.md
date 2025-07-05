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

### General

[CryptoCat - Intro to Binary Exploitation](https://youtu.be/wa3sMSdLyHw?si=976kuK3W4SygRRWR)

**Description:** This is a series by CryptoCat that will teach you how to do binary exploitation challenges. Pretty useful

[Cybersecurity Notes - ir0nstone](https://ir0nstone.gitbook.io/notes/binexp/stack)

**Description:** This is a set of notes I pulled from the Binary Exploitation series that CryptoCat had linked. It's got some good notes regarding binary exploitation. It has other notes but it seems that binary exploitation is the main focus here. 

[Format Strings 101 - Alexandre CHERON](https://axcheron.github.io/exploit-101-format-strings/)

**Description:** This is another article I pulled from the CryptoCat's sources in his Binary Exploitation series. Is a little somewhat confusing so I would look through the binary exploitation video in the series for overwriting the global offset table

[GOT and PLT for pwning - System Overload](https://systemoverlord.com/2017/03/19/got-and-plt-for-pwning.html)

**Description:** Explains the global offset table for pwn challenges.

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

**Rule of Thumb:** Does the code look wonky decompiled initially? Try a decompiler that is specific to that coding language. You'll probably get better results

## Forensics

### Tools

- FTK imager
    - Memory dumps! Get your memory dumps!
- Volatility 
    - Rummage through mem dumps with this

# Automation

[Automate the Boring Stuff with Python](https://automatetheboringstuff.com/#toc)

**Description:** The good to for learning how to automate digital workflows for beginners. It teaches the important stuff of python to get you started.

# Job Finding

## Job Strategy

Before getting into the job hunting strategies below, I want to share a quick perspective that helped me stay grounded during the process.

According to statistics, it usually takes around 100 job applications to land a position. That roughly equals about three months of consistent searching and applying, depending on your background and the job market.

The key thing to remember is this: if you keep applying, eventually an opportunity will come. One of humanity's oldest and most powerful traits is perseverance. Going back to ancient times, humans were able to hunt not because we were the strongest, but because we kept going until our prey gave up and and succumbed to our sticks and stones. That persistence helped us survive.

In a similar way, job hunting works the same. The cycle of applying for jobs will be so worn out from you applying that it just gives up and gives you something. It's just that annoyed. It may sound strange, but it is something worth thinking about.

**BIG DISCLAIMER:** None of this info is a guarantee for a position and I recognize some of it may seem a hokey but take what I have written what you will.

Below is the formatted notes. If you are interested in the raw unorganized notes here you go:

[Raw Job Notes]({{< relref "./raw-cybersecurity-markdown-notes/raw-job-notes.md" >}})

### Job Description Evaluation
--------------------------

When to Apply:
- Apply if job is labeled:
  - “Entry-Level”
  - “Associate”
  - “New Grad”
  - Mentions 5 or fewer years of experience
- Don’t apply for now if:
  - No experience level is listed
  - No years of experience are mentioned
    (May change later as you get better at interpreting job requirements)

Company Size Consideration:
- Big Companies often have new grad roles → Apply
- Small-Medium Companies may not label as such →
  Apply anyway if you can show ability to learn fast

Job Description Red Flags:
- Too much is asked?
  → Could be a recruiter being unrealistic or a company asking too much
- Look for keywords indicating level:
  - entry-level
  - new grad
  - associate
- Look for keywords indicating type of role:
  - information technology analyst
  - cybersecurity analyst
  - information security analyst
  - security analyst

Contract Roles:
- Usually want someone who can start immediately
- Often looking for mid-level laid-off professionals
- May not be suitable for entry-level, but use judgment


### Application Timing
------------------

- Apply early in the morning or late at night
- Apply Friday evening – large influx of applications
- Apply early in general, even if it says “< 50 applicants”
- Look for postings that have been posted in the last week and if they meet criteria apply for it.


### Reposted Jobs
-------------

- Apply if reposted by large companies (e.g. ReliaQuest, Lockheed, L3Harris, Deloitte)
  - Rule of thumb: if the company has about 10000 or more employees and in tech or MSP, it’s worth it
- Don’t apply if reposted by medium or small companies


### Security Clearance
------------------

- Look for roles that sponsor clearance
- If role requires active clearance, consider applying based on description fit


### Ghost Jobs
----------

- Pay attention to frequent reposting
- Consider the type of company:
  - MSP (Managed Service Provider)? → Always hiring → Still apply
  - Manufacturing or similar? → Likely ghost job → Avoid


### Internships
-----------

- Apply to all internships regardless of company size


### Job Boards & Resources
----------------------

- newgrad-job.com
- New-Grad-Positions GitHub


### Application Strategy
--------------------

- If you meet ⅔ of the combined qualifications (minimum, preferred, and job duties) → Apply
  - Focus most on minimum qualifications
  - Even if you're 50/50, still try
- If something strongly matches your interests → Tailor your resume
  - Identify common themes
  - Create a general resume
  - Maintain flexibility:
    Have a general resume ready, customize when necessary


## Job Posting Locations