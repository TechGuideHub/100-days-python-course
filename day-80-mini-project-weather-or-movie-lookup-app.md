# Day 80: Mini Project: Weather Lookup App

**Focus:** Building a small command-line app that gets live weather data  
**You will practice:** `urllib.request`, `urllib.parse`, `json`, functions, nested dictionaries, lists, error handling, and saving a JSON result  
**Estimated time:** 70-90 minutes

## Today's Goal

Today you will build a weather lookup app.

The app will ask for a city, find that city's latitude and longitude, request a short forecast, and print a clean summary.

You will use:

- the Python standard library
- Open-Meteo's geocoding API
- Open-Meteo's forecast API
- JSON parsing
- `try` and `except`
- a small optional cache file

By the end of the lesson, you should be able to:

- turn user input into a web request
- build a URL with query parameters
- read JSON from a web response
- pull useful values from nested data
- split a program into helper functions
- show a friendly message when something goes wrong
- save the last result to a JSON file

This is a project day, so the goal is not to memorize every line.

The goal is to connect the pieces you already know into one useful program.

## The Big Idea

A weather app is mostly a conversation between your program and another service.

Your program asks:

```text
What place did the learner type?
```

The geocoding API answers:

```text
Here are coordinates for that place.
```

Then your program asks:

```text
What is the weather at these coordinates?
```

The forecast API answers with JSON.

Your job is to turn that JSON into something a person can read.

That means this project has five main jobs:

```text
input -> geocode -> forecast -> parse -> display
```

Then you will add one optional job:

```text
save the last result
```

## The Mental Model

When you use a web API, you usually send a URL with extra details attached.

Those extra details are called query parameters.

This URL:

```text
https://geocoding-api.open-meteo.com/v1/search?name=Tokyo&count=1
```

means:

```text
Use the geocoding search endpoint.
Look for Tokyo.
Return one matching result.
```

In Python, do not build query strings by gluing text together by hand.

Use `urllib.parse.urlencode()` so spaces and special characters are handled correctly.

For example, this city:

```text
New York
```

needs to become safe for a URL.

Python can do that for you.

The other mental model is nested data.

An API response might come back shaped like this:

```text
dictionary
    results
        list
            dictionary
                name
                latitude
                longitude
```

That means you often read API data one level at a time:

```python
results = data.get("results", [])
first_result = results[0]
latitude = first_result["latitude"]
```

Slow, clear steps beat clever one-line code here.

## The Project

Create a folder named:

```text
day-80
```

Inside that folder, create this file:

```text
day-80/weather_lookup.py
```

Your finished app will:

1. Ask the user for a city.
2. Find the first matching location.
3. Request current weather and today's high, low, and rain chance.
4. Translate the weather code into a readable phrase.
5. Print a short weather report.
6. Handle common errors without a scary crash.
7. Optionally save the last report to:

```text
day-80/last_weather.json
```

Open-Meteo does not require an API key for this beginner project.

That keeps the focus on Python instead of account setup.

## Step-by-Step Build

Build this project in small pieces.

Do not paste the final code first if you want the most practice. Type each step, run often, and let mistakes teach you where the data is moving.

### Step 1: Import The Tools

Start with the modules you need.

```python
import json
from pathlib import Path
from urllib.error import HTTPError, URLError
from urllib.parse import urlencode
from urllib.request import urlopen
```

These are all from the standard library.

You do not need to install anything.

### Step 2: Store The API Endpoints

Add constants for the two web addresses your app will use.

```python
GEOCODING_URL = "https://geocoding-api.open-meteo.com/v1/search"
FORECAST_URL = "https://api.open-meteo.com/v1/forecast"
SAVE_PATH = Path("day-80/last_weather.json")
```

The geocoding endpoint turns a city name into coordinates.

The forecast endpoint turns coordinates into weather data.

### Step 3: Build A JSON Request Helper

Many API programs need the same small routine:

```text
build the URL
open it
read text
turn JSON text into Python data
```

