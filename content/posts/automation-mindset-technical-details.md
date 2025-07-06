---
date: 2025-07-05
# description: ""
# image: ""
lastmod: 2025-07-05
showTableOfContents: false
tags: ["Cybersecurity", "Automation"]
title: "Automation Mindset - Technical Details"
type: "post"
---

# Foreword

As a brief disclaimer, I want to make it clear that I do not consider myself an expert or advanced scripter, and that is completely acceptable. It is important to understand that not all code is perfect on the first attempt, and the code I will be discussing here is no exception.

This was my first serious attempt at automating a task within a real enterprise environment, so the code is far from optimal.

In the world of scripting, functionality often takes precedence. Optimization typically becomes a priority only when the code becomes noticeably slow or difficult to work with.

Of course, this reflects my personal perspective. You are welcome to interpret it as you see fit.

But without a further adieu, let's jump into the start of technical details.

---

As mentioned in the first automation post, it is important to understand what data you want and how to get it. 

When I was automating risky user data, I needed to find a way to grab the azure data for a user. I had used the API explorer that is in O365 (aka Defender), which could run KQL statements. 

So the KQL statement I used in to send to the API looked like this:

```kql
let created_date_time = IdentityInfo
| where AccountUpn contains 'account_upn'
| project CreatedDateTime, AccountUpn;
AADSignInEventsBeta 
| join kind=innerunique created_date_time on AccountUpn
| take 1 
| project CreatedDateTime, LastPasswordChangeTimestamp
```

---

Let's walk through the code starting with the first three lines:

```kql
let created_date_time = IdentityInfo
| where AccountUpn contains 'account_upn'
| project CreatedDateTime, AccountUpn;
```

In KQL, the keyword **let** signal usage of a variable. So in this instance, entire query after the "=" character and before the ";" character is saved into the variable called "created_data_time"

This is helpful if we want to make the rest of the query look less cluttered. 

The next line is saying that in the IdentityInfo, show be results where the values in the AccountUpn column contain "account_upn", where account_upn is the user principal name you are looking

In our case, it will be a user email. So ```bob.evans@example.com``` would be an example of the principal name we are looking for. 

In the final line, it says that for every entry only show the CreatedDateTime and AccountUpn columns.

This is so that less data has to be displayed and making the query run a little faster.

Once all of that query is ran, it is saved into the var to be used in the next part of the query

So at this point, we have the Date/Time of Bob Evans's account and the UPN, which will bused in the next part of the query

---

```kql
AADSignInEventsBeta 
| join kind=innerunique created_date_time on AccountUpn
| take 1 
| project CreatedDateTime, LastPasswordChangeTimestamp
```

Now, in the next part, we are going to query the AADSignInEventsBeta table, which contains information about user's SignIn logs but also some other metadata on the user's account

In the next line, we are going to join the data from the "created_date_time" query (or table) with the current AADSignInEventsBeta table on the AccountUpn. The query is using an innerunique join.

To get a visual of what this looks like, you can see the visual at the official Microsoft (MS) documentation [here](https://learn.microsoft.com/en-us/kusto/query/join-operator?view=microsoft-fabric)

The two circles, in the visual represent tables and the data were joining on is the middle of the two circles

So in our case, the only SignIn logs (or more precisely table entires) that are going to be shown are those with the ```bob.evans@example.com``` in the AccountUpn column.

From here, we are going to only take the first entry the pops up. After that we are only going to show the CreatedDateTime and LastPasswordChangeTimestamp columns for the user.

So in summary, when we input a user email we are going to get the Date/time of when the user's account was created and the timestamp of when the user changed their password last as output.

It is a bit of a long one but I hope the KQL makes sense. Also have to stick with me, because we haven't gotten to the API part of this.

---

But before that I want to answer a question someone might have. 

How did I figure out what data were in these tables and, by extension, columns? And how did I figure out which keywords to use?

Starting with the keywords, I have a background in some SQL from some database projects I have done in the past. So kql was very similar in syntax to it and did a trial and error of was the same and what wasn't.

But for those who don't have the background it is going to be a little harder of course.

Two good things you can do is read documentation and following examples, watching input and output. 

For documentation, I am not saying to read the entire thing but read the "Get started" guide so you can follow how to run and write queries.

At the end of the day, documentation is meant to be referenced not read. 

Secondly, look into many examples. Look at how they run in your own environment. Also make sure to break apart your queries.

Run each line one by one added together so you can understand logic of the query.

With figuring out the tables and columns I needed to use, I had done trial and error. I had looked through the available tables I had and just ran the tables by themselves, which gives a lot of data.

I had just combed through the columns and tried to understand what data was being given to me. So for example, when I was rummaging around in the AADSignInEventsBeta table I had found that it had a AccountUpn column and a LastPasswordChangeTimestamp column. 

This was interesting as this table had the AccountUpn which matched up with another AccountUpn column in the IdentityInfo table. So I thought, what if I joined them on that column. 

Additionally, the IdentityInfo column was missing the LastPasswordChangeTimestamp column but did have the CreatedDateTime which was not present in the AADSignInEventsBeta. So what if I combined them together and only showed the necessary columns? And that's what I did

There are also keywords like: getschema that will get you the schema of the table so you can more easily understand what is in it skeleton-wise

But I prefer just taking the first few rows and looking at how the data is presented. 

---

With that out of the way, it's now really time to talk about the code. 

Which I'll come back to when I finish writing up this post.

---

---

# Under Construction

---
