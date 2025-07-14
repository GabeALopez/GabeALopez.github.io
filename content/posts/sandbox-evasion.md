---
date: 2025-07-14
# description: ""
# image: ""
lastmod: 2025-07-14
showTableOfContents: false
tags: ["Cybersecurity", "Malware"]
title: "Sandbox Evasion"
type: "post"
---

> Sandboxing is a proven way to detect malware and prevent its execution. However, malicious actors search for ways to teach their malware to stay inactive in the sandbox. Sandbox-evading malware can bypass protections and execute malicious code without being detected by modern cybersecurity solutions. 
>
> In this article, we analyze techniques used by malware to avoid sandbox analysis and share best practices we use at Apriorit to build sandboxes that can detect and stop evading malware. 
> 
> This article will be useful for developers who are working on cybersecurity solutions and want to improve their sandboxes.
>
> Authors: Alina Beliba & Anna Katrenko
> 
> Date: August 8, 2023
> 
> [Catching Sandbox-Evading Malware: Techniques, Principles & Solutions](https://www.apriorit.com/dev-blog/545-sandbox-evading-malware)

This is an interesting article that I had found when I researching a bit more into sandbox evasion techniques. 

This topic of malware development is also a favorite of mine as everyone uses sandboxes when they don't feel like using static analysis.

There are various ways that malware can detect if they are in a sandbox, or even sometime they don't even really check to begin with.

But one of the main ways and also what the article mentions is doing system checks.

The checks range from checking how much ram is allocated to the machine to what is the MAC address of the machine that the malware is on

One might be asking: why check something like RAM?

Well a lot of time sandboxes are only give a little bit of RAM to do a quick check and malware can check that amount of RAM

Malware can just not run if there is too little RAM, which is quite interesting technique

---

Another cool technique group is through user activity like the article mentions

One way of doing this is determining if the mouse is being moved around and clicking on things

Many sandboxes do not move and click a mouse around within them and so malware can detect this

--- 

Another interesting technique group is timing.

Some malware will just try to outlive the sandbox as some sandboxes are only on for a certain amount of time before it makes a decision

This makes sense from an organization perspective, when there are multiple files and emails being sent everywhere

I have even heard of some sandboxes look for code that indicates that the malware is using sleep

One evasion from this that I have heard is calculating prime numbers

Calculating to a certain prime number can take an X amount of time

Because of this, no sleep is used and thus sandboxes are unable to detect the usage of sleep functions

I would like to show these evasion techniques in code the future to give a more technical explanation of this

Overall, sandbox evasion is one of my favorite defense evasion techniques due to the creativity that can be done with manipulating the OS.

### Additional Reads

[Malware Sandbox Evasion Techniques: All You Need to Know](https://www.vmray.com/sandbox-evasion-techniques/#elementor-toc__heading-anchor-3)

[Anti-VM and Anti-Sandbox Explained](https://www.cyberbit.com/endpoint-security/anti-vm-and-anti-sandbox-explained/)