---
name: zoho-cliq-mcp
description: Interact with Zoho Cliq using the Zoho MCP server when the user mentions @zoho, Zoho, Zoho Cliq, or requests operations like listing chats, sending messages, or managing channels.
license: Apache-2.0
metadata:
  version: v1
  publisher: custom
---

# Zoho Cliq MCP Integration Skill

Use this skill when interacting with **Zoho Cliq** via the **Zoho MCP** remote server or local MCP configuration.

## Configuration & Endpoint

- **Server Name**: `ZohoMCP`
- **Remote Endpoint**: `https://cliqqq-939313492.zohomcp.com/mcp/b15c0199dc27ac287174013b14669856/message`
- **Transport**: `http-only` via `npx mcp-remote`
- **Kilo MCP Config File**: [`/home/reak/.config/kilo/mcp_config.json`](file:///home/reak/.config/kilo/mcp_config.json)

```json
"ZohoMCP": {
  "command": "npx",
  "args": [
    "mcp-remote",
    "https://cliqqq-939313492.zohomcp.com/mcp/b15c0199dc27ac287174013b14669856/message",
    "--transport",
    "http-only"
  ]
}
```

## Available MCP Tools

Tools exposed by the remote Zoho MCP server use the `ZohoCliq_` prefix:

### 1. Chats & Conversations
- `ZohoCliq_list_chats`: List direct messages and group chats for the authenticated user.
- `ZohoCliq_get_chat`: Retrieve details for a specific chat by `CHAT_ID`.
- `ZohoCliq_searchChatsV3`: Search chats by name, type, date range, or participant.
- `ZohoCliq_createChatV3`: Create a direct chat or group chat.
- `ZohoCliq_update_chat`: Update chat title, history settings, read status, or close chat.
- `ZohoCliq_pin_chat_v2` / `ZohoCliq_unpin_chat_v2`: Pin/unpin chats.
- `ZohoCliq_mute_chat` / `ZohoCliq_unmute_chat`: Mute or unmute notifications.

### 2. Messaging
- `ZohoCliq_send_message_to_chat`: Post text, cards, slides, or buttons to a chat (`chat_id`, `text`).
- `ZohoCliq_postMessageInChannelByChannelId`: Post a message to a channel by `CHANNEL_ID`.
- `ZohoCliq_share_file_to_chat`: Upload/share a file to a chat.
- `ZohoCliq_delete_message`: Delete a specific message by `CHAT_ID` and `MESSAGE_ID` (Requires user confirmation).
- `ZohoCliq_list_chat_reminders`: List reminders set on chat messages.

### 3. Chat Members & Channels
- `ZohoCliq_list_channels`: List channels.
- `ZohoCliq_list_chat_members`: List participants in a group chat or channel.
- `ZohoCliq_add_chat_members`: Add users to an existing group chat.
- `ZohoCliq_remove_chat_members`: Remove users from a group chat (Requires user confirmation).
- `ZohoCliq_leave_group_chat` / `ZohoCliq_leave_channel`: Leave group chat/channel (Requires user confirmation).

### 4. Organization & Users
- `ZohoCliq_list_users`: List organization users and find user IDs.
- `ZohoCliq_list_designations`: List organization designations.

## Executing Operations via MCP

To call any tool directly via Node script or CLI bridge:

```javascript
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import { StdioClientTransport } from "@modelcontextprotocol/sdk/client/stdio.js";

const transport = new StdioClientTransport({
  command: "npx",
  args: [
    "mcp-remote",
    "https://cliqqq-939313492.zohomcp.com/mcp/b15c0199dc27ac287174013b14669856/message",
    "--transport",
    "http-only"
  ]
});

const client = new Client({ name: "zoho-client", version: "1.0.0" }, { capabilities: {} });
await client.connect(transport);

// Example tool call:
const result = await client.callTool({
  name: "ZohoCliq_list_chats",
  arguments: {}
});
```

## Safety Protocols
- **Always ask for confirmation** before invoking destructive actions (`ZohoCliq_delete_message`, `ZohoCliq_remove_chat_members`, `ZohoCliq_leave_channel`, `ZohoCliq_leave_group_chat`).
