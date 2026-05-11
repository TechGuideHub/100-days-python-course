# Day 78: Using an External API

**Focus:** Requesting data from a web API and turning the response into Python values  
**You will practice:** building URLs, adding query parameters, opening a web request with `urllib.request`, checking a response status, parsing JSON with `json`, extracting nested fields, and handling network or JSON errors  
**Estimated time:** 55-70 minutes

## Today's Goal

Today you will use Python to ask another service for data.

That service is called an API.

API stands for application programming interface. The name sounds formal, but the idea is practical:

```text
Your program asks for information.
Another program sends information back.
```

You have already worked with files on your own computer.

An external API is a little different. The data comes from somewhere else, usually over the internet.

By the end of today, you should be able to:

- explain what a URL is doing in an API request
- add query parameters with `urllib.parse.urlencode()`
- make a simple GET request with `urllib.request.urlopen()`
- read the response body as text
- parse JSON text into Python dictionaries and lists
- pull useful fields out of a nested response
- check a basic HTTP status code
- handle network errors without pretending the internet is perfect
- handle JSON parsing errors
- prepare for Day 79, where you will practice making API data easier to reuse

Today's examples use Open-Meteo, a public weather API.

You do not need an account.

You do not need to install any packages.

You do need an internet connection for the live request examples.

When your connection is off, slow, blocked, or the service is temporarily unavailable, the program may fail. That is not a sign that you did something wrong. It is part of writing programs that talk to the outside world.

## The Big Idea

An API request is a structured question.

Here is a URL you could paste into a browser:

```text
https://geocoding-api.open-meteo.com/v1/search?name=Tokyo&count=1&language=en&format=json
```

It has two main parts.

First, the base URL:

```text
https://geocoding-api.open-meteo.com/v1/search
```

That tells Python where to send the request.

Second, the query string:

```text
?name=Tokyo&count=1&language=en&format=json
```

That tells the API what details you want.

The query string is made of query parameters:

| Parameter | Value | Meaning |
| --- | --- | --- |
| `name` | `Tokyo` | Search for a place named Tokyo |
| `count` | `1` | Return one result |
| `language` | `en` | Use English names when possible |
| `format` | `json` | Send the answer back as JSON |

In Python, do not build query strings by hand once values can change.

Use `urllib.parse.urlencode()`.

Code:

```python
from urllib.parse import urlencode

base_url = "https://geocoding-api.open-meteo.com/v1/search"

params = {
    "name": "Tokyo",
    "count": 1,
    "language": "en",
    "format": "json"
}

query_string = urlencode(params)
url = base_url + "?" + query_string

print(url)
```

You should see:

```text
https://geocoding-api.open-meteo.com/v1/search?name=Tokyo&count=1&language=en&format=json
```

This is safer than typing the URL yourself because `urlencode()` knows how to handle spaces and special characters.

Try this small change:

```python
from urllib.parse import urlencode

params = {
    "name": "New York",
    "count": 1,
    "language": "en",
    "format": "json"
}

print(urlencode(params))
```

You should see:

```text
name=New+York&count=1&language=en&format=json
```

The space became `+`.

That is normal URL encoding.

## The Mental Model

Think of an API call as a five-step trip:

```text
1. Build the URL.
2. Send the request.
3. Receive a response.
4. Decode the response body.
5. Extract the fields you need.
```

For a JSON API, the flow looks like this:

```text
URL
 |
 | urllib.request.urlopen()
 v
HTTP response
 |
 | response.read().decode("utf-8")
 v
JSON text
 |
 | json.loads()
 v
Python dict or list
```

The response has two useful parts.

The first part is the status.

Common status codes include:

| Status | Meaning |
| --- | --- |
| `200` | The request worked |
| `400` | The request was not valid |
| `401` | The request needs permission |
| `404` | The thing you requested was not found |
| `500` | The server had a problem |

The second part is the body.

For today's API, the body is JSON text.

JSON text is not quite Python yet.

This is JSON text:

```json
{
    "name": "Tokyo",
    "latitude": 35.6895,
    "longitude": 139.6917
}
```

After `json.loads()`, Python turns it into a dictionary:

```python
import json

json_text = '{"name": "Tokyo", "latitude": 35.6895, "longitude": 139.6917}'
place = json.loads(json_text)

print(place["name"])
print(place["latitude"])
print(place["longitude"])
```

You should see:

```text
Tokyo
35.6895
139.6917
```

The API may return more data than you need.

Your job is often to find the small useful piece inside a bigger response.

