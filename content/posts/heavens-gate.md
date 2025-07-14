---
date: 2025-07-12
# description: ""
# image: ""
lastmod: 2025-07-13
showTableOfContents: false
tags: ["Cybersecurity", "Malware"]
title: "Heavens Gate Technique"
type: "post"
---

> When Microsoft introduced 64-bit Windows, backward compatibility for 32-bit applications remained essential. This compatibility layer, called WOW64 (Windows-On-Windows 64-bit), allowed older software to function seamlessly. Underneath this compatibility abstraction, however, an opportunity emerged for attackers.
>
> Security solutions frequently focused their defenses around 32-bit behaviors, neglecting less commonly exploited 64-bit operations. Heaven’s Gate was born from this oversight, enabling threat actors to break free from WOW64’s restrictions and execute unmonitored 64-bit code.
>
> Named metaphorically after the idea of “ascending” from a restricted environment to a broader, more privileged space, Heaven’s Gate cleverly manipulates processor architecture to achieve stealth.
>
> Author: Rinzl3r
>
> Date: April 29, 2025
>
> [Heaven’s Gate: How Attackers Exploit Architecture to Evade Detection](https://itinnovationstation.com/2025/04/29/heavens-gate-how-attackers-exploit-architecture-to-evade-detection/)

I ended up finding out this interesting mechanic in windows for backwards compatibility and how it can be used in defense evasion.

The usage of "Heaven's Gate" as a defense evasion technique is actually quite interesting as one can masquerade their malware

Imagine making their seemingly 32 bit app, that cannot use modern syscalls, to all of a sudden use 64 bit syscalls

The article here also gives some hardening and threat hunting techniques as well to look for this type of activity:


> ***Threat Hunting Techniques:***
>
>   Examine WOW64 processes for unusual syscalls.
>
>   Analyze memory sections for mixed-mode instructions.
>
>   Flag processes making 64-bit syscalls without first exiting the WOW64 environment.
> 
> Custom YARA rules targeting unusual syscall gates inside user-mode processes can help uncover hidden threats utilizing this approach.
>
> ***Hardening Approaches:***
>
> Enforce strict application whitelisting.
>
> Disable WOW64 subsystem where feasible on servers or highly controlled endpoints.
>
> Apply Kernel-mode code integrity (KMCI) protections.
>
> Use virtualization-based security (VBS) features like Credential Guard or Hypervisor-enforced Code Integrity (HVCI).

Overall, a very interesting technique and would be interested in implementation in more modern coding languages like zig or go

---

### **Some other reads I found when looking at this technique:**

[Github implementation I found](https://github.com/B4shCr00k/He4vensG4te)

[An explanation of Heaven's Gate for a crackme](https://0xk4n3ki.github.io/posts/Heavens-Gate-Technique/)

[Interesting look of Heaven's Gate on Linux](https://redcanary.com/blog/threat-detection/heavens-gate-technique-on-linux/)

[Article explaining how Heaven's Gate is still being abused to this day, although over 5 years old](https://www.zdnet.com/article/malware-authors-are-still-abusing-the-heavens-gate-technique/)