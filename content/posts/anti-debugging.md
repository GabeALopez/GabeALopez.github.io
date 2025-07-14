---
date: 2025-07-13
# description: ""
# image: ""
lastmod: 2025-07-13
showTableOfContents: false
tags: ["Cybersecurity", "Malware"]
title: "Anti Debugging"
type: "post"
---

> What is Anti-Debugging?
>
> Debugging malware code enables a malware analyst to run the malware step by step, introduce changes to memory space, variable values, configurations and more. Therefore, if debugging is done successfully, it facilitates the understanding of the malware’s behavior, mechanisms and capabilities. For obvious reasons, this is something malware authors would want to prevent. Anti-Debugging techniques are meant to ensure that a program is not running under a debugger, and in the case that it is, to change its behavior correspondingly. In most cases, the Anti-Debugging process will slow down the process of reverse engineering, but will not prevent it.
> 
> Author: Dalya Guttman
>
> Date: December 27, 2017
>
> [Common Anti-Debugging Techniques in the Malware Landscape](https://www.deepinstinct.com/blog/common-anti-debugging-techniques-in-the-malware-landscape)

Anti-debugging is interesting topic to me with malware. 

I have know some very simple anti-debugging techniques like looking at the PEB structure that was mentioned in the article but there are some other ones that interesting in the article too.

Although this article is old I still think it introduces some pretty interesting concepts nevertheless

But, like I wrote here, checking the PEB structure is one of the easiest ways to detect if you are being debugged

There is a literal flag you can just check in the Visual Studio to see if you are being debugged called ```BeingDebugged```

But this can be easily bypassed by doing some binary patching but anything to slow the reverser.

However this may not be as easy as that depending if the malware scans for patching, which gets into the technique that caught my eye. 

That technique here was the ability for malware to identify breakpoints and patching through checksums.

According to the article, malware can "calculate a checksum or hash of its code in run time to determine if it was patched or if a breakpoint was inserted", which is a really neat idea.

And, according to the article, malware can also do instruction scanning looking for the assembly the debuggers use to, well, debug. 

Overall, some neat techniques that are interesting here.

## Extra Reads

[Anti-Debugging Techniques](https://medium.com/@X3non_C0der/anti-debugging-techniques-eda1868e0503)

Medium article found when doing some research for this topic.

There are some additional techniques mentioned here using timing.

[Anti-disassembly, anti-debugging and anti-VM](https://www.infosecinstitute.com/resources/malware-analysis/anti-disassembly-anti-debugging-and-anti-vm/)

Now this one some other anti-debugging techniques including API obfuscation and opcode/assembly code obfuscation.

But is also showing some sandbox evasion techniques as well, which I will eventually write a post about.