## Try It Yourself

Create a folder named:

```text
day-78
```

Then create a Python file named:

```text
day-78/find_place.py
```

Code:

```python
import json
from urllib.parse import urlencode
from urllib.request import urlopen

base_url = "https://geocoding-api.open-meteo.com/v1/search"

params = {
    "name": "Tokyo",
    "count": 1,
    "language": "en",
    "format": "json"
}

url = base_url + "?" + urlencode(params)

with urlopen(url, timeout=10) as response:
    status = response.status
    body = response.read().decode("utf-8")

print("Status:", status)

data = json.loads(body)

first_result = data["results"][0]

print("Name:", first_result["name"])
print("Country:", first_result["country"])
print("Latitude:", first_result["latitude"])
print("Longitude:", first_result["longitude"])
```

Run it.

If the request works, you should see a status of `200` and information about Tokyo.

The exact location details may vary a little over time because this data comes from a live service.

Now change:

```text
"name": "Tokyo"
```

to:

```text
"name": "Lagos"
```

Run it again.

Your code did not change much, but the data did.

That is the point of an API. You write one small tool, then ask it different questions.

Now try:

```text
"name": "New York"
```

Notice that you did not need to manually replace the space with `+`.

`urlencode()` handled that for you.

## Common Mistake

A common mistake is assuming the response always has the exact shape you hoped for.

This code works only if the API returns at least one result:

```python
first_result = data["results"][0]
```

If there are no matches, there may be no `"results"` key, or the list may be empty.

Try searching for something unlikely:

```python
params = {
    "name": "zzzzzzzzzzzz",
    "count": 1,
    "language": "en",
    "format": "json"
}
```

If you then run this:

```python
first_result = data["results"][0]
```

your program may crash with a `KeyError` or an `IndexError`.

A safer version checks first.

Fixed code:

```python
results = data.get("results", [])

if len(results) == 0:
    print("No matching place found.")
else:
    first_result = results[0]
    print(first_result["name"])
```

The API is not being rude.

It is answering your question with "I did not find anything."

Your program needs to know what to do with that answer.

## Debug It

Here is a version with a few mistakes.

Broken code:

```python
import json
from urllib.parse import urlencode
from urllib.request import urlopen

base_url = "https://geocoding-api.open-meteo.com/v1/search"

params = {
    "name": "Tokyo",
    "count": 1,
    "language": "en",
    "format": "json"
}

url = base_url + urlencode(params)

with urlopen(url, timeout=10) as response:
    body = response.read()

data = json.load(body)
first_result = data["result"][0]

print(first_result["name"])
```

Before you look at the fixed version, find three problems.

Hints:

- The base URL and query string need a separator.
- `response.read()` gives bytes.
- `json.load()` and `json.loads()` are different.
- The key is `"results"`, not `"result"`.

Fixed code:

```python
import json
from urllib.parse import urlencode
from urllib.request import urlopen

base_url = "https://geocoding-api.open-meteo.com/v1/search"

params = {
    "name": "Tokyo",
    "count": 1,
    "language": "en",
    "format": "json"
}

url = base_url + "?" + urlencode(params)

with urlopen(url, timeout=10) as response:
    body = response.read().decode("utf-8")

data = json.loads(body)
first_result = data["results"][0]

print(first_result["name"])
```

You should see:

```text
Tokyo
```

Here is the important difference:

```text
json.load(file_object) reads JSON from a file-like object.
json.loads(text) reads JSON from a string.
```

In this lesson, after decoding the response body, you have a string.

That is why you use `json.loads(body)`.

## Read the Docs

API documentation answers questions like:

```text
What URL do I use?
What parameters can I send?
Which parameters are required?
What does the response look like?
What errors can happen?
```

For the Open-Meteo geocoding API, the endpoint is:

```text
https://geocoding-api.open-meteo.com/v1/search
```

The useful parameters for today's example are:

| Parameter | Required | Meaning |
| --- | --- | --- |
| `name` | Yes | The place name to search for |
| `count` | No | How many matches to return |
| `language` | No | Which language to use for names |
| `format` | No | The response format |

The documentation also shows the general shape of a successful JSON response:

```json
{
    "results": [
        {
            "name": "Berlin",
            "latitude": 52.52437,
            "longitude": 13.41053,
            "country": "Germany"
        }
    ]
}
```

Do not memorize the whole response.

Read it with a question in mind.

For example:

```text
Where is the city name?
Where are latitude and longitude?
Is the result a dictionary or a list?
What happens when there are no results?
```

