---
date: 2025-06-26
# description: ""
# image: ""
lastmod: 2025-06-27
showTableOfContents: false
tags: ["Cybersecurity", "History"]
title: "Automation Mindset - A How To"
type: "post"
---

# Introduction

**Welcome! Welcome!** Traveler, I see you’ve come to hear the tale of automation’s greatness. Excellent choice. Shall we begin?

So… what *is* automation? I know, I know—you didn’t come here for a history lesson. Neither did I. But a little context helps, so don’t click away just yet. You hear me?

Anyway, in today’s digital world, automation means using technology to handle repetitive tasks—automatically. Instead of manually sending emails, moving files, or copying data, software does it for you.

(Yep, those last two sentences were straight from ChatGPT. But hey, it got the point across!)

What’s that? You want a *human* explanation now? *Sigh.* The things I do to keep you people happy…

So why does automation matter? Because doing the same boring tasks over and over sucks. Plain and simple. On a more professional note, it also reduces errors, saves time, and lets you focus on work that actually requires thinking.

---

# The Meat and Potatoes

See? That wasn’t so bad.

Now, how can *you* start thinking about automation—whether in your daily routine, your job, or even your own business?

### Step 1: Identify repetitive tasks

Start by noticing what you do over and over again. Do you copy/paste data between apps? Keep retyping the same thing into a spreadsheet? That’s your automation opportunity.

If you find yourself saying, “Not this again,” congrats—you’ve found something you can probably automate.

### Step 2: Ask, “Can a program do this for me?”

Once you've spotted that annoying task, ask yourself: *How could software do this instead of me?*

That’s where **scripting** comes in.

You write a small script (a simple bit of code) to repeat the task for you. For example, if you're working with specific software, you might use an **API** to pull the data automatically. If there’s no API, you might use **web scraping** to grab it from the interface.

---

### A Simple Analogy

Let’s say I’m a baker. Every day I make cakes, but they all start the same way—get the ingredients, mix, bake, cool, etc. It’s repetitive.

So I hire a machinist to build a robot to handle that base process. Now I can jump straight to the fun part: decorating cakes.

But what if I want the robot to adjust flavors based on the customer’s order? The machinist tweaks it so it reads the flavor from the order sheet.

If the order sheet is clean and well-structured (like data from an **API**), easy peasy.

But if the orders are written messily by hand (like **web scraping** messy websites), the machinist has to teach the robot to recognize patterns in all that chaos.

And if someone changes how they write the orders? The robot breaks. That’s the downside of automation—your process is only as good as the data it depends on.

---

# A Real-World Example

During my internship, I had to triage risky user alerts every day. Before I could even *start* investigating, I had to manually collect basic info about each user:

- When was the account created?
- Who’s the user?
- What IP triggered the alert?

Every. Single. Time.

I’d copy this into a text document before I could even start analyzing the situation. That manual step slowed me down—and made the process more frustrating than it needed to be.

So I asked: *How can I get this information into a text doc automatically, every time I see a risky user?*

The org was using Microsoft Defender 365. I realized I was getting all my info from the Azure Sign-In logs. Later, I started using **KQL** (Kusto Query Language) in Defender to get even more accurate data.

At this point, I had two options to automate getting that data:
1. Use an **API**
2. Use **web scraping**

Both required scripting—usually in Python or PowerShell. And no, you don’t need to know the code *right now*. First, understand the concept. The code comes after the plan.

---

# A Quick Detour: APIs vs Web Scraping

\<INSERT LINK TO SECTION\>

---

# Back on Track

Now that you know what APIs and web scraping are, the question becomes:

**How can I use them to pull data into a usable, automated format?**

Most vendors provide APIs. These are easier to work with because the data is already structured. But sometimes, if an API isn’t available (or access is limited), you have to resort to web scraping.

In my internship, I ended up using an unofficial method. I didn’t have an API key—but I *did* have my cookie value. Not ideal, but it worked. Sometimes in automation, you’ve gotta do what works—within reason and policy, of course.

---

# The Bottom Line

If you haven’t caught the theme yet:  
**If something is repetitive and consistent, you can probably automate it.**

Start noticing the time-sucking tasks in your day. The stuff that makes you roll your eyes. Then ask yourself how a script could take that load off your plate.

Even if you’re not a coder (yet), just understanding how APIs and web scraping work will set you up for success. Learn to see the patterns—and the pain points—and automation will naturally follow.