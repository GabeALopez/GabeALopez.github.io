---
date: 2025-06-23
title: "Resources"
description: "This is a collection resources I have for varying things in cybersecurity"
tags: ["Cybersecurity", "resources"]
type: "post"
showTableOfContents: true
---

# Red Team

## Pentesting

[Hacktricks](https://book.hacktricks.wiki/en/index.html)

**Description:** A nice collection of methodologies for pentesting all kinds of things

[VAPI](https://github.com/roottusk/vapi)

**Description:** A repo that has a broken application for API testing from the OWASP Top 10. May be outdated though.

[Google Dorks Github](https://github.com/TakSec/google-dorks-bug-bounty)

**Description:** A list of google dorks to use for recon in bug bounty

[Bug Bounty Tools List](https://github.com/vavkamil/awesome-bugbounty-tools)

**Description:** List of tools that can be used for varying things in bug bounty

[IppSec's Website](https://ippsec.rocks/?#)

**Description:** This is IppSec's website that you can use to triage through his videos. If you have a keyword to look into, let's say how to use netexec, it will triage the descriptions of his videos to find what you are looking for.

[IppSec's Youtube Channel](https://www.youtube.com/channel/UCa6eh7gCkpPo5XXUDfygQQA)

**Description:** This is IppSec's Youtube channel where he does a lot HTB machines. Pretty nice resource for these boxes.

[Malware Dev Academy](https://maldevacademy.com/)

**Description:** This is an interesting site for learning malware. Now I'm not saying to buy this. No, what I am saying to look at the syllabus that is posted on the site and start looking into the different techniques mentioned. A wealth of ideas

[Offensive Nim](https://github.com/byt3bl33d3r/OffensiveNim?tab=readme-ov-file#why-nim)

**Description:** Now this is an interesting repo for weaponizing a new coding language to create malware with

## Malware Development

### **General**

```
"malware dropper"
"malware loader"
"initial access techniques"
```
**Description:** Google searches that can be used to find info about malware droppers

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

[Black Hat Zig](https://black-hat-zig.cx330.tw/#intro)

**Description:** Interesting project regarding making malware with zig 

[r/Malware](https://www.reddit.com/r/Malware/)

**Description:** Reddit to follow what people are saying about malware.

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

### Tools

- General Reversing
  - Ghidra
  - Cutter RE
  - Radare
  - IDA Free
- Mobile
  - Jadix

## Forensics

[Digital Forensics Lab](https://github.com/frankwxu/digital-forensics-lab)

**Description:** This is a old lab to learn digital forensics but I think it is still useful

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

[Job Search Terms Github](https://github.com/harisqazi1/Cybersecurity)

**Description:** This isn't a place that has job posting but it is a repo to look out for certain keywords in your searches

[Job Search Repo - "security-jobs"](https://github.com/sakshisangamwar/security-jobs)

**Description:** This is a repo where two contributors put down job postings they have found in relation to internships and general security jobs

[Job Search Repo - "2025-CyberSecurity-Internships"](https://github.com/WiCySRice/2025-CyberSecurity-Internships)

**Description:** Another repo where people post jobs. Hasn't been updates in a bit but the idea of finding these repos is there

[Job Search Repo - "New-Grad-2025"](https://github.com/vanshb03/New-Grad-2025)

**Description:** This is another repo where jobs are posted but this one gets updated more often

[Job Search Repo - "New-Grad-Positions"](New-Grad-Positions)

**Description:** Yet another repo that gets job postings. This one gets updates fairly quickly as well