Those questions tell you how to write your Python.

Code:

```python
results = data.get("results", [])

if results:
    place = results[0]
    print(place["name"])
    print(place["latitude"])
    print(place["longitude"])
else:
    print("No place found.")
```

The docs do not replace testing.

They help you know what to test.

## Mini Challenge

Now use the first API request to feed a second API request.

The first request finds a place.

The second request asks for the current weather at that place.

Create a file named:

```text
day-78/weather_now.py
```

Code:

```python
import json
from urllib.parse import urlencode
from urllib.request import urlopen


def build_url(base_url, params):
    return base_url + "?" + urlencode(params)


def get_json(url):
    with urlopen(url, timeout=10) as response:
        body = response.read().decode("utf-8")

    return json.loads(body)


geocoding_url = build_url(
    "https://geocoding-api.open-meteo.com/v1/search",
    {
        "name": "Tokyo",
        "count": 1,
        "language": "en",
        "format": "json"
    }
)

place_data = get_json(geocoding_url)
results = place_data.get("results", [])

if len(results) == 0:
    print("No matching place found.")
else:
    place = results[0]

    forecast_url = build_url(
        "https://api.open-meteo.com/v1/forecast",
        {
            "latitude": place["latitude"],
            "longitude": place["longitude"],
            "current": "temperature_2m,wind_speed_10m",
            "timezone": "auto"
        }
    )

    forecast_data = get_json(forecast_url)
    current = forecast_data["current"]
    units = forecast_data["current_units"]

    temperature = current["temperature_2m"]
    temperature_unit = units["temperature_2m"]
    wind_speed = current["wind_speed_10m"]
    wind_unit = units["wind_speed_10m"]

    print(place["name"] + ", " + place["country"])
    print("Temperature:", temperature, temperature_unit)
    print("Wind speed:", wind_speed, wind_unit)
```

Run it.

If the requests work, you should see the place name and current weather values.

This program has a common API shape:

```text
Ask API A for an ID, coordinate, or search result.
Use that value to ask API B for details.
```

You will see this pattern in many real projects.

## Real-World Use

External APIs are how programs talk to services they do not own.

You might use an API to:

- show weather in a travel app
- look up book information by ISBN
- fetch public transit arrival times
- read a GitHub repository's public details
- send a message through a notification service
- convert one currency to another
- search a public dataset

The basic steps are the same:

```text
Build a URL.
Send a request.
Check what came back.
Parse the response.
Use only the fields your program needs.
Handle failure.
```

The last step matters.

File programs can fail when a file is missing.

API programs can fail when:

- the internet connection is down
- the server is slow
- the server is unavailable
- the URL is wrong
- a parameter is missing
- the response is not JSON
- the response shape changed
- your code asked for a field that is not present

Good API code does not assume the outside world is always ready.

It gives the user a clear message and stops cleanly when it cannot continue.

Here is a more careful version of `get_json()`.

Code:

```python
import json
from urllib.error import HTTPError, URLError
from urllib.request import urlopen


def get_json(url):
    try:
        with urlopen(url, timeout=10) as response:
            status = response.status
            body = response.read().decode("utf-8")

        if status != 200:
            print("Request failed with status:", status)
            return None

        return json.loads(body)

    except HTTPError as error:
        print("The server rejected the request.")
        print("Status:", error.code)
        return None

    except URLError:
        print("Could not reach the server.")
        return None

    except TimeoutError:
        print("The request took too long.")
        return None

    except json.JSONDecodeError:
        print("The response was not valid JSON.")
        return None
```

This function returns a dictionary when everything works.

It returns `None` when something recoverable goes wrong.

That gives the rest of your program a simple check:

```python
data = get_json(url)

if data is None:
    print("Could not load API data.")
else:
    print("API data loaded.")
```

## Recap

Today you used Python to request data from an external API.

You learned that a URL can include query parameters:

```text
base URL + ? + encoded parameters
```

You used:

```python
urlencode(params)
```

to build query strings safely.

You used:

```python
urlopen(url, timeout=10)
```

to send a request.

You used:

```python
response.read().decode("utf-8")
```

to turn response bytes into text.

You used:

```python
json.loads(body)
```

to turn JSON text into Python data.

And you practiced checking for missing data before reaching inside nested dictionaries and lists.

That combination is enough to read many public JSON APIs.

## Lesson Checklist

Before you move on, make sure you can:

