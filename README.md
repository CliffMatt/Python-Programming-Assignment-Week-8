# Python-Programming-Assignment-Week-8
Assignment
import requests

def get_weather(city, api_key):
    """
    Fetches weather information for a given city using the OpenWeatherMap API.
    """
    base_url = "http://api.openweathermap.org/data/2.5/weather"
    params = {
        "q": city,
        "appid": api_key,
        "units": "metric"  # Use 'metric' for Celsius, 'imperial' for Fahrenheit
    }

    try:
        # Make the API call
        response = requests.get(base_url, params=params)
        response.raise_for_status()  # Raise an exception for HTTP errors

        # Parse the JSON response
        data = response.json()
        weather = {
            "city": data["name"],
            "temperature": data["main"]["temp"],
            "humidity": data["main"]["humidity"],
            "description": data["weather"][0]["description"],
        }

        return weather

    except requests.exceptions.RequestException as e:
        return f"Error fetching weather data: {e}"

def main():
    """
    Main function to run the weather application.
    """
    # Replace 'your_api_key' with your actual API key
    api_key = "your_api_key"

    print("Welcome to the Weather Application!")
    city = input("Enter the name of the city: ")

    weather = get_weather(city, api_key)

    if isinstance(weather, dict):
        print(f"\nWeather in {weather['city']}:")
        print(f"Temperature: {weather['temperature']}°C")
        print(f"Humidity: {weather['humidity']}%")
        print(f"Description: {weather['description'].capitalize()}")
    else:
        print(weather)

if __name__ == "__main__":
    main()
