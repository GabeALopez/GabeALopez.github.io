---
date: 2024-11-17
# description: "Nothing to see here"
#image: "/regPando.jpg"
lastmod: 2024-11-17
showTableOfContents: false
tags: ["Cybersecurity", "History"]
title: "The Eternalblue Story"
type: "post"
---

### Introduction

The story of the eternalblue vulnerability is quite an interesting one as it comes back to the ever-recurring issue of government spying and whether or not the ends justify the means when it comes to government spying for the sake of protection.

### Background Info

Before getting into the events of what happened surrounding the discovery of the eternalblue vulnerability it is important to know what this vulnerability is in the first place. Eternalblue was a vulnerability in the file-sharing service SMB in various Windows operating systems. These operating systems included Windows Vista all the way to Windows Server 2016. This was done by using corroded packets sent to the service which allowed for remote code execution. According to NIST, this was designated with a CVS score of 8.8[^1]. To put this score into perspective usually anything ranging from a 6-1 is considered minor, 7 is somewhat a concern, and 8-10 is a major problem.

Now that is just the score. To put the impact of the vulnerability into perspective of how many devices were affected in the image below from Help Net Security shows the number of IP addresses that were affected by the vulnerability[^2]:

![Number of IP addresses affected](/cybersecurityPhotos/eternalBlue/ipPic.png)

Out of the 8.03m devices, 60k were vulnerable around the world which is a large number that is hard to comprehend. But wait there is more. In the USA alone 1,572 devices were affected by the vulnerability which considering other countries, the USA got off easy as seen in the following graphic from the same Help Net Security:

![US Devices](/cybersecurityPhotos/eternalBlue/usDevices.png)

So overall, we can see that this vulnerability allowed for remote code execution. This means that any person could just get access to a device with an exploit for the vulnerability from any location as long as they could hit the service.

So in summary the eternalblue vulnerability has affected many of the world's machines.

If you are interested in the nitty-gritty details of how this vulnerability really works then go through the details section below. If not go [here](#the-wild-events-leading-up-events-leading-up). The link will move you to events leading up to the discovery of the vulnerability, which is the main meat and potatoes of all of this.

### Details

Most of this explanation comes from a sentinel one page [here](https://www.sentinelone.com/blog/eternalblue-nsa-developed-exploit-just-wont-die/). So if you want to go the source there you go.

The enternalblue vulnerability takes advantage of three vulnerabilities in the programming of the SMB protocol. Furthermore, the vulnerability lies within the ```srv!SrvOS2FeaListSizeToNt``` Windows function. The first vulnerability is in a math error when casting a ```OS/2 FileExtended Attribute (FEA)``` list structure to a ```NT FEA``` structure which results in an integer overflow in the amount of memory that is allocated. The amount of memory that is allocated is small but enough not to cause the program to error. Because of less memory allocation, one can use it to perform a buffer overflow. Now this overflow would not be enough to get remote code execution (RCE) if it wasn't for the second vulnerability.

The second vulnerability lies within the ```SMB_COM_TRANSACTION2``` and ```SMB_COM_NT_TRANSACT```sub-commands, where both have a secondary function in case a packet has too much data. The important thing about these two subcommands is that ```TRANSACTION2``` has calls for a packet size that is smaller than when using ```NT_TRANSACT```. This is important as the smaller the packet size the easier it is to exploit the buffer overflow. Furthermore, there is error validation when using ```NT_TRANSACT``` before ```TRANSACTION2``` when sending a crafted message. The other interesting thing here too is that the program assigns the type and size of both packets based on the type of the last packet it has received.

But we are not done yet. We still need to get the RCE from the program and this can be done by using the third vulnerability. The third vulnerability allows for one to allocate a portion of memory at a given address, which could be at an address of a shell library embedded into the program, called heap spraying.


### The Wild Events Leading Up {#events-leading-up}

So our story starts on Friday, April 15th, 2017 when a group known as "Shadow Brokers" released a large set of tools that were supposed to be NSA tools[^3]. These tools included many exploits that ranged from Windows devices, network devices, and Unix vulnerabilities[^4]. That being said, this toolset had significant impacts when released at the time. When this toolset was released troves of attackers flocked to exploit as many devices as possible[^5]. This even led to a famous ransomware outbreak known as the WannaCry ransomware which was supported by, you guessed it, the eternalblue vulnerability. The WannaCry virus was, again, a ransomware that affected many devices and had large impacts on the infrastructure of many organizations around the world.

Now Kaspersky had found that this Equation Group was a highly sophisticated hacking group as they were linked to the Stuxnet and Flame espionage malware[^6]. Going through an exhaustive search Kaspersky went on to say that these attacks were caused by the NSA themselves. If this is truly the case, then this shows that the NSA was stockpiling exploits. Surprisingly, Microsoft had seemingly agreed with this train of thought from Kaspersky and posted on their site explaining why stockpiling these types of vulnerabilities can lead to big issues for end users [^7].

Overall, there is some interesting evidence showing that government agencies, like the NSA, stockpile vulnerabilities. This brings into question the number of other tools that may still exist but are more well-hidden from the public. These events, and the subsequent tool set, surrounding the eternalblue vulnerability were found in 2017. Who's to say that other toolsets in the current time haven't already been created and are being actively used against whomever?

[^1]: https://nvd.nist.gov/vuln/detail/CVE-2017-0144
[^2]: https://www.helpnetsecurity.com/2017/07/12/eternalblue-vulnerability-scanner-statistics/
[^3]: https://www.rapid7.com/blog/post/2017/04/18/the-shadow-brokers-leaked-exploits-faq/
[^4]: https://www.nopsec.com/blog/the-shadow-brokers-leaked-equation-groups-hacking-tools-a-lab-demo-analysis/
[^5]: https://www.security.com/threat-intelligence/buckeye-windows-zero-day-exploit
[^6]: https://arstechnica.com/information-technology/2015/02/how-omnipotent-hackers-tied-to-the-nsa-hid-for-14-years-and-were-found-at-last/
[^7]: https://blogs.microsoft.com/on-the-issues/2017/05/14/need-urgent-collective-action-keep-people-safe-online-lessons-last-weeks-cyberattack/#sm.0000mpb068eggcqczh61fx32wtiui
