# Ontraccr MCP server for ChatGPT and Claude

**ChatGPT, Claude and other AI agents can work with your Ontraccr account through Cotlet.dev.** Connect your own signed-in Cloud Browser to review time cards, approve forms, draft field shifts and check project budgets. Approvals, published shifts and actions that reach clients or crews wait for your confirmation.

## What you can ask

> Review Team Cards waiting for my approval.

> List forms pending my approval.

> Draft field shifts for next week for my review.

> Check hours used against the project budget.

> Prepare a change order for signature for my approval.

> Move a job card and assign the follow-up.

## Connect your account

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Add `https://cotlet.dev/mcp/v1/connect` in Settings > Apps & Connectors, then sign in to Cotlet.dev with OAuth.

### Claude

Add `https://cotlet.dev/mcp/v1/connect` in Settings > Connectors > Add custom connector.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Ontraccr tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```bash
git clone https://github.com/cotlet-connect/ontraccr-mcp.git
cd ontraccr-mcp
python3 ontraccr_agent.py serve
```

Or with Docker:

```bash
docker build -t ontraccr-mcp .
docker run -i --rm -e COTLET_API_KEY ontraccr-mcp
```

Tools: `ontraccr_guide`, `ontraccr_status`, `ontraccr_open`, `ontraccr_read`, `ontraccr_click`, `ontraccr_type`, `ontraccr_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, standard library only. Run from this repository:

```bash
export COTLET_API_KEY="your-key"
python3 ontraccr_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 ontraccr_agent.py status    # is Ontraccr ready in your Cotlet.dev account
python3 ontraccr_agent.py guide     # Ontraccr screens and sign-in link
python3 ontraccr_agent.py read      # open Ontraccr, read the page, close the browser
python3 ontraccr_agent.py tools     # list Cotlet.dev tools
python3 ontraccr_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Ontraccr users

**Does Ontraccr have a public API or official MCP server?**

The Cotlet.dev integration page reports no public Ontraccr API documentation, official Ontraccr MCP server or official ChatGPT or Claude connector found, checked 17 November 2026.

**How do I connect Ontraccr to ChatGPT?**

Sign up at https://cotlet.dev/signup?app=ontraccr and sign in at app.ontraccr.com/login in your Cotlet.dev Cloud Browser. Add https://cotlet.dev/mcp/v1/connect in ChatGPT with OAuth.

**Can I use Ontraccr with Claude?**

Yes. Add https://cotlet.dev/mcp/v1/connect as a custom connector in Claude and sign in to Cotlet.dev.

**Is this an official Ontraccr MCP server?**

No. Cotlet.dev is independent and is not affiliated with, endorsed by or sponsored by Ontraccr.

## Integration details

https://cotlet.dev/integrations/ontraccr-api-mcp-server

---

More: https://cotlet.dev/integrations/ontraccr-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=ontraccr

Start free: https://cotlet.dev/signup?app=ontraccr&utm_source=github&utm_medium=readme&utm_campaign=ontraccr
