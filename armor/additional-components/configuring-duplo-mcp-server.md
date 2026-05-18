# Configuring the DuploCloud MCP Server

The DuploCloud MCP (Model Context Protocol) server exposes your DuploCloud HelpDesk as a set of tools that AI assistants can call directly. Once configured, the assistant can create tickets, manage workspaces, agents, skills, environments, providers, and more — without leaving the chat interface.

This guide covers configuration in the **Claude desktop app** and **Claude Code (VSCode)**.

---

## Part 1 — Claude Desktop App

### Step 1 — Open Developer Settings

Open the Claude desktop app and go to **Settings → Developer** (under the Desktop app section in the left sidebar). The **Local MCP servers** panel shows all configured servers. Initially it is empty.

![](<../../../.gitbook/assets/duplo-mcp-desktop-step-01.png>)

### Step 2 — Edit the Config File

Click **Edit Config**. This opens `claude_desktop_config.json` in your editor — located at `~/Library/Application Support/Claude/claude_desktop_config.json`.

Add the `duplo-helpdesk` entry under `mcpServers`. Replace the URL with your HelpDesk endpoint and the Bearer token with your API token. To find the path to `npx`, run `which npx` in your terminal.

```json
{
  "mcpServers": {
    "duplo-helpdesk": {
      "command": "<full path to npx>",
      "args": [
        "-y",
        "mcp-remote",
        "https://helpdesk.duplo.yourcompany.com/mcp",
        "--header",
        "Authorization: Bearer <your API token>"
      ]
    }
  }
}
```

![](<../../../.gitbook/assets/duplo-mcp-desktop-step-02.png>)

Save the file, then reload the Claude desktop app for the changes to take effect.

### Step 3 — Verify the Server is Running

Return to **Settings → Developer**. The `duplo-helpdesk` server now appears in the list with a **running** status. The panel shows the resolved command path and arguments. Click **View Logs** to inspect connection output if needed.

![](<../../../.gitbook/assets/duplo-mcp-desktop-step-03.png>)

### Step 4 — Confirm Access in Chat

Open a new chat and ask Claude whether it has access to the DuploCloud MCP server. Claude will confirm and list all available tool categories.

![](<../../../.gitbook/assets/duplo-mcp-desktop-step-04.png>)

---

## Part 2 — Claude Code (VSCode)

There are two ways to add the DuploCloud MCP server to Claude Code: via the CLI (recommended) or by manually editing `~/.claude.json`.

### Option 1 — CLI (Recommended)

Open the terminal in VSCode and run the following command, replacing the URL and token with your own:

```bash
claude mcp add --transport http duplo-helpdesk \
  "https://helpdesk.duplo.yourcompany.com/mcp" \
  --header "Authorization: Bearer <your-token>" \
  --scope use
```

![](<../../../.gitbook/assets/duplo-mcp-vscode-step-02.png>)

![](<../../../.gitbook/assets/duplo-mcp-vscode-step-03.png>)

The command confirms the server has been added and shows the URL and headers registered. It also confirms that `~/.claude.json` has been updated.

### Option 2 — Manual Edit

Open `~/.claude.json` in your editor and add the following entry inside the `mcpServers` object (create the key if it does not exist):

```json
"mcpServers": {
  "duplo-helpdesk": {
    "type": "http",
    "url": "https://helpdesk.duplo.yourcompany.com/mcp",
    "headers": {
      "Authorization": "Bearer <your API token>"
    }
  }
}
```

### Reload the Window

After adding the server via either method, reload the VSCode window to apply the changes. Open the command palette with **Cmd+Shift+P**, type **Reload Window**, and select **Developer: Reload Window**.

![](<../../../.gitbook/assets/duplo-mcp-vscode-step-04.png>)

### Verify the Connection

Once the window reloads, open the MCP servers panel in Claude Code by running `/mcp`. The `duplo-helpdesk` server appears under **User** with a **Connected** status.

![](<../../../.gitbook/assets/duplo-mcp-vscode-step-05.png>)

### Confirm Access in Chat

Open a new Claude Code chat and ask whether Duplo MCP access is available. Claude confirms access to the `duplo-helpdesk` server and lists all available tool namespaces.

![](<../../../.gitbook/assets/duplo-mcp-vscode-step-06.png>)
