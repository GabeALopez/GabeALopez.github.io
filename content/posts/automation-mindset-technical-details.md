---
date: 2025-07-05
# description: ""
# image: ""
lastmod: 2025-07-13
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

With the code itself there are two main pieces of code that I wrote up. One that handled the creation of a markdown file and one that handled getting the information from the Defender API.

These are create_template_with_API.py and account_info.py respectively

If you would like to see the raw code here is the [Link](/projects/cybersecurity/raw-cybersecurity-markdown-notes/raw-risky-user-code)

Going foreword I am going to do an overview with each function as it will take a long time to go over each line.

But I'm going to start off with the account_info.py script and start with the "start" function:

```python
# Main function that starts the process, takes account UPN and a threading lock as parameters
def start(account_upn_param, lock: Lock) -> str:

    # Read the authorization cookie from a template file
    with open("template_authorization.txt", 'r') as file:
        file_content = file.read() 

    auth_cookie = file_content

    # Line numbers for reading different URLs (incident and query)
    incident_line = 1
    query_line = 2

    # Get the incident and query URLs from a predefined list of URLs
    incident_url = read_urls(incident_line)
    query_url = read_urls(query_line)

    # Assign the input account UPN parameter to a local variable
    account_upn = account_upn_param 

    # BUG: Edge case where there are no identity logon events but there are entries in AADSignInEventsBeta
    # Construct the user info query to fetch the user's creation date and last password change timestamp
    user_info_query = (
        f"let created_date_time = IdentityInfo | where AccountUpn contains '{account_upn}' "
        "| project CreatedDateTime, AccountUpn;"
        "AADSignInEventsBeta | join kind=innerunique created_date_time on AccountUpn"
        "| take 1 | project CreatedDateTime, LastPasswordChangeTimestamp"
    )
    
    # Query to get the account display name, sorted by the most recent generation time
    account_display_name_query = (
        f"IdentityInfo | where AccountUpn contains '{account_upn}' "
        "| sort by TimeGenerated desc | take 1 | project AccountDisplayName"
    )
    
    # Construct query objects for API requests
    query = {
        "Query": f"{user_info_query}"
    }
    display_name_query = {
        "Query": f"{account_display_name_query}"
    }

    # Make API requests to fetch incident details and user-related data
    first_activity, incident_id = incident_info_api_request(incident_url, auth_cookie, account_upn, lock)
    created_data_time, last_pass_change_time = query_api_request(query_url, auth_cookie, query, lock)
    
    # Check if the account is an employee account
    is_employee = is_employee_account(account_upn)
    
    # Fetch the account display name using a separate API request
    account_display_name = display_name_api_request(query_url, auth_cookie, display_name_query, lock)

    # Return all collected data
    return created_data_time, incident_id, first_activity, \
        last_pass_change_time, is_employee, account_display_name
```

The main overview of this function is that it is the main function for this program that controls the whole code. 

Furthermore, this code handles setting up the all the queries that are going to be fed into other functions and fired off to the API.

Additionally, the main function will read designated urls (i.e. Defender API url, query API url, etc) from a text file and use them in making requests to the Defender API.

Once the queries and getting the urls are set up, this data is then passed into the varying functions. 

---

Going down the lines in the start function, the first function we hit is the read_urls function:

```python
def read_urls(line) -> str:
    # Open the file in read mode
    with open('template_urls.txt', 'r', encoding='utf-8') as file:
        # Read all lines into a list
        lines = file.readlines()

    # Check if the specified line number is valid
    if 1 <= line <= len(lines):
        # Get the URL from the chosen line
        url = lines[line - 1].strip()  # Adjust index for 0-based indexing
        return url
    else:
        print("Invalid line number.")
```

This function is straightforward as all it does is read the specific line that the function is supplied.

So for instance, if I supply the function with the number 1 it will read the first line of the text document called "template_urls.txt"

To be honest, this function could reworked to be a bit more pertinent to the entire code as everything for reading urls could have been self contained. 

But it gets the job done and that's what matters here.

Unless it is slow, then start caring :\)

But overall, pretty simple function. Nothing crazy about it.

---

The next we going to look at is the "incident_info_api_request" function:

```python
# Function to make an incident info API request
def incident_info_api_request(url_param, cookie, user_principal_name_param, lock: Lock) -> str:
    try:
        with lock:
            print("\rGetting Incident Info...")
            sys.stdout.flush()


        # Ensure the URL is properly encoded
        encoded_url = quote(url_param, safe=':/?&=')

        headers = {"Authorization": cookie.encode('utf-8')}

        # Send request and handle response
        response = requests.get(encoded_url, headers=headers)
        response.raise_for_status()  # Raise an error for bad status codes
        json_response = response.json()

        incident_id = ""
        first_activity = ""

        # Extract relevant incident information
        for incident in json_response.get('value', []):
            alerts = incident.get('alerts', [])
            if not alerts:
                continue

            entities = alerts[0].get('entities', [])
            if not entities:
                continue

            user_principal_name = entities[0].get('userPrincipalName', '')

            if user_principal_name != user_principal_name_param:
                continue
            else:
                first_activity = alerts[0].get('firstActivity', '')
                incident_id = incident.get('incidentId', '')
                break

        with lock:
            # Ensure proper encoding for console output
            print("\rIncident Web Request Done!".encode(sys.stdout.encoding, errors='replace').decode(sys.stdout.encoding))
            sys.stdout.flush()

        if incident_id:
            return first_activity, incident_id
        else:
            return "N/A", "N/A"
    except requests.RequestException as e:
        print("Error:", e)
        exit()
```

This one is a big one, as it is trying to search for an associated incident ID and/or the latest timestamp of the risky user alert.

First off the parameters that are being passed into this function are the incident url to the Defender API, the browser cookie, the account upn, and a lock.

The lock is used here for the animation here. I created a little loading animation for when the script is running to give that extra pizazz.

Now the next few lines mainly handle authorization where I assemble the request to the incident url with the browser cookie.

Furthermore, I also assemble the payload with the user's upn to get results back for the user.

Next, the for loop iterates through the json response to see if there is an incident ID associated with the user.

If there isn't any, it will pass an empty string to the the two vars.

Sometime Defender didn't have an incident ID associated with the user and often this would be the case.

Once that's done, the function will return with the values back to the start function.


---

# Under Construction

---
