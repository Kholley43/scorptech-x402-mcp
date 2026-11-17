# ScorpTech x402 MCP Server

**1,012 x402 pay-per-call tools: web data, security/OSINT, SEC/public data, Solana/EVM lookups.**
Paid per call in USDC on Solana through the [PayAI](https://facilitator.payai.network) facilitator. No signup, no API key, no subscription.

This repository is the public listing for the hosted ScorpTech x402 MCP server. The server runs as a remote
Streamable HTTP endpoint operated by [ScorpTech](https://scorptech.it.com); there's nothing to install or self-host.

| | |
|---|---|
| MCP endpoint (Streamable HTTP) | `https://scorptech.it.com/api/x402/mcp` |
| Docs / tool catalog | https://scorptech.it.com/api/x402/docs |
| Health | https://scorptech.it.com/api/x402/health |
| Official MCP Registry | [`com.it.scorptech/x402`](https://registry.modelcontextprotocol.io/v0/servers?search=com.it.scorptech/x402) |
| Protocol | x402 v2 (exact scheme, USDC) |
| Network | Solana mainnet |

## What's inside

1,012 tools grouped roughly as:

- **Web data:** page fetch and extraction, robots/sitemaps, tech-stack detection, Wayback lookups, and more
- **Security / OSINT:** HTTP security-header audits, email auth (SPF/DKIM/DMARC/MTA-STS), domain intel (DNS, RDAP, crt.sh certificates), CVE lookups, dependency checks
- **SEC and public data:** SEC EDGAR filings and company facts, weather (NWS), earthquakes (USGS), arXiv, public holidays, and others
- **Crypto lookups:** Solana and EVM wallet, token, and gas data
- **Developer utilities**

The full catalog, with each tool's price, parameters, and example output, is at the [docs endpoint](https://scorptech.it.com/api/x402/docs)
(also available as [OpenAPI](https://scorptech.it.com/api/x402/openapi.json)).

## Add it to your MCP client

Any client that supports remote Streamable HTTP servers can connect directly:

```json
{
  "mcpServers": {
    "scorptech-x402": {
      "type": "streamable-http",
      "url": "https://scorptech.it.com/api/x402/mcp"
    }
  }
}
```

For clients that only support stdio, use a bridge such as [`mcp-remote`](https://www.npmjs.com/package/mcp-remote):

```json
{
  "mcpServers": {
    "scorptech-x402": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://scorptech.it.com/api/x402/mcp"]
    }
  }
}
```

Listing tools (`tools/list`) is free. Calling a tool returns an x402 payment requirement unless the call includes a payment.

## How pricing works

- Every tool has a fixed per-call price, mostly **$0.001 to $0.01 USDC** (a few heavier tools cost up to $0.03). Each tool's price is listed in the docs.
- Payment uses the [x402 protocol](https://x402.org): an unpaid call returns a `Payment required` response describing the price, asset (USDC), network (Solana), and recipient.
  Your x402-capable client signs a USDC payment and retries the call, and the result comes back once the payment settles.
- Settlement goes through the PayAI facilitator, which also pays the Solana network fee, so you only need USDC.
- Over plain HTTP the same tools are at `https://scorptech.it.com/api/x402/v1/...`. Use any x402 client (`@x402/fetch`, `@x402/axios`, Python `x402`).
- `/health`, `/docs`, `/docs.json`, and `/openapi.json` are free.

## Links

- Website: https://scorptech.it.com
- Docs: https://scorptech.it.com/api/x402/docs
- MCP Registry entry: `com.it.scorptech/x402`
- x402 protocol: https://x402.org

## Author

ScorpTech / Kaleb Holley · https://scorptech.it.com

## License

MIT. See [LICENSE](LICENSE). This repo has listing metadata only; the hosted service is operated by ScorpTech.
