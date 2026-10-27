# MCP Configurations

Complete Model Context Protocol (MCP) server configurations for all AI agents.

## Available MCP Servers

### 1. **gopls-mcp-server**
- **Purpose**: Go language server for code intelligence
- **Binary**: `/home/reak/go/bin/gopls mcp`
- **Used by**: Kilo, VS Code, Cursor

### 2. **postgres**
- **Purpose**: PostgreSQL database queries and schema introspection
- **Script**: `.kilo/scripts/run-postgres-mcp.sh`
- **Used by**: Kilo, VS Code, Cursor

### 3. **typesense**
- **Purpose**: Search engine operations and document queries
- **Script**: `.kilo/scripts/run-typesense-mcp.sh`
- **Used by**: Kilo, VS Code, Cursor

### 4. **playwright**
- **Purpose**: Browser automation and frontend testing
- **Script**: `.kilo/scripts/run-playwright-mcp.sh`
- **Used by**: Kilo, VS Code, Cursor

### 5. **kubectl**
- **Purpose**: Kubernetes cluster management
- **Command**: `npx -y mcp-server-kubernetes`
- **Env**: `KUBECONFIG` required
- **Used by**: Kilo, VS Code, Cursor

### 6. **filesystem**
- **Purpose**: File system access and operations
- **Command**: `npx -y @modelcontextprotocol/server-filesystem`
- **Used by**: Kilo, VS Code, Cursor

### 7. **google-kubernetes-engine**
- **Purpose**: GKE cluster management via Google Cloud
- **URL**: `https://container.googleapis.com/mcp`
- **Auth**: Google credentials
- **Used by**: Kilo, VS Code, Cursor

### 8. **ZohoMCP**
- **Purpose**: Zoho Cliq messaging integration
- **Command**: `npx mcp-remote`
- **URL**: `https://cliqqq-939313492.zohomcp.com/mcp/...`
- **Used by**: Kilo only

### 9. **runpod**
- **Purpose**: RunPod GPU cloud operations
- **URL**: `https://mcp.getrunpod.io/`
- **Used by**: Cursor, Gemini CLI, Claude Desktop, VS Code

### 10. **GitKraken**
- **Purpose**: Git integration and code review
- **Binary**: `/home/reak/.config/Code/User/globalStorage/eamodio.gitlens/gk`
- **Used by**: Claude Desktop only

## Configuration Files

- `complete-mcp-config.json` - All MCPs in one config (use as reference)
- Agent-specific configs should be placed in respective agent directories

## Agent MCP Status

| Agent | MCPs Configured | Missing |
|-------|----------------|---------|
| **Kilo** | 8/8 | ✅ Complete |
| **VS Code** | 7/9 | ZohoMCP |
| **Cursor** | 8/9 | ZohoMCP (has runpod) |
| **Gemini CLI** | 1/9 | 8 MCPs missing |
| **Claude Desktop** | 2/9 | 7 MCPs missing |
| **Claude Code** | 0/9 | All missing |
| **Gemini Antigravity** | 0/9 | All missing |

## Setup Instructions

### For Kilo (Complete)
Already configured at `~/.config/kilo/mcp_config.json`

### For VS Code
Copy to `~/.config/Code/User/mcp_config.json` and add missing MCPs

### For Cursor
Copy to `~/.config/Cursor/User/mcp_config.json` and add ZohoMCP

### For Gemini CLI
Copy to `~/.gemini/config/mcp_config.json`

### For Claude Desktop
Copy to `~/.config/Claude/claude_desktop_config.json`

## Notes

- All configurations use local paths specific to this system
- Adjust paths when deploying to different systems
- Credentials are sourced from `/home/reak/.env`
- Never commit actual credentials to the repository
