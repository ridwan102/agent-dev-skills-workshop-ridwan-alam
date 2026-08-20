# Agent Development Skills Workshop - Ridwan Alam

Google Partner Development Sprint - Gemini Enterprise & Agentic AI Case Studies

## Challenge 1: Weather Agent with Custom Tools

This repository contains a weather agent built using the Google Agent Development Kit (ADK) that provides real-time weather information and alerts for US locations.

### Features

- **Real-time Weather Data**: Uses the National Weather Service API to retrieve current conditions and forecasts
- **Location Geocoding**: Converts city names and addresses to coordinates using Google Maps API
- **Weather Alerts**: Automatically identifies and reports extreme weather conditions
- **Multi-Provider Support**: Works with both Google Gemini and Anthropic Claude models
- **Comprehensive Testing**: Includes unit tests and integration tests for multiple US cities

### Project Structure

```
.
├── weather_agent.ipynb    # Main Jupyter notebook with agent implementation
├── requirements.txt       # Python dependencies
└── README.md             # This file
```

### Setup Instructions

#### 1. Cloud Skills Boost Environment

Log into your Cloud Skills Boost environment:
- **URL**: https://console.cloud.google.com/
- **Username**: student-00-025db6bd4eb5@qwiklabs.net
- **Password**: GcxM053Rw6Gh
- **Project**: qwiklabs-gcp-02-138827e82db5

#### 2. Create Colab Enterprise Notebook

1. Navigate to **Vertex AI** > **Workbench** in Google Cloud Console
2. Create a new **Colab Enterprise** notebook
3. Upload the `weather_agent.ipynb` file

#### 3. Configure API Keys

Set the following environment variables in your notebook:

```python
import os

# Google Cloud API Key (for Gemini)
os.environ['GOOGLE_API_KEY'] = 'your-google-api-key'

# Google Maps API Key (optional, for geocoding)
os.environ['GOOGLE_MAPS_API_KEY'] = 'your-maps-api-key'

# Anthropic API Key (optional, for Claude support)
os.environ['ANTHROPIC_API_KEY'] = 'your-anthropic-api-key'
```

#### 4. Install Dependencies

Run the first cell in the notebook to install required packages:

```bash
pip install google-genai anthropic requests google-adk -q
```

### Usage

#### Running the Weather Agent

```python
# Using Gemini
response = run_weather_agent("What's the weather in San Francisco?", provider='gemini')
print(response)

# Using Claude
response = run_weather_agent("What's the weather in New York?", provider='claude')
print(response)
```

#### Running Tests

Execute the test suite for multiple cities:

```python
# Test with Gemini
gemini_results = run_test_suite(provider='gemini')

# Test with Claude
claude_results = run_test_suite(provider='claude')
```

#### Running Unit Tests

```python
# Run the unit test cell in the notebook
suite = unittest.TestLoader().loadTestsFromTestCase(TestWeatherTools)
runner = unittest.TextTestRunner(verbosity=2)
test_results = runner.run(suite)
```

### Tools Implementation

#### 1. National Weather Service API

```python
def get_weather_by_coordinates(latitude: float, longitude: float) -> Dict[str, Any]:
    """
    Retrieve current weather data from the National Weather Service API.

    Args:
        latitude: The latitude coordinate (decimal degrees)
        longitude: The longitude coordinate (decimal degrees)

    Returns:
        Dictionary containing weather data including temperature, conditions,
        wind speed, and detailed forecast
    """
```

#### 2. Google Maps Geocoding API

```python
def geocode_location(location: str, api_key: Optional[str] = None) -> Dict[str, Any]:
    """
    Convert a location name or address to latitude and longitude coordinates.

    Args:
        location: The address or place name to geocode
        api_key: Optional Google Maps API key

    Returns:
        Dictionary containing latitude, longitude, and formatted address
    """
```

### Agent Capabilities

The weather agent can:

1. **Convert Locations**: Transform city names into geographic coordinates
2. **Fetch Weather Data**: Retrieve current conditions and forecasts
3. **Identify Alerts**: Detect extreme temperatures, storms, and high winds
4. **Provide Summaries**: Generate user-friendly weather reports

### Testing

The notebook includes comprehensive tests:

- **Unit Tests**: Test individual functions with various inputs
- **Integration Tests**: Test the full agent workflow across 5 US cities:
  - San Francisco, CA
  - New York City, NY
  - Chicago, IL
  - Miami, FL
  - Seattle, WA

### PEP 8 Compliance

All functions follow Python PEP 8 style guidelines:
- Type hints for all parameters and return values
- Comprehensive docstrings with Args, Returns, and Examples
- Clear error handling and status reporting

### Multi-Provider Architecture

The agent supports multiple LLM providers through a unified interface:

- **Gemini**: Uses Google's genai client with `gemini-2.0-flash-exp` model
- **Claude**: Uses Anthropic's client with `claude-3-5-sonnet-20241022` model

Both providers share the same tools and instructions, ensuring consistent behavior.

### Example Output

```
Using GEMINI model
Query: What's the weather like in San Francisco, CA?
======================================================================

🔧 Calling function: geocode_location
   Arguments: {'location': 'San Francisco, CA'}
   Result: {'status': 'success', 'latitude': 37.7749, 'longitude': -122.4194, ...}

🔧 Calling function: get_weather_by_coordinates
   Arguments: {'latitude': 37.7749, 'longitude': -122.4194}
   Result: {'status': 'success', 'temperature': 62, 'conditions': 'Partly Cloudy', ...}

Response:
The weather in San Francisco, CA is currently partly cloudy with a temperature
of 62°F. Winds are light from the west at 5-10 mph. No weather alerts at this time.
```

### License

This project is part of the Google Partner Development Sprint educational program.

### Author

Ridwan Alam
