# Installing the ScorpTech x402 MCP server (for AI agents such as Cline)

This is a **hosted remote MCP server**. There's nothing to clone, build, or run locally, and no API key or environment variable.

1. Add this entry to the MCP settings file (Cline: `cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "scorptech-x402": {
      "type": "streamableHttp",
      "url": "https://scorptech.it.com/api/x402/mcp/lite",
      "disabled": false
    }
  }
}
```

   If the client only supports stdio servers, use this instead:

```json
{
  "mcpServers": {
    "scorptech-x402": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://scorptech.it.com/api/x402/mcp/lite"]
    }
  }
}
```

2. Check that it works by calling the free `search_tools` tool, for example with `{"query": "dns"}`. It should return a list of tools with prices.

3. `call_tool` runs one of the 1,012 tools and is paid per call in USDC via x402 (Solana or Base). Without a payment, it returns an x402 `PaymentRequired` object (price, network, recipient). That's expected behavior, not an installation error. Paying requires an x402-capable client or wallet. See https://scorptech.it.com/api/x402/docs.

Optional smaller servers with direct tools: `/mcp/security`, `/mcp/web`, `/mcp/sec`, `/mcp/crypto`, `/mcp/dev` (same base URL `https://scorptech.it.com/api/x402`).
