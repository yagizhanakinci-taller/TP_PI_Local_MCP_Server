# Weather, Countries & Holidays MCP Server

A local [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) server that provides live weather, country, and public holiday data with AI-formatted visual output.

## Features

- **Weather** — current conditions + 7-day forecast for any city (via [Open-Meteo](https://open-meteo.com/))
- **Country info** — population, area, capital, languages, currencies, Gini index, and more (via [REST Countries](https://restcountries.com/))
- **Location overview** — combined weather + country data in one call
- **Public holidays** — full holiday list with monthly distribution (via [Nager.Date](https://date.nager.at/))
- **AI formatting** — raw data is passed to Google AI Studio (Gemini) which returns rich markdown with tables and charts

## Tools

| Tool | Description |
|------|-------------|
| `get_weather` | Current conditions and 7-day forecast for a city |
| `get_country_info` | Demographics, geography, and economic data for a country |
| `get_location_overview` | Combined weather + country profile |
| `get_holidays` | Public holidays for a country and year (ISO 3166-1 alpha-2 code) |

## Setup

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Configure environment variables

Copy `.env.example` to `.env` and fill in your keys:

```bash
cp .env.example .env
```

| Variable | Required | Description |
|----------|----------|-------------|
| `GOOGLE_AI_STUDIO_API_KEY` | Yes | [Google AI Studio](https://aistudio.google.com/app/apikey) API key |
| `GOOGLE_AI_MODEL` | No | Model to use (default: `gemini-2.5-flash-lite`) |

### 3. Register with Claude Desktop

Add this server to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "weather-countries-holidays": {
      "command": "path/to/python.exe",
      "args": ["path/to/server_v4.py"]
    }
  }
}
```

On Windows the config file is typically at:
`%APPDATA%\Claude\claude_desktop_config.json`

### 4. Run manually (optional)

```bash
python server_v4.py
```

## External APIs Used

All APIs are free and require no authentication except Google AI Studio.

| API | Purpose | Auth |
|-----|---------|------|
| [Open-Meteo Geocoding](https://geocoding-api.open-meteo.com/) | City → coordinates | None |
| [Open-Meteo Forecast](https://api.open-meteo.com/) | Weather data | None |
| [REST Countries](https://restcountries.com/) | Country profiles | None |
| [Nager.Date](https://date.nager.at/) | Public holidays | None |
| [Google AI Studio](https://aistudio.google.com/) | Data formatting | API key |