Write one helper for that.

```python
def get_json(url, params):
    query_string = urlencode(params)
    full_url = f"{url}?{query_string}"

    with urlopen(full_url, timeout=10) as response:
        body = response.read().decode("utf-8")

    return json.loads(body)
```

This function returns a Python dictionary or list, depending on the JSON response.

Later you will add error handling around it.

### Step 4: Geocode The City

Now write a function that searches for a city and returns the first match.

```python
def find_city(city_name):
    data = get_json(GEOCODING_URL, {
        "name": city_name,
        "count": 1,
        "language": "en",
        "format": "json"
    })

    results = data.get("results", [])

    if not results:
        raise ValueError(f"No location found for {city_name}.")

    return results[0]
```

Notice the guard:

```python
if not results:
```

That protects your program from trying to read `results[0]` when the list is empty.

### Step 5: Fetch The Forecast

Once you have latitude and longitude, you can ask for weather.

```python
def get_forecast(location):
    return get_json(FORECAST_URL, {
        "latitude": location["latitude"],
        "longitude": location["longitude"],
        "current": "temperature_2m,relative_humidity_2m,weather_code,wind_speed_10m",
        "daily": "temperature_2m_max,temperature_2m_min,precipitation_probability_max",
        "timezone": "auto",
        "forecast_days": 1
    })
```

This asks for only the values this app needs.

That makes the response easier to inspect.

### Step 6: Translate Weather Codes

Weather APIs often return compact codes.

People prefer words.

Add this helper:

```python
def describe_weather_code(code):
    descriptions = {
        0: "Clear sky",
        1: "Mainly clear",
        2: "Partly cloudy",
        3: "Overcast",
        45: "Fog",
        48: "Depositing rime fog",
        51: "Light drizzle",
        53: "Moderate drizzle",
        55: "Dense drizzle",
        61: "Slight rain",
        63: "Moderate rain",
        65: "Heavy rain",
        71: "Slight snow",
        73: "Moderate snow",
        75: "Heavy snow",
        80: "Slight rain showers",
        81: "Moderate rain showers",
        82: "Violent rain showers",
        95: "Thunderstorm"
    }

    return descriptions.get(code, f"Unknown weather code {code}")
```

You do not need every possible code for the first version.

You can add more later.

### Step 7: Format The Location Name

The geocoding result may include city, region, and country.

This helper keeps the display neat:

```python
def format_location(location):
    parts = [
        location.get("name"),
        location.get("admin1"),
        location.get("country")
    ]

    return ", ".join(part for part in parts if part)
```

If `admin1` is missing, the function skips it.

### Step 8: Pull Out The Forecast Values

The forecast JSON has nested dictionaries.

This helper collects the values your app cares about into one smaller dictionary.

```python
def first_value(values, default="Not available"):
    if not values:
        return default

    return values[0]


def make_summary(location, forecast):
    current = forecast.get("current", {})
    current_units = forecast.get("current_units", {})
    daily = forecast.get("daily", {})
    daily_units = forecast.get("daily_units", {})

    if not current:
        raise ValueError("The forecast did not include current weather data.")

    weather_code = current.get("weather_code")

    return {
        "location": format_location(location),
        "time": current.get("time", "Unknown time"),
        "weather": describe_weather_code(weather_code),
        "temperature": current.get("temperature_2m", "Not available"),
        "temperature_unit": current_units.get("temperature_2m", "C"),
        "humidity": current.get("relative_humidity_2m", "Not available"),
        "humidity_unit": current_units.get("relative_humidity_2m", "%"),
        "wind_speed": current.get("wind_speed_10m", "Not available"),
        "wind_speed_unit": current_units.get("wind_speed_10m", "km/h"),
        "high": first_value(daily.get("temperature_2m_max")),
        "low": first_value(daily.get("temperature_2m_min")),
        "daily_temperature_unit": daily_units.get("temperature_2m_max", "C"),
        "rain_chance": first_value(daily.get("precipitation_probability_max")),
        "rain_chance_unit": daily_units.get("precipitation_probability_max", "%")
    }
```

