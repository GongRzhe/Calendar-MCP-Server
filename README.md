# Calendar MCP Server

A Model Context Protocol (MCP) server for Google Calendar integration in Claude Desktop. This server enables AI assistants to manage Google Calendar events through natural language interactions.

![](https://badge.mcpx.dev?type=server 'MCP Server')
[![smithery badge](https://smithery.ai/badge/@gongrzhe/server-calendar-mcp)](https://smithery.ai/server/@gongrzhe/server-calendar-mcp)
[![npm version](https://badge.fury.io/js/%40gongrzhe%2Fserver-calendar-mcp.svg)](https://www.npmjs.com/package/@gongrzhe/server-calendar-mcp)
[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](https://opensource.org/licenses/ISC)

## Features

- Create calendar events with title, time, description, and location
- Retrieve event details by event ID
- Update existing events (title, time, description, location)
- Delete events
- List events within a specified time range
- Full integration with Google Calendar API
- Secure OAuth2 authentication

## Installation

### Installing via Smithery

To install Google Calendar Integration for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@gongrzhe/server-calendar-mcp):

```bash
npx -y @smithery/cli install @gongrzhe/server-calendar-mcp --client claude
```

### Manual Installation
```bash
npm install @gongrzhe/server-calendar-mcp
```

## Setup

1. Create a Google Cloud Project and obtain credentials:

   a. Create a Google Cloud Project:
      - Go to [Google Cloud Console](https://console.cloud.google.com/)
      - Create a new project or select an existing one
      - Enable the Google Calendar API for your project

   b. Create OAuth 2.0 Credentials:
      - Go to "APIs & Services" > "Credentials"
      - Click "Create Credentials" > "OAuth client ID"
      - Choose "Desktop app" as application type
      - Give it a name and click "Create"
      - You will get your `GOOGLE_CLIENT_ID` and `GOOGLE_CLIENT_SECRET`

   c. Get Refresh Token:
      - Go to [OAuth 2.0 Playground](https://developers.google.com/oauthplayground/)
      - Click the gear icon (Settings) in the top right
      - Check "Use your own OAuth credentials"
      - Enter your OAuth Client ID and Client Secret
      - In the left panel, find "Calendar API v3" and select "https://www.googleapis.com/auth/calendar"
      - Click "Authorize APIs" and complete the OAuth flow
      - Click "Exchange authorization code for tokens"
      - Copy the "Refresh token" - this is your `GOOGLE_REFRESH_TOKEN`

2. Configure in Claude Desktop:

```json
{
  "calendar": {
    "command": "npx",
    "args": [
      "@gongrzhe/server-calendar-mcp"
    ],
    "env": {
      "GOOGLE_CLIENT_ID": "your_client_id_here",
      "GOOGLE_CLIENT_SECRET": "your_client_secret_here",
      "GOOGLE_REFRESH_TOKEN": "your_refresh_token_here"
    }
  }
}
```

## Usage Examples

The server provides several tools that can be used through the Claude Desktop:

### Create Event
```json
{
  "summary": "Team Meeting",
  "start": {
    "dateTime": "2024-01-20T10:00:00Z"
  },
  "end": {
    "dateTime": "2024-01-20T11:00:00Z"
  },
  "description": "Weekly team sync",
  "location": "Conference Room A"
}
```

### List Events
```json
{
  "timeMin": "2024-01-01T00:00:00Z",
  "timeMax": "2024-12-31T23:59:59Z",
  "maxResults": 10,
  "orderBy": "startTime"
}
```

### Update Event
```json
{
  "eventId": "event123",
  "summary": "Updated Meeting Title",
  "start": {
    "dateTime": "2024-01-20T11:00:00Z"
  },
  "end": {
    "dateTime": "2024-01-20T12:00:00Z"
  }
}
```

### Delete Event
```json
{
  "eventId": "event123"
}
```

## Security Notes

- Keep your Google API credentials secure
- Regularly rotate your refresh tokens
- Store sensitive information in Claude Desktop configuration
- Never share or commit your credentials to version control
- The refresh token gives access to your Google Calendar, treat it like a password

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the ISC License.

## Author

gongrzhe

## Support

If you encounter any issues or have questions, please file an issue on the GitHub repository.
