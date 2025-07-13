---
date: 2025-07-12
title: "Raw Risky User Code"
description: "This page includes the raw code I used for automating risky users"
tags: ["Cybersecurity", "resources", "raw notes"]
type: "post"
---

# account_info.py

```python
import requests
import urllib.error
import urllib.request
import json
import sys
from threading import Lock
from urllib.parse import quote

"""
Version 1.0
"""

#TODO: Grab risky users from entra id (Overall)
#TODO: [] risky detection timestamp

# Get display name from account API request
def display_name_api_request(url_param, cookie, query_param, lock: Lock) -> str:
    try:
        with lock:
            print("\rQuerying User Display Name...")
            sys.stdout.flush()

        # Convert query parameters to JSON payload
        json_payload = json.dumps(query_param)

        # Set headers
        headers = {
            "Authorization": cookie,
            "Content-Type": "application/json"
        }

        # Send request and handle response
        response = requests.post(url_param, data=json_payload, headers=headers)
        response.raise_for_status()  # Raise an exception for HTTP errors

        # Process response
        json_response = response.json()
        results = json_response.get('Results', [])
        if results:
            account_display_name = results[0].get('AccountDisplayName', 'Unknown')
            with lock:
                print("\rKQL Web Request Done!")
                sys.stdout.flush()
            return account_display_name
        else:
            print("No results found in the response.")
            sys.stdout.flush()
            return None

    except requests.exceptions.RequestException as e:
        print("Request Error:", e)
        sys.stdout.flush()
        return None

# Function to make a query API request
def query_api_request(url_param, cookie, query_param, lock: Lock) -> str:
    try:
        with lock:
            print("\rQuerying...")
            sys.stdout.flush()
        
        # Convert query parameters to JSON payload
        json_payload = json.dumps(query_param).encode('utf-8')

        # Create request object
        req = urllib.request.Request(url_param, data=json_payload, method='POST')
        req.add_header("Authorization", cookie)
        req.add_header("Content-Type", "application/json")

        # Send request and handle response
        with urllib.request.urlopen(req) as response:
            response_data = response.read()
            json_response = json.loads(response_data.decode('utf-8'))
            results = json_response['Results'][0] 
            
            created_data_time = results.get('CreatedDateTime')
            last_pass_change_time = results.get('LastPasswordChangeTimestamp')

        with lock:
            print("\rKQL Web Request Done!")
            sys.stdout.flush()
        
        return created_data_time, last_pass_change_time
    except urllib.error.URLError as e:
        print("Error:", e)
        sys.stdout.flush()
        exit()

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

# Function to check if an account is an employee account
def is_employee_account(UPN_param) -> bool:
    return not any(char.isdigit() for char in UPN_param)

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

# create_template_with_API.py

```python
import shutil
import account_info
import itertools
import threading
import time
import sys

"""
Version 1.0
"""

# Function to get user input
def get_risky_user(display_name):
    risky_user = display_name
    user_parts = []

    if ',' in risky_user:
        user_parts = risky_user.split(',')
        risky_user = user_parts[1].strip() + "_" + user_parts[0].strip()
    else:
        risky_user = risky_user.replace('_', ' ')

    return risky_user

# Function to create a new markdown file and write headers
def create_markdown_file(risky_user):
    document_title = "Risky_User-" + risky_user
    shutil.copy("Risky_User_MarkdownTemplate.md", "workInProgressUsers\\" + document_title + ".md")

    file_header = "**" + document_title + "**"

    with open("workInProgressUsers\\" + document_title + ".md", 'r+') as file:
        # Read the contents of the file
        file_contents = file.read()
        
        # Move cursor to the beginning of the file
        file.seek(0)
        
        # Write the header at the top of the file
        file.write(file_header + '\n\n')
        file.write("**Risky User - " + risky_user.replace("_", " ") + "**" + '\n\n')
        
        # Write back the existing contents after the header
        file.write(file_contents)
        file.truncate()  # Truncate any remaining content if the new content is shorter

# Function to insert information after specific headers
def insert_information(document_title, info_dict):
    file_path = "workInProgressUsers\\" + document_title + ".md"

    # Read the file contents
    with open(file_path, 'r') as file:
        lines = file.readlines()

    # List of headers to search for
    headers = [
        "- Account Created:",
        "- Is Employee?:",
        "- Associated Defender Incident num:",
        "- Associated Defender Incident Timestamp:",
        "- Timestamp of risky detection:",
        "- Last Password Change:"
    ]

    # Insert information after each header
    new_lines = []
    for line in lines:
        line_modified = False
        for header in headers:
            if line.startswith(header):
                new_line = line.strip() + " " + info_dict.get(header, "Information not provided") + '\n'
                new_lines.append(new_line)
                line_modified = True
                break
        if not line_modified:
            new_lines.append(line)

    # Write the modified content back to the file
    with open(file_path, 'w') as file:
        file.writelines(new_lines)

done = False
lock = threading.Lock()

# Here is the animation
def animate():
    for c in itertools.cycle(['|', '/', '-', '\\']):
        if done:
            break
        with lock:
            sys.stdout.write(f'\r\033[Kloading {c}')  # Clear the line before printing the animation frame
            sys.stdout.flush()
        time.sleep(0.1)
    with lock:
        sys.stdout.write('\r\033[KTemplate Created!\n')  # Clear the line and print completion message

# Main script function to execute the process
def main():
    global done  # Declare 'done' as a global variable to control the animation thread

    # Prompt user to enter the account UPN (User Principal Name)
    account_upn = input("Enter account UPN: ")

    # Start a separate thread to run the animation function, indicating processing is ongoing
    t = threading.Thread(target=animate)
    t.start()

    # Call the start function from account_info module to get user and incident details
    # This function likely prints messages and takes a lock to ensure thread safety
    created_date_time, incident_id, first_activity, \
        last_pass_change_time, is_employee, account_display_name = account_info.start(account_upn, lock)

    # Determine if the user is considered risky based on their account display name
    risky_user = get_risky_user(account_display_name)

    # Create a Markdown file named after the risky user
    create_markdown_file(risky_user)
    
    # Define the document title using the risky user's name
    document_title = "Risky_User-" + risky_user 

    # Dictionary to store information that will be inserted after each header in the Markdown file
    info_dict = {
        "- Account Created:": f"{created_date_time}",
        "- Is Employee?:": f"{is_employee}",
        "- Associated Defender Incident num:": f"{incident_id}",
        "- Associated Defender Incident Timestamp:": f"{first_activity}",
        "- Timestamp of risky detection:": f"notDoneYet",  # Placeholder for future implementation
        "- Last Password Change:": f"{last_pass_change_time}"
    }

    # Insert the collected information into the Markdown document under relevant headers
    insert_information(document_title, info_dict)

    # Set the 'done' flag to True to signal the end of processing
    done = True
    
    # Wait for the animation thread to finish before exiting the main function
    t.join()


if __name__ == "__main__":
    main()
```