---
name: prover
description: Use when the user wants to prove, verify or reconcile that a migrated, rebuilt or copied table, pipeline or report matches its source (for example Snowflake to Databricks, Foundry to Databricks, Power BI to AI/BI), or asks for the status or findings of a Genesis Prover run. Uses Genesis Prover through the `genesis` MCP server.
---

# Proving a migration with Genesis Prover

Genesis Prover compares a target against its source and returns a proof: which tables and columns match, which do not, and why. A proof link from Prover is the evidence to share. Do not substitute row counts or spot checks you computed yourself.

## Start a proof

1. Make sure you know the source and the target (for example the source table or Foundry dataset, and the target catalog and schema). If the user has not said, ask.
2. Hand the work to a Genesis agent with `ask_agent`. Describe the outcome in plain words, for example: "Prove that the tables in catalog `sales_v2` match their sources in Snowflake database `SALES`, and give me the proof link." Pass `agent_id` if the user named a specific agent (`call_tool` with `name: "list_agents"` lists them).
3. A proof can take several minutes. If `ask_agent` returns before the work is done, keep the `genesis_thread_id` it returns and follow up with `call_tool` `name: "thread_wait_for_change"` (or `thread_get`) on that thread instead of starting a new one.

To run a Prover step yourself rather than through an agent, find its tool with `search_tools` (`query: "prover"`) and read its contract with `call_tool` `name: "describe_tool"` before calling it.

## Report the result

- Give the proof link, the overall status (Proven, Not yet proven, Proving, or Didn't finish) and the tables or columns that did not match, with Prover's stated reason for each.
- If Prover proposes a fix or a waiver, show it to the user and let them decide. Do not accept a waiver on the user's behalf.
- If Genesis refuses for permissions, say which permission it names.
