# steuerboard

Model Context Protocol (MCP) Server for the *steuerboard* API.

<div align="left">
    <a href="https://www.speakeasy.com/?utm_source=steuerboard&utm_campaign=mcp-typescript"><img src="https://www.speakeasy.com/assets/badges/built-by-speakeasy.svg" /></a>
    <a href="https://opensource.org/licenses/MIT">
        <img src="https://img.shields.io/badge/License-MIT-blue.svg" style="width: 100px; height: 28px;" />
    </a>
</div>


<br /><br />
> [!IMPORTANT]
> This MCP Server is not yet ready for production use. To complete setup please follow the steps outlined in your [workspace](https://app.speakeasy.com/org/steuerboard-4kc/mcp). Delete this notice before publishing to a package manager.

<!-- Start Summary [summary] -->
## Summary

For more information about the API: [Find out more about Steuerboard API](https://docs.steuerboard.com)
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [steuerboard](#steuerboard)
  * [Installation](#installation)
  * [Development](#development)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start Installation [installation] -->
## Installation

> [!TIP]
> To finish publishing your MCP Server to npm and others you must [run your first generation action](https://www.speakeasy.com/docs/github-setup#step-by-step-guide).
<details>
<summary>DXT (Desktop Extension)</summary>

Install the MCP server as a Desktop Extension using the pre-built [`mcp-server.dxt`](./mcp-server.dxt) file:

Simply drag and drop the [`mcp-server.dxt`](./mcp-server.dxt) file onto Claude Desktop to install the extension.

The DXT package includes the MCP server and all necessary configuration. Once installed, the server will be available without additional setup.

> [!NOTE]
> DXT (Desktop Extensions) provide a streamlined way to package and distribute MCP servers. Learn more about [Desktop Extensions](https://www.anthropic.com/engineering/desktop-extensions).

</details>

<details>
<summary>Cursor</summary>

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=Steuerboard&config=eyJtY3BTZXJ2ZXJzIjp7IlN0ZXVlcmJvYXJkIjp7InR5cGUiOiJtY3AiLCJ1cmwiOiJodHRwczovL2V4YW1wbGUtY2xvdWRmbGFyZS13b3JrZXIuY29tL21jcCIsImhlYWRlcnMiOnsiYXV0aG9yaXphdGlvbiI6IiR7U1RFVUVSQk9BUkRfQkVBUkVSX0FVVEh9In19fX0=)

Or manually:

1. Open Cursor Settings
2. Select Tools and Integrations
3. Select New MCP Server
4. If the configuration file is empty paste the following JSON into the MCP Server Configuration:

```json
{
  "mcpServers": {
    "Steuerboard": {
      "type": "mcp",
      "url": "https://example-cloudflare-worker.com/mcp",
      "headers": {
        "authorization": "${STEUERBOARD_BEARER_AUTH}"
      }
    }
  }
}
```

</details>

<details>
<summary>Claude Code CLI</summary>

```bash
claude mcp add --transport sse Steuerboard undefined/sse --header "authorization: ..."
```

</details>
<details>
<summary>Windsurf</summary>

Refer to [Official Windsurf documentation](https://docs.windsurf.com/windsurf/cascade/mcp#adding-a-new-mcp-plugin) for latest information

1. Open Windsurf Settings
2. Select Cascade on left side menu
3. Click on `Manage MCPs`. (To Manage MCPs you should be signed in with a Windsurf Account)
4. Click on `View raw config` to open up the mcp configuration file.
5. If the configuration file is empty paste the full json
```
{
  "mcpServers": {
    "Steuerboard": {
      "command": "npx",
      "args": [
        "steuerboard",
        "start",
        "--bearer-auth",
        "..."
      ]
    }
  }
}
```
</details>
<details>
<summary>VS Code</summary>

Refer to [Official VS Code documentation](https://code.visualstudio.com/api/extension-guides/ai/mcp) for latest information

1. Open [Command Palette](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette)
1. Search and open `MCP: Open User Configuration`. This should open mcp.json file
2. If the configuration file is empty paste the full json
```
{
  "mcpServers": {
    "Steuerboard": {
      "command": "npx",
      "args": [
        "steuerboard",
        "start",
        "--bearer-auth",
        "..."
      ]
    }
  }
}
```

</details>


<details>
<summary> Stdio installation via npm </summary>
To start the MCP server, run:

```bash
npx steuerboard start --bearer-auth ...
```

For a full list of server arguments, run:

```
npx steuerboard --help
```

</details>
<!-- End Installation [installation] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

## Development

Run locally without a published npm package:
1. Clone this repository
2. Run `npm install`
3. Run `npm run build`
4. Run `node ./bin/mcp-server.js start --bearer-auth ...`
To use this local version with Cursor, Claude or other MCP Clients, you'll need to add the following config:

```json
{
  "mcpServers": {
    "Steuerboard": {
      "command": "node",
      "args": [
        "./bin/mcp-server.js",
        "start",
        "--bearer-auth",
        "..."
      ]
    }
  }
}
```

Or to debug the MCP server locally, use the official MCP Inspector: 

```bash
npx @modelcontextprotocol/inspector node ./bin/mcp-server.js start --bearer-auth ...
```


### Cloudflare Deployment

To deploy to Cloudflare Workers:

```bash
npm install 
npm run deploy
```

To run the cloudflare deployment locally:

```bash
npm install 
npm run dev
```

The local development server will be available at `http://localhost:8787`

Then install with Claude Code CLI:

```bash
claude mcp add --transport sse Steuerboard http://localhost:8787/sse --header "authorization: ..."
```





## Contributions

While we value contributions to this MCP Server, the code is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release. 

### MCP Server Created by [Speakeasy](https://www.speakeasy.com/?utm_source=steuerboard&utm_campaign=mcp-typescript)
