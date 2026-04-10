---
description: Step-by-step guide to configure the Dynamics 365 Finance & Supply Chain Management (FSCM) MCP server and connect it to VS Code with GitHub Copilot.
mode: ask
---

# Dynamics 365 FSCM – MCP Server Configuration Guide

Follow these steps to enable and connect the **Dynamics 365 ERP Model Context Protocol (MCP) server** for Finance & Supply Chain Management to Visual Studio Code.

---

## Prerequisites

Before you start, confirm the following:

- Your D365 environment is running **version 10.0.47 or higher**.
- The environment is a **Tier 2 (or above)** sandbox or a **Unified Developer Environment**  
  *(Cloud Hosted Environments are not supported)*.
- You have **System Administrator** rights in D365 FSCM.
- **VS Code** is installed with the **GitHub Copilot** extension enabled.

---

## Part 1 – Configure Dynamics 365 FSCM

### Step 1 – Enable the MCP Server Feature

1. Sign in to your Dynamics 365 Finance & Supply Chain Management environment.
2. Navigate to **Feature management** (`System administration > Workspaces > Feature management`).
3. Search for **"(Preview) Dynamics 365 ERP Model Context Protocol server"**.
4. If the feature is not listed, click **Check for updates** in the top-right corner.
5. Select the feature and click **Enable now**.

### Step 2 – Register VS Code as an Allowed MCP Client

1. In D365 FSCM, go to **System administration > Setup > Allowed MCP clients**.
2. Click **New** to add a client entry.
3. Open VS Code and attempt to connect to the MCP server (see Part 2 below).  
   VS Code will print the **Client ID** in the **Output** panel (select "GitHub Copilot" from the dropdown).
4. Copy that Client ID and paste it into the **Client ID** field in D365.
5. Give the entry a friendly **Name** (e.g., `VS Code – GitHub Copilot`) and click **Save**.

> **Tip:** Microsoft pre-registers the VS Code / GitHub Copilot client ID in recent releases.  
> Check whether an entry already exists before adding a new one.

### Step 3 – (Optional) Enable External Language Model Providers

If you want to use external AI models such as Anthropic Claude Sonnet:

1. Open the **Microsoft 365 Admin Center**.
2. Navigate to **Copilot > Settings > Data access**.
3. Under **AI providers**, enable the desired external provider (e.g., Anthropic).
4. Allow 15–30 minutes for the setting to propagate.

---

## Part 2 – Configure VS Code

### Step 4 – Connect VS Code to the D365 MCP Server

1. Open VS Code.
2. Press **Ctrl+Shift+P** (Windows/Linux) or **Cmd+Shift+P** (macOS) to open the Command Palette.
3. Run **MCP: Add Server…**
4. Select **HTTP** as the connection type.
5. Enter the MCP endpoint URL:
   ```
   https://<your-d365-base-url>/mcp
   ```
   Example: `https://contoso.operations.dynamics.com/mcp`
6. VS Code writes the connection into `.vscode/mcp.json` automatically.

> **Note:** If this repository already contains a `.vscode/mcp.json`, VS Code will prompt for your  
> D365 base URL automatically when you open the workspace.

### Step 5 – Authenticate

1. When prompted, sign in with your **D365 / Microsoft Entra ID credentials**.
2. Grant the requested permissions for VS Code to access your D365 environment.
3. The MCP server status icon in the VS Code status bar will turn green when connected.

### Step 6 – Verify the Connection in Copilot Agent Mode

1. Open **GitHub Copilot Chat** (`Ctrl+Shift+P` → **Chat: Open Chat**).
2. Switch to **Agent** mode using the dropdown next to the chat input.
3. Click the **Configure tools** icon (⚙) and confirm **Dynamics-365-ERP-MCP** is listed and checked.
4. Run a test prompt, for example:
   ```
   List the open purchase orders in my D365 environment.
   ```
5. Copilot should call the MCP server and return results from your D365 FSCM data.

---

## Troubleshooting

| Issue | Resolution |
|---|---|
| Feature not visible in Feature management | Click **Check for updates**, then refresh the list |
| "Client not allowed" error | Add the VS Code Client ID to **Allowed MCP clients** in D365 |
| MCP server status stays grey/disconnected | Verify the URL format (`https://<base-url>/mcp`) and your network access |
| Cloud Hosted Environment (CHE) | CHEs are not supported; use a Tier 2 sandbox or Unified Developer Environment |
| External AI model not available | Enable the provider in M365 Admin Center and wait up to 30 minutes |

---

## References

- [Microsoft Docs – Use MCP for finance and operations apps](https://learn.microsoft.com/dynamics365/fin-ops-core/dev-itpro/copilot/copilot-mcp)
- [Microsoft Docs – Connect to the D365 ERP MCP server with VS Code](https://learn.microsoft.com/dynamics365/fin-ops-core/dev-itpro/copilot/mcp/mcp-vscode)
- [VS Code – Prompt Files documentation](https://code.visualstudio.com/docs/copilot/customization/prompt-files)
