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

If you find yourself saying, “Ugh, not this again,” congrats—you’ve found something you can probably automate.

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








# Introduction 

Welcome! Welcome! Traveler I see you wish to hear about the greatness of automation! That's good news. Well? Shall we begin? What is automation? I know I know you didn't come here for a history lesson. Neither did I but this is to give you context to everything I will say. So don't click away just yet. You hear me!?

Anyway automation, in today’s digital workflows, means using technology to handle repetitive tasks automatically. Instead of doing things like sending emails, moving files, or entering data by hand, software tools do it for you. Yep those last two sentences where straight from ChatGPT! But it gets that point across. What's that? You want human responses now? *sigh* fine. The things I have to do to please these people I swear. But anyway, why is this important? Automation is important because you don't want to do the same BS over and over again! But scientifically, it helps to reduce errors and save time. 

# Meat and Potatoes

See. It wasn't going to be that long. Anyway, how can you start to thinking automation in your day to day life? Or maybe in your workplace? Or maybe in your own company? One of the first things you can do is start thinking about things you do in your workflow that is repetitious. This can be you copying and pasting a lot between two programs or it can information you copy/paste a lot into a text doc.

The idea is that if you notice an action you do repeatedly and consistently, you can automate it. The second part of this understanding is asking: How can I get software to do this for me so I don’t have to keep repeating the same task over and over again?

This is where scripting comes in. You use scripts—or code—to perform the same actions repeatedly in order to get the data you want each time. This saves both time and energy. Now, if you're using a specific program or software, like I was with the SignIn logs, you would typically use an API. However, not all software providers offer APIs, so sometimes you need to use web scraping to get the data instead.

I’ll explain APIs and web scraping in more detail later, but the basic thing to understand is this: these are programmatic tools you can use to turn data you frequently copy and paste into a more repeatable, automated format. You can then feed that data into a program to process it automatically.

To give a high-level overview, think of it this way:
Let’s say I’m a baker. Every day I bake different types of cake, but every cake starts with the same base. In order to make that base, I have to get the recipe, gather the ingredients, mix them together, pour the mixture into a tin, bake it, take it out, wait for it to cool—only then can I begin designing the actual cake.

As you can see, just making the base involves a lot of repetitive steps. So I hire a machinist to build a robot that handles all of those steps for me. Now, when I start my day, I can jump straight into the fun part—designing the cake.

You might wonder, What about the flavor? That’s why I ask the machinist to tweak the robot so it can adjust flavors based on each order.

Then comes the next question: How does the robot know what the orders are? In our case, the robot reads the orders as they come in on a conveyor belt—but only if the orders follow a specific structure. The machinist says, “No problem,” and updates the robot to read that format. Once it reads the order, it processes the data and begins the repetitive steps automatically.

In this analogy, the order format is like data from an API—structured and predictable.
With web scraping, however, things are messier. The orders may come in different formats depending on who writes them, but the essential information is still there. The machinist then studies how each employee writes their orders and teaches the robot to read them accordingly, based on those patterns.

Of course, you might notice some flaws in this whole system. That’s the challenge with a lot of programmatic automation: if the data isn’t consistent, the robot breaks. And unfortunately, not many people know how to fix the robot when it does...

To give a more real-world example, during my internship I was tasked to triage through risky users and determine whether or not there was a risk. However before I started the triage I need to get some basic user info (ie. When the account was created, who was it, what IP addr was the alert coming from, etc.). And every time I had a risky user, which every day I would have to collect this information every time and put it in a text doc. Then do my investigation. Checking IPs, finding impossible travel, find compromised users, etc. Do you notice how repetitious that is? And especially how it slows down my investigation? I could be saving time actually doing my investigation if I just had the info to start with. 

So at this moment, I thought I want to somehow get this information into a text doc every single time I see a particular risky user and for that particular risk user. How can I do that? At this moment, I started thinking about my process of how I got the user information. And this is where you should be thinking about this too. Where do I get this information repetitiously? For me, since the organization was using Defender 365, I got my information from azure SignIn logs but I later would use the KQL language in Defender to get the information. At this point, the question remains how do I get the SignIn Log info out from Azure into a text doc. If you write up scripts you might be thinking of one solution but those who don't know, in the world of programming there are usually two ways to get info from a program. Either A, web scrape the site, or B use an API. I'm not saying there aren't other ways going about it but these are usually the main two. And because of the way that these two topics operate you are going to need a know a little bit of scripting. But don't worry you are not going to need know it here per se. If anything understand the concept, not any code. Code comes after planning. But anyway, usually either python or PowerShell will be allowed so assume that you are using either of those scripting languages.

But before we go further we have to go on a little detour to explain what web scrapping and APIs are. For those who want to skip click here

\<INSERT LINK HERE\>

# APIs and Web Scrapping: What the Hell Are They?

# Back on Track

With that explanation out of the way. The important to think about is how can I leverage these tools to get info out of them. The idea behind this, is that you want to get the info you repeatably grab into a more programmatical form so that it can be easily transferred into a text document via a quick program.

Most vendors are nice enough to give you an API for their program so I would usually go down this route since data formatting will be easier. However, sometime you have to use web scrapping to get the info you are looking for and that can take a little bit of data wrangling. In my case, during my internship, I was able to find an API that would give me that information in Defender. Now usually you would have an API key you would use to authenticate, however for me I didn't have that but what I did have was my cookie value. Which was not the greatest way of doing things but it is what worked and that is something that you have to get used to sometimes. You might not be able to access data the right way, or official way but if that what takes and allowed then take it. 

If you haven't been seeing the idea already, if something is done repetitiously and consistently it can be automated with a program. And the important thing is to start disliking the repetitious acts you do on a daily basis and feel the time waste that you are doing, doing this act over and over again. Additionally, it is important to understand that you want to take these tools and use them to 

Continuing, the idea is that I want to get the raw data from either and API or through scraping into a text doc and use requests from a program to do this.