import requests
import json

def get_weather(city, api_key):
    base_url = "(link unavailable)"
    params = {
        "q": city,
        "appid": api_key,
        "units": "metric"
    }
    response = requests.get(base_url, params=params)
    weather_data = response.json()
    return weather_data

def main():
    api_key = "YOUR_API_KEY"
    city = input("Enter city name: ")
    weather_data = get_weather(city, api_key)
    print("Weather in", city)
    print("Description:", weather_data["weather"][0]["description"])
    print("Temperature:", weather_data["main"]["temp"], "°C")
    print("Humidity:", weather_data["main"]["humidity"], "%")
    print("Wind Speed:", weather_data["wind"]["speed"], "m/s")
