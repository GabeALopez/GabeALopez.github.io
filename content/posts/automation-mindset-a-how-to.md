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

Why does automation matter? Because doing the same boring tasks over and over sucks. It’s that simple. On a more professional note, it also reduces errors, saves time, and lets you focus on work that actually requires thinking.

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

As mentioned earlier, this section is about APIs and web scraping.

Starting with APIs—what are they?

The acronym stands for **Application Programming Interface**, and the idea behind APIs is that they give programmers and scripters a clean, consistent way to interact with software.

APIs typically return a nicely formatted version of the data you're looking for. However, not all APIs are made equally, so be sure to read the documentation of the specific API you're trying to use with your scripts or programs.

APIs are one of my favorite things about automation because of how powerful and well-structured they can be. Once you start looking for them, you start to see APIs *everywhere*.

Hell, even the Windows operating system has an API for developers (and malware devs) to interact with. But I digress.

The key thing to remember is this: APIs don’t just let you **get** data—they also let you **send** data.

If you’re following where this is going, you’ll realize you can automate far more than just reading information—you can automate entire actions by pushing data back to the system.

From there, the sky's the limit.

Now, I unfortunately can't tell you how to interact with every API, but the general approach is this:

- You send a **web request** to a **web endpoint**
- You include your **API key** for authentication

You usually register for an API key through the application you’re trying to access. Then, send web requests to the documented endpoints. Most API documentation includes examples of basic requests—so read the docs carefully and experiment with a few endpoints to get comfortable.

---

On the other side of the coin, you have **web scraping**.

Sometimes, you won’t have a nice API to work with. During my internship, I didn’t have a proper API endpoint available in the typical way.

Instead, I had to read **raw HTML** from websites and transform it into structured data.

But be clear—the data you're looking for usually won’t be in the static source page when you right-click and "View Source."

No, the real gold is in the **web requests** your browser sends to the server when you interact with a site.

A good example of this is LinkedIn.

LinkedIn *has* an API, but the community/free edition doesn’t give you access to much. I didn’t want to pay for access or go through the process of verifying a business, so I had to get creative and watch the web requests.

When I started thinking about automating my job search after my internship, I noticed that the job listings must be getting requested somehow behind the scenes.

So I opened **Inspect Element** in Firefox, clicked the button that loads the next page of job listings, and watched the **Network tab**.

There, I could see the requests my browser was sending to the LinkedIn servers. I found the specific one that fetched the next page of results—and guess what? I could replicate that request myself and get the same data.

From there, I studied the request and figured out how my browser was sending it—what headers, parameters, and cookies it used. Then I realized it was just hitting a particular endpoint.

All I had to do was:

1. Send the request myself
2. Authenticate using my browser cookie
3. Parse the returned **JSON** data
4. Extract the info I wanted

That, in essence, is **web scraping**.

It’s about understanding how your browser is interacting with a site, mimicking those requests, and extracting the data from the responses.

---

Between the two, I prefer **APIs**—they're cleaner, more stable, and meant to be used. But if a vendor doesn’t provide one, then you have to make do and scrape.

That’s just how it is. That’s life—sometimes you just have to make do with what you’ve got.


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

Start noticing the time-sucking tasks in your day. The stuff that makes you want to quit because it is so repetitive. Then ask yourself how a script could take that load off your plate.

Even if you’re not a coder (yet), just understanding how APIs and web scraping work will set you up for success. Learn to see the patterns—and the pain points—and automation will naturally follow.

Want to see how I actually wrote the script? I’ll be making a follow-up post that dives into the technical side.