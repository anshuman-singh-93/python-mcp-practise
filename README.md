# Weather MCP Server

A Model Context Protocol (MCP) server that provides weather information using the National Weather Service (NWS) API.

## Features

This MCP server exposes two tools for accessing weather data:

- **get_alerts**: Retrieve active weather alerts for any US state
- **get_forecast**: Get detailed weather forecasts for specific coordinates

## Installation

This project uses `uv` for dependency management. Install dependencies with:

```bash
uv sync
```

## Usage

Run the MCP server:

```bash
uv run weather.py
```

The server runs using stdio transport and can be integrated with any MCP-compatible client.

## Tools

### get_alerts(state: str)

Get active weather alerts for a US state.

**Parameters:**
- `state`: Two-letter US state code (e.g., "CA", "NY", "TX")

**Returns:** Formatted string containing active alerts with event type, affected area, severity, description, and instructions.

### get_forecast(latitude: float, longitude: float)

Get weather forecast for a specific location.

**Parameters:**
- `latitude`: Latitude coordinate
- `longitude`: Longitude coordinate

**Returns:** Formatted forecast for the next 5 periods including temperature, wind conditions, and detailed forecast.

## MCP Client Configuration

Add this server to your MCP client configuration:

```json
{
  "mcpServers": {
    "weather": {
      "command": "uv",
      "args": ["run", "weather.py"],
      "cwd": "/path/to/python-mcp"
    }
  }
}
```

## Data Source

All weather data is provided by the National Weather Service API (weather.gov), which covers US locations only.

## Requirements

- Python >= 3.14
- httpx >= 0.28.1
- mcp[cli] >= 1.25.0
