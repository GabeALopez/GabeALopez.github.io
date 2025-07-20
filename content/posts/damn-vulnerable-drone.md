---
date: 2025-07-20
# description: ""
# image: ""
lastmod: 2025-07-20
showTableOfContents: false
tags: ["Cybersecurity", "Drone"]
title: "Damn Vulnerable Drone"
type: "post"
---

> The old saying that the best way to learn is by doing holds as true for penetration testing as for anything else, which is why intentionally vulnerable systems like the Damn Vulnerable Web Application are so useful. Until now, however, there hasn’t been a practice system for penetration testing with drones.
> 
> The Damn Vulnerable Drone (DVD, a slightly confusing acronym) simulates a drone which flies in a virtual environment under the command of of an Ardupilot flight controller. A companion computer on the drone gives directions to the flight controller and communicates with a simulated ground station over its own WiFi network using the Mavlink protocol. The companion computer, in addition to running WiFi, also streams video to the ground station, sends telemetry information, and manages autonomous navigation, all of which means that the penetration tester has a broad yet realistic attack surface.
> 
> Author: Aaron Beckendorf
>
> Date: July 20, 2025
>
> [A Vulnerable Simulator For Drone Penetration Testing](https://hackaday.com/2025/07/18/a-vulnerable-simulator-for-drone-penetration-testing/)

This is an interesting article I had found from looking through some news feeds.

I have heard of the Damn Vulnerable Website (DVW) but it seems interesting to look into pentesting drones as they are being used more often for surveillance purpose. 

I have heard of controllers that exist to block the signal between the controller and the drone.

But actually attempting to hijack it with commands would be interesting thing and could be found using this drone simulator

When I saw this I started looking into some more info with drone hacking it seems to be somewhat of a niche field at least technical-wise.

Most articles that I found never really went into detail but mostly just said to do regular patches

This meaning that attackers would go after unpatched firmware and software and/or attack the encrypted wifi/RF signals with aircrack-ng.

Additionally, I have found there attacks on the mobile apps that used to control these drones as well as 

Overall, this seems like an interesting niche to get into if you are already into hardware/wifi hacking. 

### Extra Reading

[How to Hack a Drone: Security Risks and Countermeasures](https://undercodetesting.com/how-to-hack-a-drone-security-risks-and-countermeasures/)

**Description:** Simple but not very descriptive 

[DroneSploit](https://github.com/dronesploit/dronesploit)

**Description:** Metasploit but for drones 

[How To Hack A Drone](https://robots.net/tech/how-to-hack-a-drone/)

**Description:** Cover attacks more conceptually rather than technically.