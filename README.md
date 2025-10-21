# opsera-mcp-server

# Opsera MCP Configuration Guide

This guide will walk you through the steps to configure your Opsera MCP (Model Context Protocol) server access in Cursor IDE.

## Prerequisites

- Access to Opsera Portal with valid login

## Configuration Steps

### Step 1: Access the Opsera Portal

1. Navigate to your Opsera portal
2. Log in with your credentials
3. Once logged in, you will see the Opsera home page

### Step 2: Navigate to Personal Access Tokens

![Profile and Access Tokens](./assets/profile.png)

1. Click on your profile icon in the top-right corner
2. From the dropdown menu, select **"Profile"**
3. You will land on the **"My Profile"** page
4. Click on the **"Access Tokens"** tab at the top of the page

### Step 3: Generate API Access Token

![Generate Personal Access Token](./assets/generate_token.png)

On the **"Access Tokens"** page, you will see the **"Generate Personal Access Token"** section.

Fill in the following fields:

#### Name
- Enter a descriptive name for your token (e.g., "MCP Integration")
- Spaces, letters, numbers, dashes, colons, underscores, and periods are allowed

#### Expires After
- Select the expiration period from the dropdown (default: 1 Month)
- Options typically include: 1 Month, 3 Months, 6 Months, 1 Year

#### Scope
- Select **"API Access"** (full read/write access)
- This grants complete read/write access to the API, including all Pipeline and Tool Registry routes based on individual resource access rules

#### Create Token
Click the **"Create"** button to create the token.

> **IMPORTANT:** Once generated, copy the token immediately!
> - The token will be displayed only once
> - It will be in JWT format (starting with "eyJ...")
> - Store it securely as you won't be able to see it again

### Step 4: Configure MCP in Cursor IDE

1. Locate your Cursor MCP configuration file:
   - **macOS/Linux:** `~/.cursor/mcp.json`
   - **Windows:** `%USERPROFILE%\.cursor\mcp.json`

2. Open the `mcp.json` file in a text editor

3. Add the Opsera MCP server configuration with your API key:

```json
{
  "mcpServers": {
    "opsera-ai-agent": {
      "url": "https://agent.opsera.io/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_TOKEN_HERE"
      }
    }
  }
}
```

4. Replace `"YOUR_API_TOKEN_HERE"` with the actual API token you copied in Step 3

5. Save the `mcp.json` file

### Step 5: Verify Configuration

1. Save the `mcp.json` file
2. The Opsera MCP server should now be available in your MCP tools list
3. You can verify the connection by checking if Opsera-related tools and functions appear in your available MCP functions

## Configuration Example

Complete example of `mcp.json` file:

```json
{
  "mcpServers": {
    "opsera-ai-agent": {
      "url": "https://agent.opsera.io/mcp",
      "headers": {
        "Authorization": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
      }
    }
  }
}
```

> **Note:** The token shown above is abbreviated. Your actual token will be much longer.

## Troubleshooting

### Authentication Error (401 Unauthorized)

- Verify your API token is correct and not expired
- Check if the token has the required scopes/permissions (should be "API Access")
- Generate a new token if the current one has expired
- Ensure there are no extra spaces before or after the token

### Connection Error

- Verify the URL is correct for your Opsera instance
- Check your network connection and internet connectivity
- Confirm the agent URL is accessible from your network

### MCP Server Not Appearing in Cursor

- Completely restart Cursor IDE (close all windows)
- Check that the `mcp.json` syntax is valid JSON format
- Verify the file is saved in the correct location
- Check file permissions to ensure the file is readable

### Token Expired

1. Navigate back to the Personal Access Tokens page
2. Generate a new token with appropriate expiration date
3. Update the `mcp.json` file with the new token
4. Restart Cursor IDE

## Available Opsera MCP Tools

Once successfully configured, you will have access to various Opsera operations through the MCP interface, including:

- Pipeline operations
- User management
- Task management
- Insights and dashboards
- And more...

## Support

For additional help or questions:

**Email:** support@opsera.io