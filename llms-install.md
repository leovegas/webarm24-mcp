# Installing the WebArm24 MCP server (instructions for AI agents such as Cline)

WebArm24 is a **hosted remote MCP server**. There is nothing to clone, build or install:
do not run `npm install`, `pip install` or `git clone`. You only add a remote server entry with an API key.

## 1. Get an API key from the user

Ask the user for their WebArm24 API key. It starts with `wak_`.
If they don't have one:
1. Sign up at https://webarm24.online. New accounts get free credits.
2. Click the **MCP** button in the app and create a key.

## 2. Add the server to the MCP settings

Add this entry to `mcpServers` in Cline's MCP settings file (`cline_mcp_settings.json`). Keep any existing servers.

```json
{
  "mcpServers": {
    "webarm24": {
      "type": "streamableHttp",
      "url": "https://webarm24.online/mcp",
      "headers": {
        "Authorization": "Bearer wak_YOUR_KEY"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Replace `wak_YOUR_KEY` with the user's key. Use exactly `https://webarm24.online/mcp`: the `www.` host
redirects, and some clients don't follow redirects.

## 3. Verify

Call the `account_me` tool. It is free, and it returns the user's account and credit balance.
- **401 / "Invalid, revoked or missing API key"**: the key is wrong or missing the `Bearer ` prefix.
- **Tools are listed but calls fail**: the `Authorization` header isn't being sent. Check the `headers` block.

## Notes for the agent

- Read the resource `webarm://docs/pipeline-steps` before you create pipelines.
- CRUD and status tools are free. Pipeline runs, AI builder calls and browser/email tool calls cost credits.
- `credits_checkout_url` returns a payment link. Only a human should open it.
