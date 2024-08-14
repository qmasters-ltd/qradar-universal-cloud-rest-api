import requests
from datetime import datetime, timedelta
import time
import json
import os
from dotenv import load_dotenv

load_dotenv()

identifier = os.getenv('IDENTIFIER')
base_url = os.getenv('BASE_URL')
username = os.getenv('USERNAME')
password = os.getenv('PASSWORD')
events_per_fetch = int(os.getenv('EVENTS_PER_FETCH', 100))
initial_fetch_period = int(os.getenv('INITIAL_FETCH_PERIOD', 7))
sleep_time_in_seconds = int(os.getenv('SLEEP_TIME_IN_SECONDS', 120))
qradar_endpoint = os.getenv('QRADAR_ENDPOINT')

with open('config.json', 'r') as f:
    params = json.load(f)

fetch_counter = params.get('fetch_counter', 1)
events_count = params.get('events_count', 0)
sleep_time = params.get('sleep_time', sleep_time_in_seconds * 1000)
time_format = params.get('time_format', "%Y-%m-%dT%H:%M:%SZ")
bookmark = params.get('bookmark', (datetime.utcnow() - timedelta(days=initial_fetch_period)).strftime(time_format))
start_time = params.get('start_time', datetime.utcfromtimestamp(datetime.strptime(bookmark, time_format).timestamp()).strftime(time_format))

def log(message, log_type="INFO"):
    print(f"[{log_type}][dynamics365crm]: {message}")

log("Start fetching events...")
log(f"Username: {username}. Start time: {start_time}.")

next_link = f"https://{base_url}/api/data/v9.1/audits"

def post_events(events, identifier):
    headers = {
        'Content-Type': 'application/json',
        'Accept': 'application/json'
    }
    payload = {
        'logSourceIdentifier': identifier,
        'events': events
    }
    response = requests.post(qradar_endpoint, headers=headers, json=payload, verify=False)
    
    if response.status_code == 200:
        log(f"Successfully posted {len(events)} events to QRadar.")
    else:
        log(f"Failed to post events to QRadar. Status code: {response.status_code}, Reason: {response.text}", "ERROR")

while next_link:
    log(f"[Boomi]: Running fetch number {fetch_counter} for AuditLogs...")
    log(f"Fetching audits from URL: {next_link}")

    response = requests.get(
        next_link,
        auth=(username, password),
        headers={
            "Prefer": "odata.include-annotations=*",
            "OData-Version": "4.0",
            "Prefer": f"odata.maxpagesize={events_per_fetch}"
        },
        params={
            "$orderby": "createdon asc",
            "$filter": f"createdon gt {start_time}"
        },
        verify=False
    )

    log(f"Done fetching audits, got status code: {response.status_code}.")

    if response.status_code == 200:
        response_json = response.json()
        events = response_json.get("value", [])
        next_link = response_json.get("@odata.nextLink", None)

        events_count = len(events)
        log(f"Fetched {events_count} audits.")

        if events_count > 0:
            fetch_counter += 1
            log(f"Posting {events_count} fetched events...")
            post_events(events, identifier)

            start_time = events[-1]["createdon"]
            log(f"Max events date {start_time}.")

    else:
        log(f"status code {response.status_code}, abort to get events. Reason: {response.text}", "ERROR")
        break

    time.sleep(sleep_time_in_seconds)

# Save updated initialize parameters to config.json file
params['fetch_counter'] = fetch_counter
params['events_count'] = events_count
params['sleep_time'] = sleep_time
params['bookmark'] = start_time
params['start_time'] = start_time

with open('config.json', 'w') as f:
    json.dump(params, f, indent=4)

log("Fetching events completed.")
