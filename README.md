# MCP-test
Testing VS Code and MCP for D365

## Setup

### Prerequisites

- VS Code with the [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) extension installed
- A Dynamics 365 Finance & Operations environment (version 10.0.46 or higher, Tier 2 or PPAC-deployed)
- The **(Preview) Dynamics 365 ERP Model Context Protocol server** feature enabled in D365 Feature Management
- Your VS Code client ID added to **System administration > Setup > Allowed MCP clients** in D365

### Connecting to the D365 MCP Server

This repository includes a `.vscode/mcp.json` configuration that connects VS Code to the Dynamics 365 ERP MCP server.

1. Open this repository in VS Code.
2. Open GitHub Copilot Chat (**Ctrl+Shift+P** → **Chat: Open Chat**) and switch to **Agent** mode.
3. VS Code will prompt you for your **Dynamics 365 base URL** (e.g. `https://contoso.operations.dynamics.com`).
4. Authenticate with your D365 credentials when prompted.
5. The `Dynamics-365-ERP-MCP` server will appear in the MCP tools list and be available to Copilot agents.
