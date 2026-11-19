---
name: genesis
description: Use when the user asks about their company's data, tables, pipelines, lineage, data migrations, or wants a Genesis data agent to do data engineering work (find data, run queries, build or check a pipeline, run a blueprint or mission, prove a migration). Routes the work to the Genesis MCP server.
---

# Working with Genesis

Genesis is the user's data agent platform. It is reached through the MCP server named `genesis`.

The server exposes a small set of named tools:

| Tool | Use it to |
|---|---|
| `search_data_context` | Find tables, columns, reports, pipelines and wiki pages by what they mean |
| `describe_asset` | Read one asset's columns, owners and description by its qualified name |
| `get_lineage` | See what feeds an asset and what breaks if it changes |
| `run_query` | Run SQL through a Genesis connection |
| `search_tools` | Find any other Genesis capability: tools, skills, blueprints, knowledge bases |
| `ask_agent` | Hand a whole task to a Genesis agent and wait for its answer |
| `call_tool` | Run any other Genesis action or tool by name, such as `list_agents`, `help` or `status` |

## Before you start

- If the `genesis` server's tools are missing or return an authentication error, tell the user to run `/mcp`, choose `genesis`, pick **Authenticate**, and finish signing in in the browser.
- Call `call_tool` with `name: "list_agents"` to see which Genesis agents the user can work with, and which one is the default. Pass `agent_id` to the other tools to use a different agent.
- When unsure how an action works, call `call_tool` with `name: "describe_action"` (or `help`) before guessing its arguments.

## How to use it

- Questions about the user's data (what tables exist, where a column comes from, what feeds a report): ask Genesis rather than guessing. Start with `search_data_context`, then `describe_asset` and `get_lineage`.
- Database work: run queries with `run_query` through Genesis connections. Never ask the user to paste database credentials into the chat; connections are managed in Genesis.
- Larger work (a migration, a new silver or gold layer, onboarding a data source): see the `blueprints` skill, or hand it to a Genesis agent with `ask_agent`.
- Checking that a migration or rebuild matches its source: see the `prover` skill, and share the proof link Genesis returns rather than row counts you computed yourself.

## Reporting back

- Say which Genesis agent did the work and link any proof, Mission, thread or file Genesis returns.
- If Genesis refuses an action for permissions, tell the user which permission it names; do not try to work around it.
