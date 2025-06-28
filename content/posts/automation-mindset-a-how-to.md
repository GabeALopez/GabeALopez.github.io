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

Welcome! Welcome! Traveler I see you wish to hear about the greatness of automation! That's good news. Well? Shall we begin? What is automation? I know I know you didn't come here for a history lesson. Neither did I but this is to give you context to everything I will say. So don't click away just yet. You hear me!?

Anyway automation, in today’s digital workflows, means using technology to handle repetitive tasks automatically. Instead of doing things like sending emails, moving files, or entering data by hand, software tools do it for you. Yep those last two sentences where straight from ChatGPT! But it gets that point across. What's that? You want human responses now? *sigh* fine. The things I have to do to please these people I swear. But anyway, why is this important? Automation is important because you don't want to do the same BS over and over again! But scientifically, it helps to reduce errors and save time. 

# Meat and Potatoes

See. It wasn't going to be that long. Anyway, how can you start to thinking automation in your day to day life? Or maybe in your workplace? Or maybe in your own company? One of the first things you can do is start thinking about things you do in your workflow that is repetitious. This can be you copying and pasting a lot between two programs or it can information you copy/paste a lot into a text doc.

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



The idea is that if you see an action you do over and over again and is done consistently, you can automate it. That is the first part. The second part to the understanding. The next how can I get software to do this for me so I don't have to do this over an over again. 

Well this is where scripting comes in. You use scripts to run the same actions, or code, over and over again to get you the data you want every time you do something. And this saves time and energy. Now if you are using a particular program or software like I was with the SignIn logs you would use an API, however not all software are willing to give you an API so you have to use web scrapping to do. Now I will explain that later but the basic thing to understand that is that these programmatic tools you can leverage to get the data you copy and paste all of the time into a more repeatable format and feed that data into a program to process. 

So think about it this way to give a high level overview. Let's say I am a baker and every day I bake different types of cake, however every time start creating the cake I make a base. So every cake starts out with this base and then create the cake from the there. In order to make the base, I have to get the recipe out, grab the ingredients, mix up the ingredients, put the mix into a tin, put it into the over, take it out, wait for it cool, and then I can start designing the cake. Do you notice how repetitious it is just to get to the base cake. So then I get a machinist to create a robot for me to do all of these beginning steps for me. Now when I start the day, I can start working on the fun part, actually designing the cake. You might be thinking, what about the flavor. This is why you ask the machinist to modify the robot to get the flavors that come in for the orders. 

The next question comes now. How does the robot know what the orders. Well in our case, the robot is able to read the order as the come in on a conveyer belt, however the orders are only written in a set structure. The machinist says: "No problem" and modifies the robot to read the format and read the data that comes from it. Once read it processes the data and then starts doing the repetitious process. In our case, the order format is the data that is the data formatted from an API. Now with web scrapping, there is data wrangling. So in the case of the orders, the orders instead would be put into varying orders and formats. However the important data is still there and the employees all tend to write their orders in the same way. So machinist, looks at how all of the orders are formatted from each employee and tells the robot how to read those orders depending on how it is formatted. 

Of course, you might notice some flaws in all of this and is the issue with a lot of programmatic automation. The issue being is that, if the data is ever not consistent then the robot will break. Such is how it is but not a lot people know how to fix this robot so...