# Steuerboard TypeScript MCP Server

Model Context Protocol (MCP) Server for the **Steuerboard API**.

<div align="left">
    <a href="https://www.speakeasy.com/?utm_source=steuerboard&utm_campaign=mcp-typescript"><img src="https://www.speakeasy.com/assets/badges/built-by-speakeasy.svg" /></a>
    <a href="https://opensource.org/licenses/MIT">
        <img src="https://img.shields.io/badge/License-MIT-blue.svg" style="width: 100px; height: 28px;" />
    </a>
</div>

<br /><br />

<!-- Start Summary [summary] -->
## Summary

For more information about the API: [Find out more about Steuerboard API](https://docs.steuerboard.com)
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [Steuerboard TypeScript MCP Server](#steuerboard-typescript-mcp-server)
  * [Installation](#installation)
  * [Progressive Discovery](#progressive-discovery)
  * [Development](#development)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start Installation [installation] -->
## Installation

Deployed at https://mcp.steuerboard.com
<details>
<summary>Claude Desktop</summary>

Install the MCP server as a Desktop Extension using the pre-built [`mcp-server.mcpb`](https://github.com/steuerboard/steuerboard-mcp-typescript/releases/download/v0.4.1/mcp-server.mcpb) file:

Simply drag and drop the [`mcp-server.mcpb`](https://github.com/steuerboard/steuerboard-mcp-typescript/releases/download/v0.4.1/mcp-server.mcpb) file onto Claude Desktop to install the extension.

The MCP bundle package includes the MCP server and all necessary configuration. Once installed, the server will be available without additional setup.

> [!NOTE]
> MCP bundles provide a streamlined way to package and distribute MCP servers. Learn more about [Desktop Extensions](https://www.anthropic.com/engineering/desktop-extensions).

</details>

<details>
<summary>Cursor</summary>

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](cursor://anysphere.cursor-deeplink/mcp/install?name=Steuerboard&config=eyJjb21tYW5kIjoibnB4IiwiYXJncyI6WyIteSIsIm1jcC1yZW1vdGVAMC4xLjI1IiwiaHR0cHM6Ly9tY3Auc3RldWVyYm9hcmQuY29tL3NzZSIsIi0taGVhZGVyIiwiYmVhcmVyLWF1dGg6JHtCRUFSRVJfQVVUSH0iXX0=)

Or manually:

1. Open Cursor Settings
2. Select Tools and Integrations
3. Select New MCP Server
4. If the configuration file is empty paste the following JSON into the MCP Server Configuration:

```json
{
  "command": "npx",
  "args": [
    "@steuerboard/mcp",
    "start",
    "--bearer-auth",
    ""
  ]
}
```

</details>

<details>
<summary>Claude Code CLI</summary>

```bash
claude mcp add Steuerboard -- npx -y @steuerboard/mcp start --bearer-auth 
```

</details>
<details>
<summary>Gemini</summary>

```bash
gemini mcp add Steuerboard -- npx -y @steuerboard/mcp start --bearer-auth 
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

```bash
{
  "command": "npx",
  "args": [
    "@steuerboard/mcp",
    "start",
    "--bearer-auth",
    ""
  ]
}
```
</details>
<details>
<summary>VS Code</summary>

[![Install in VS Code](https://img.shields.io/badge/VS_Code-VS_Code?style=flat-square&label=Install%20Steuerboard%20MCP&color=0098FF)](vscode://ms-vscode.vscode-mcp/install?name=Steuerboard&config=eyJjb21tYW5kIjoibnB4IiwiYXJncyI6WyIteSIsIm1jcC1yZW1vdGVAMC4xLjI1IiwiaHR0cHM6Ly9tY3Auc3RldWVyYm9hcmQuY29tL3NzZSIsIi0taGVhZGVyIiwiYmVhcmVyLWF1dGg6JHtCRUFSRVJfQVVUSH0iXX0=)

Or manually:

Refer to [Official VS Code documentation](https://code.visualstudio.com/api/extension-guides/ai/mcp) for latest information

1. Open [Command Palette](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette)
1. Search and open `MCP: Open User Configuration`. This should open mcp.json file
2. If the configuration file is empty paste the full json

```bash
{
  "command": "npx",
  "args": [
    "@steuerboard/mcp",
    "start",
    "--bearer-auth",
    ""
  ]
}
```

</details>
<details>
<summary> Stdio installation via npm </summary>
To start the MCP server, run:

```bash
npx @steuerboard/mcp start --bearer-auth 
```

For a full list of server arguments, run:

```
npx @steuerboard/mcp --help
```

</details>
<!-- End Installation [installation] -->

<!-- Start Progressive Discovery [dynamic-mode] -->
## Progressive Discovery

MCP servers with many tools can bloat LLM context windows, leading to increased token usage and tool confusion. Dynamic mode solves this by exposing only a small set of meta-tools that let agents progressively discover and invoke tools on demand.

To enable dynamic mode, pass the `--mode dynamic` flag when starting your server:

```jsonc
{
  "mcpServers": {
    "Steuerboard": {
      "command": "npx",
      "args": ["@steuerboard/mcp", "start", "--mode", "dynamic"],
      // ... other server arguments
    }
  }
}
```

In dynamic mode, the server registers only the following meta-tools instead of every individual tool:

- **`list_tools`**: Lists all available tools with their names and descriptions.
- **`describe_tool_input`**: Returns the input schema for one or more tools by name.
- **`execute_tool`**: Executes a tool by name with its arguments.

This approach significantly reduces the number of tokens sent to the LLM on each request, which is especially useful for servers with a large number of tools.
<!-- End Progressive Discovery [dynamic-mode] -->

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
      "args": ["./bin/mcp-server.js", "start", "--bearer-auth", "..."]
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