The smaller `summary` dictionary is easier to print and easier to save.

### Step 9: Display The Summary

Now turn the summary into output for a human.

```python
def display_summary(summary):
    print()
    print(f"Weather for {summary['location']}")
    print(f"Time: {summary['time']}")
    print(f"Condition: {summary['weather']}")
    print(f"Temperature: {summary['temperature']} {summary['temperature_unit']}")
    print(f"Humidity: {summary['humidity']} {summary['humidity_unit']}")
    print(f"Wind: {summary['wind_speed']} {summary['wind_speed_unit']}")
    print(
        f"Today: high {summary['high']} {summary['daily_temperature_unit']}, "
        f"low {summary['low']} {summary['daily_temperature_unit']}"
    )
    print(f"Rain chance: {summary['rain_chance']} {summary['rain_chance_unit']}")
```

A sample run might look like this:

```text
City: Tokyo

Weather for Tokyo, Tokyo, Japan
Time: 2026-05-10T15:45
Condition: Partly cloudy
Temperature: 24.7 C
Humidity: 58 %
Wind: 12.1 km/h
Today: high 26.4 C, low 18.9 C
Rain chance: 10 %
```

Your numbers will be different because weather changes.

### Step 10: Save The Last Result

Add a helper that creates the folder if needed and saves the summary.

```python
def save_summary(summary):
    SAVE_PATH.parent.mkdir(parents=True, exist_ok=True)

    with SAVE_PATH.open("w", encoding="utf-8") as file:
        json.dump(summary, file, indent=4)
```

This creates:

```text
day-80/last_weather.json
```

Only if the user chooses to save.

### Step 11: Put The App Together

The `main()` function controls the app.

It asks for input, calls the helpers in order, and handles common failures.

```python
def main():
    city = input("City: ").strip()

    if not city:
        print("Please enter a city name.")
        return

    try:
        location = find_city(city)
        forecast = get_forecast(location)
        summary = make_summary(location, forecast)
        display_summary(summary)

        choice = input("\nSave this result? (y/n): ").strip().lower()

        if choice == "y":
            save_summary(summary)
            print(f"Saved to {SAVE_PATH}")

    except HTTPError as error:
        print(f"The weather service returned HTTP {error.code}.")
    except URLError:
        print("Could not reach the weather service. Check your internet connection.")
    except TimeoutError:
        print("The weather request took too long. Try again in a moment.")
    except json.JSONDecodeError:
        print("The weather service returned data that was not valid JSON.")
    except (KeyError, TypeError, ValueError) as error:
        print(f"Could not finish the lookup: {error}")
```

Finally, call `main()` only when the file is run directly.

```python
if __name__ == "__main__":
    main()
```

That pattern makes the helper functions easier to test later.

### Complete Final Code

Your full file should look like this:

