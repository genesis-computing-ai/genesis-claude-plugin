# Genesis Data Agents for Claude Code

This plugin connects Claude Code to your Genesis server, so you can work with Genesis data agents from your terminal: search your data and its lineage, run queries through your Genesis connections, start blueprints and Missions, and prove migrations with Prover.

## What you need

- A Genesis server reachable over HTTPS with sign-in turned on. Your Genesis admin can confirm this on **Config > Agent Gateways**.
- Claude Code v2.1.292 or later.

## Install

```bash
claude plugin install genesis-data-agents --marketplace genesis-computing-ai/genesis-claude-plugin
```

Or in two steps (any recent Claude Code):

```bash
claude plugin marketplace add genesis-computing-ai/genesis-claude-plugin
claude plugin install genesis-data-agents@genesis-computing
```

When you enable the plugin, Claude Code asks for your **Genesis server URL** (for example `https://your-genesis-host`). You can change it later in `/config`.

## Sign in

Start Claude Code, type `/mcp`, choose `genesis`, pick **Authenticate**, and sign in in the browser tab that opens. You do this once. On a machine without a browser, run `claude mcp login genesis --no-browser`, open the link it prints, and paste the address you land on back into the terminal.

Claude Code signs in without a client ID: it identifies itself to Genesis with a client metadata document, and Genesis sends you on to your company's sign-in page.

### If your Genesis admin gives you a client ID

Some Genesis deployments sign in directly with your identity provider and need a pre-registered OAuth client ID. In that case, add the server yourself instead of using the plugin's built-in one, with the client ID your admin gives you:

```bash
claude mcp add --transport http --client-id <client-id> --callback-port 31318 genesis https://your-genesis-host/mcp
```

## Try it

Run `/genesis-data-agents:genesis-status`. It lists the Genesis agents you can work with.

## What's included

| Component | What it does |
|---|---|
| `genesis` MCP server | Connects to `<your Genesis server>/mcp` with browser sign-in |
| `genesis` skill | Tells Claude when and how to hand data work to Genesis |
| `prover` skill | Proves that a migrated or rebuilt table matches its source with Genesis Prover |
| `blueprints` skill | Finds a Genesis blueprint and runs it as a Mission |
| `genesis-status` command | Checks the connection and lists your agents |

## Support

support@genesiscomputing.ai

## License

Apache-2.0. See [LICENSE](LICENSE).
