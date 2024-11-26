---
date: 2024-11-18
# description: ""
# image: ""
lastmod: 2024-11-18
showTableOfContents: false
tags: ["Cybersecurity", "History"]
title: "The Birth of Computer Viruses: Origins and Evolution"
type: "post"
---

## Self-Replicating Automata

Now the idea of having a program replicate itself was, actually, not new. The first real theory of a self-replicating program starts in the 1940s with a mathematician named John von Neumann. His designs called for a universal separator, which builds the machine from a copier which replicated a machine's description. The separation he called for allowed for mutations, enabling the new automata to evolve much like real organisms[^2]. Furthermore, his research looked into two ways of which the automata spread. The first was that information was interpreted as instructions to build a copy and the second was where information was just copied into a separate instance.

## The World's First Computer Virus

The world's first well known computer virus was called Creeper and it was developed by a BBN programmer, Bob Thomas[^1]. Thomas initially created this virus as an experiment to test the idea of a self-replicating program, or worm. When Thomas had released it for testing he did not realize the extent to which his program would spread and found out quickly as his virus had quickly corrupted the DEC PDP-10 mainframe. After being corrupted these computers would go on to display a message saying "I'm the creeper, catch me if you can!". Now is not really considered a malicious virus as the virus did not destroy or steal data and it only displayed a simple message.

Now how this virus worked was interesting by itself. The virus had caused the computer it was one to print a file, stop abruptly, find another Tenex computer, open a connection, then downloaded and transfer itself, and then start back up on the new system. The other interesting thing about this is that it did not really replicate itself. It almost shuffled from system to system displaying its message, thus not creating multiple instances of itself in the process[^1].

From the beginning of world seeing the effects of Creeper, it prompted research into preventing such programs for the future. As a result, the first anti-virus was created, known as Reaper, which was furthermore created to stop the Creeper virus[^1]. Little did the world know that this simple computer virus and anti-virus would be the start of the everlasting fight between malware developer and malware analyst.

## Malware as an Art

As the years went on people started to create malware as an art form funnily enough around the 90's-2000's. At this time, people had created viruses as more something to just annoy someone rather than finding, exfiltrating, and selling sensitive data. But the art that came from it was quite interesting. Many of the malware at this time had ever changing colors or would have basic pixel images that would stay up on the screen until you formatted the device. 

Here is an example of the FLAME.COM virus which just had the command console just saying FLAME.COM while showing flames on the screen:

![FLAME.COM](/cybersecurityPhotos/virusImages/fireVirus.jpeg)

This virus was pretty interesting but others went to just be visually annoying so much so that it can hurt someone's eyes but, again, still quite interesting:

![colors](/cybersecurityPhotos/virusImages/colors.gif)

Last but not least of my showcase here is a virus called kuku which definitely shows being like that when you see it in action. Unfortunately, I could not find a gif of it but it you can still see the results from an image:

![kuku](/cybersecurityPhotos/virusImages/kuku.png)

Overall, there can be an appreciation for this type of art. Something that is not so malicious that it would steal and transmit personal data but something that is malicious enough to still cause a stir in not only the user but also an organization. But still, one look at these viruses of old and still, again, appreciate the art form the demonstrate.

If you are interested in seeing more old viruses on your own you can look at the internet archive's malware museum [here](https://archive.org/details/malwaremuseum?page=2)

## Modern Malware

Modern malware of today is one that a lot more malicious than that of the some the viruses of old. Today modern malware aims to take personal data to used by a hacker to sell it. Now mainly malware holds data for ransom, called ransomware, that demands payments in the form of bitcoin or some other type or crypto currency. If a malware is not a ransomware, it may be worm instead, traveling from device to device until an intended target is found.

But starting off with ransomware, there are some major examples that have been through the news in the past. One major one was called the Wannacry virus which used an exploit called Eternal Blue (I have written an article on the history of this exploit if you are interested) had exploited a weakness in the SMB service to spread within a network. This virus had compromised many devices and had caused major damage to many organization around the world. Like any other ransomware, it had encrypted the data on a user's laptop and demanded a payment in bitcoin. Here is what a computer looks like when infected: 

![WannaCry](/cybersecurityPhotos/virusImages/WannaCry.png)

As you can see, it demands the user bitcoin in exchange for the data being decrypted. Now many organizations have ransomware insurance and will pay out money just to see if hackers are actually telling the truth. Sometimes hackers do stay by their word but others won't. It is always a hard decision to make in times where you don't have such insurance. 

Now on the other hand, we have worms. One of the most famous of which was the Stuxnet virus. This virus had traveled from device to device around the world until it found a particular nuclear powerplant in the middle east. The virus would actually slow but surly raise the temperature of the reactor to eventually explode it. This virus was later found out to have connections to the NSA and that it was an operation to take out a few targets they had in mind. 

## Final Words

The days of old MS DOS malware have long gone and now the malware of today aims to steal or hold ransom personal data for money. But the evolution of how we got to this point in time is interesting where it started with theories of self-replicating automata to the very first computer virus and the finally to modern ransomware and worms, the journey how we got here is an exciting one. 

[^1]: https://history-computer.com/technology/the-first-computer-virus-of-bob-thomas/
[^2]: https://historyofcomputers.eu/inovation/the-first-computer-virus-origins-and-evolution/