```python
import json
from pathlib import Path
from urllib.error import HTTPError, URLError
from urllib.parse import urlencode
from urllib.request import urlopen


GEOCODING_URL = "https://geocoding-api.open-meteo.com/v1/search"
FORECAST_URL = "https://api.open-meteo.com/v1/forecast"
SAVE_PATH = Path("day-80/last_weather.json")


def get_json(url, params):
    query_string = urlencode(params)
    full_url = f"{url}?{query_string}"

    with urlopen(full_url, timeout=10) as response:
        body = response.read().decode("utf-8")

    return json.loads(body)


def find_city(city_name):
    data = get_json(GEOCODING_URL, {
        "name": city_name,
        "count": 1,
        "language": "en",
        "format": "json"
    })

    results = data.get("results", [])

    if not results:
        raise ValueError(f"No location found for {city_name}.")

    return results[0]


def get_forecast(location):
    return get_json(FORECAST_URL, {
        "latitude": location["latitude"],
        "longitude": location["longitude"],
        "current": "temperature_2m,relative_humidity_2m,weather_code,wind_speed_10m",
        "daily": "temperature_2m_max,temperature_2m_min,precipitation_probability_max",
        "timezone": "auto",
        "forecast_days": 1
    })


def describe_weather_code(code):
    descriptions = {
        0: "Clear sky",
        1: "Mainly clear",
        2: "Partly cloudy",
        3: "Overcast",
        45: "Fog",
        48: "Depositing rime fog",
        51: "Light drizzle",
        53: "Moderate drizzle",
        55: "Dense drizzle",
        61: "Slight rain",
        63: "Moderate rain",
        65: "Heavy rain",
        71: "Slight snow",
        73: "Moderate snow",
        75: "Heavy snow",
        80: "Slight rain showers",
        81: "Moderate rain showers",
        82: "Violent rain showers",
        95: "Thunderstorm"
    }

    return descriptions.get(code, f"Unknown weather code {code}")


def format_location(location):
    parts = [
        location.get("name"),
        location.get("admin1"),
        location.get("country")
    ]

    return ", ".join(part for part in parts if part)


def first_value(values, default="Not available"):
    if not values:
        return default

    return values[0]


def make_summary(location, forecast):
    current = forecast.get("current", {})
    current_units = forecast.get("current_units", {})
    daily = forecast.get("daily", {})
    daily_units = forecast.get("daily_units", {})

    if not current:
        raise ValueError("The forecast did not include current weather data.")

    weather_code = current.get("weather_code")

    return {
        "location": format_location(location),
        "time": current.get("time", "Unknown time"),
        "weather": describe_weather_code(weather_code),
        "temperature": current.get("temperature_2m", "Not available"),
        "temperature_unit": current_units.get("temperature_2m", "C"),
        "humidity": current.get("relative_humidity_2m", "Not available"),
        "humidity_unit": current_units.get("relative_humidity_2m", "%"),
        "wind_speed": current.get("wind_speed_10m", "Not available"),
        "wind_speed_unit": current_units.get("wind_speed_10m", "km/h"),
        "high": first_value(daily.get("temperature_2m_max")),
        "low": first_value(daily.get("temperature_2m_min")),
        "daily_temperature_unit": daily_units.get("temperature_2m_max", "C"),
        "rain_chance": first_value(daily.get("precipitation_probability_max")),
        "rain_chance_unit": daily_units.get("precipitation_probability_max", "%")
    }


def display_summary(summary):
    print()
    print(f"Weather for {summary['location']}")
    print(f"Time: {summary['time']}")
    print(f"Condition: {summary['weather']}")
    print(f"Temperature: {summary['temperature']} {summary['temperature_unit']}")
    print(f"Humidity: {summary['humidity']} {summary['humidity_unit']}")
    print(f"Wind: {summary['wind_speed']} {summary['wind_speed_unit']}")
    print(
        f"Today: high {summary['high']} {summary['daily_temperature_unit']}, "
        f"low {summary['low']} {summary['daily_temperature_unit']}"
    )
    print(f"Rain chance: {summary['rain_chance']} {summary['rain_chance_unit']}")


def save_summary(summary):
    SAVE_PATH.parent.mkdir(parents=True, exist_ok=True)

    with SAVE_PATH.open("w", encoding="utf-8") as file:
        json.dump(summary, file, indent=4)


def main():
    city = input("City: ").strip()

    if not city:
        print("Please enter a city name.")
        return

    try:
        location = find_city(city)
        forecast = get_forecast(location)
        summary = make_summary(location, forecast)
        display_summary(summary)

        choice = input("\nSave this result? (y/n): ").strip().lower()

        if choice == "y":
            save_summary(summary)
            print(f"Saved to {SAVE_PATH}")

    except HTTPError as error:
        print(f"The weather service returned HTTP {error.code}.")
    except URLError:
        print("Could not reach the weather service. Check your internet connection.")
    except TimeoutError:
        print("The weather request took too long. Try again in a moment.")
    except json.JSONDecodeError:
        print("The weather service returned data that was not valid JSON.")
    except (KeyError, TypeError, ValueError) as error:
        print(f"Could not finish the lookup: {error}")


if __name__ == "__main__":
    main()
```