- identify the base URL in an API request
- identify query parameters in a URL
- build a query string with `urlencode()`
- explain why spaces need URL encoding
- use `urlopen()` for a simple GET request
- set a timeout on a network request
- read and decode a response body
- parse JSON with `json.loads()`
- extract values from a nested dictionary and list
- check for an empty result list
- explain what status `200` usually means
- handle `HTTPError`, `URLError`, `TimeoutError`, and `JSONDecodeError`
- explain why live API data can vary

## Exercises

### Exercise 1: Build Three URLs

Write a small program that builds geocoding URLs for three cities.

Use this list:

```python
cities = ["Tokyo", "New York", "Lagos"]
```

Print one URL per city.

Use `urlencode()`, not manual string replacement.

### Exercise 2: Parse A Saved Response

This exercise does not need the internet.

Code:

```python
import json

sample_response = """
{
    "results": [
        {
            "name": "Tokyo",
            "country": "Japan",
            "latitude": 35.6895,
            "longitude": 139.6917
        }
    ]
}
"""

data = json.loads(sample_response)
place = data["results"][0]

print(place["name"])
print(place["country"])
print(place["latitude"])
print(place["longitude"])
```

Run it.

Then change the sample city details and run it again.

### Exercise 3: Handle No Results

Start with this data:

```python
data = {}
```

Write code that prints:

```text
No matching place found.
```

when the `"results"` key is missing.

Then try:

```python
data = {"results": []}
```

Your code should still print the same message.

### Exercise 4: Read Current Weather From Sample JSON

This exercise does not need the internet.

Code:

```python
import json

sample_response = """
{
    "current": {
        "time": "2026-05-10T12:00",
        "temperature_2m": 24.5,
        "wind_speed_10m": 11.2
    },
    "current_units": {
        "temperature_2m": "degrees C",
        "wind_speed_10m": "km/h"
    }
}
"""

data = json.loads(sample_response)
current = data["current"]
units = data["current_units"]

print("Temperature:", current["temperature_2m"], units["temperature_2m"])
print("Wind speed:", current["wind_speed_10m"], units["wind_speed_10m"])
```

Run it.

Then add one more field to the sample JSON and print it.

### Exercise 5: Add A Safer Getter

Write this function:

```python
def first_result(data):
    results = data.get("results", [])

    if len(results) == 0:
        return None

    return results[0]
```

Test it with:

```python
print(first_result({}))
print(first_result({"results": []}))
print(first_result({"results": [{"name": "Tokyo"}]}))
```

The first two should return `None`.

The last one should return the dictionary for Tokyo.

### Exercise 6: Catch Bad JSON

Run this:

```python
import json

bad_json = "{name: Tokyo}"

try:
    data = json.loads(bad_json)
    print(data)
except json.JSONDecodeError:
    print("That text was not valid JSON.")
```

Then fix `bad_json` so the parsing works.

Remember that JSON keys and string values need double quotes.

### Exercise 7: Check A Status Value

You do not need a live request for this one.

Code:

```python
status = 200

if status == 200:
    print("Request worked.")
else:
    print("Request failed with status:", status)
```

Try these values:

```text
200
400
404
500
```

Write down what your program prints for each one.

### Exercise 8: Make The City Search Reusable

Write a function named `build_geocoding_url(city)` that returns a full geocoding URL.

It should use:

```python
urlencode()
```

Test it with:

```python
print(build_geocoding_url("Tokyo"))
print(build_geocoding_url("New York"))
print(build_geocoding_url("Cape Town"))
```

### Exercise 9: Explain The Flow

In your own words, write one sentence for each step:

```text
Build the URL:
Send the request:
Decode the body:
Parse the JSON:
Extract the fields:
Handle failure:
```

Keep the sentences simple.

If you can explain the flow, you are much less likely to get lost in API code.

### Exercise 10: Combine The Pieces

Create a small program that:

- asks the user for a city name
- builds a geocoding URL
- requests data from the API
- handles network and JSON errors
- prints the first matching city, country, latitude, and longitude
- prints a clear message if nothing is found

Keep it small.

Do not add weather yet unless the city search works.

## Tiny Win

You made Python talk to a program outside your computer.

That is a real step.

You now know the full path from URL to response to JSON to Python values.

You also practiced the careful part: checking what came back before you trust it.

That habit matters more than memorizing one specific API.

## Tomorrow

Tomorrow is:

```text
Day 79: API Practice And Cleanup
```

Today you focused on the mechanics of one external API request.

Tomorrow you will practice turning that code into cleaner helper functions, keeping user-facing messages separate from data-fetching code, and making a small API program easier to test.