## Try It Yourself

Run your app.

Try a city you know:

```text
London
```

Then try a city with two words:

```text
New York
```

Then try a city from another country:

```text
Nairobi
```

The exact numbers will change, but the shape of the output should stay the same:

```text
Weather for ...
Time: ...
Condition: ...
Temperature: ...
Humidity: ...
Wind: ...
Today: high ..., low ...
Rain chance: ...
```

If you choose to save, open this file:

```text
day-80/last_weather.json
```

You should see a JSON object with the same summary values.

## Common Mistake

A common mistake is treating every API response as if it always has the exact data you wanted.

For example:

```python
results = data["results"]
location = results[0]
```

That works when the API finds a city.

It fails when the API returns no matches.

This version is safer:

```python
results = data.get("results", [])

if not results:
    raise ValueError("No location found.")
```

Another common mistake is using the city name directly inside the URL.

This can break with spaces:

```text
New York
```

Use `urlencode()` instead.

It turns the parameters into a URL-safe query string.

## Debug It

Use this section when your app does not work the first time.

### Problem 1: The City Is Not Found

Try printing the raw geocoding data:

```python
data = get_json(GEOCODING_URL, {
    "name": city_name,
    "count": 1,
    "language": "en",
    "format": "json"
})

print(data)
```

If you see no `results`, the city search did not find a match.

Try a larger nearby city or check the spelling.

### Problem 2: The App Cannot Reach The Service

If you see:

```text
Could not reach the weather service. Check your internet connection.
```

Check whether your internet connection is working.

Then run the program again.

Network programs can fail even when your code is correct.

### Problem 3: A Key Is Missing

If you see a `KeyError`, print the part of the JSON you are reading.

For example:

```python
print(forecast.keys())
print(forecast.get("current"))
print(forecast.get("daily"))
```

That tells you whether the response has the shape you expected.

### Problem 4: The Output Says Not Available

This means your program did not crash, but one value was missing.

Look at the matching key in `make_summary()`.

For example:

```python
daily.get("temperature_2m_max")
```

Then compare that key with the API response.

One small spelling difference is enough to produce missing data.

## Read the Docs

When you read documentation for this project, do not try to understand every option.

Look for the option you need right now.

Start with these pages:

```text
https://docs.python.org/3/library/urllib.request.html
https://docs.python.org/3/library/urllib.parse.html
https://docs.python.org/3/library/json.html
https://open-meteo.com/en/docs/geocoding-api
https://open-meteo.com/en/docs
```

Useful things to look for:

- `urllib.request.urlopen()` opens a URL and gives you a response.
- `urllib.parse.urlencode()` turns a dictionary into query parameters.
- `json.loads()` turns JSON text into Python data.
- The geocoding API returns a `results` list.
- The forecast API accepts `latitude`, `longitude`, `current`, `daily`, and `timezone`.

Documentation is easier when you arrive with a question.

For example:

```text
What parameter asks for one city result?
What key contains latitude?
What current weather variable gives humidity?
```

Small questions make large docs manageable.

## Mini Challenge

Add one improvement.

Choose one:

1. Ask the user whether they want Celsius or Fahrenheit.
2. Show the latitude and longitude in the output.
3. Save the city the user typed along with the formatted location.
4. Add more weather code descriptions.
5. Let the user search again until they type `quit`.

For the temperature unit challenge, Open-Meteo accepts a parameter named:

```text
temperature_unit
```

Try adding it to the forecast request.

## Real-World Use

This project is small, but the pattern is real.

Many apps do the same kind of work:

```text
ask for input
call a service
parse JSON
handle bad responses
show only the useful parts
save a small result
```

Weather apps, movie apps, package trackers, recipe search tools, map tools, and stock dashboards all use this shape.

The API changes, but the Python pattern stays familiar.

## Recap

Today you built a complete command-line weather lookup app.

You used a city name to get coordinates.

You used coordinates to get forecast data.

You parsed nested JSON into a smaller summary dictionary.

You printed output that a person can read.

You handled missing cities, network problems, slow requests, bad JSON, and missing data.

You also added an optional save step with `json.dump()`.

That is a lot of practical Python in one project.

## Lesson Checklist

Before you move on, make sure you can:

- explain why the app needs geocoding before weather lookup
- use `urlencode()` to build query parameters
- read JSON from a web response
- use `.get()` to handle missing keys more safely
- read values from a nested dictionary
- read the first item from a list safely
- use `try` and `except` around code that can fail
- save a dictionary to a JSON file
- run the finished app at least once

## Exercises

### Exercise 1: Inspect The Geocoding Data

Temporarily add this line inside `find_city()` after `data` is created:

```python
print(json.dumps(data, indent=4))
```

Run the program with:

```text
Paris
```

Find the keys for:

- city name
- country
- latitude
- longitude
- time zone

Remove the print when you are done.

### Exercise 2: Inspect The Forecast Data

Temporarily add this line after `forecast = get_forecast(location)`:

```python
print(json.dumps(forecast, indent=4))
```

Find these sections:

- `current`
- `current_units`
- `daily`
- `daily_units`

Remove the print when you are done.

### Exercise 3: Add Apparent Temperature

Apparent temperature means how the temperature feels to a person.

Add this current variable:

```text
apparent_temperature
```

Then update `make_summary()` and `display_summary()` so the app prints it.

### Exercise 4: Add A Second Day

Change:

```python
"forecast_days": 1
```

to:

```python
"forecast_days": 2
```

Print tomorrow's high and low.

Remember that daily values are lists, so tomorrow is at index `1`.

### Exercise 5: Make Saving Automatic

Remove the save question and save every successful lookup.

Then run the app twice with two different cities.

Open:

```text
day-80/last_weather.json
```

Notice that the second lookup replaces the first one.

That is what "last result" means.

### Exercise 6: Save A History List

Instead of replacing the previous lookup, save a list of lookups.

Use this file:

```text
day-80/weather_history.json
```

Hints:

- if the file does not exist, start with an empty list
- append the new summary
- write the whole list back to the file

### Exercise 7: Improve The Error Message

Change this:

```python
raise ValueError(f"No location found for {city_name}.")
```

to include a suggestion:

```text
Try checking the spelling or searching for a larger nearby city.
```

Then test it with a made-up city name.

### Exercise 8: Add More Weather Codes

Open the Open-Meteo weather code documentation and add at least five more codes to `describe_weather_code()`.

Test the function directly:

```python
print(describe_weather_code(0))
print(describe_weather_code(61))
print(describe_weather_code(999))
```

The last one should use the unknown-code fallback.

### Exercise 9: Repeat Until Quit

Wrap the main lookup in a loop.

The user should be able to search more than one city.

Stop when the user types:

```text
quit
```

Keep the error handling inside the loop so one failed lookup does not end the whole program.

### Exercise 10: Write A Small Test By Hand

You do not need a testing framework yet.

Create sample dictionaries directly in your file, then call `make_summary()` with them.

Use a fake location:

```python
sample_location = {
    "name": "Sample City",
    "admin1": "Sample Region",
    "country": "Sample Country"
}
```

Use a fake forecast with `current`, `current_units`, `daily`, and `daily_units`.

Print the summary.

This helps you test your parsing code without depending on the internet.

## Tiny Win

You built a program that talks to the outside world.

That is a big step.

Files, lists, dictionaries, functions, exceptions, and JSON now work together in one app.

You are no longer only writing tiny isolated examples.

You are building small tools.

## Tomorrow

Tomorrow you will keep practicing with programs that have more than one moving part.

The useful habit from today is to build in layers:

```text
get the data
check the shape
extract the useful pieces
show a clear result
handle the failures
```

That habit will follow you into larger projects.
