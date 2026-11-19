---
name: blueprints
description: Use when the user wants Genesis to carry out a larger, multi-step data project, such as migrating a platform (Snowflake, Foundry, Power BI, Informatica and others) to Databricks or Snowflake, building a silver or gold layer, or onboarding a new data source, or asks which Genesis blueprints exist or how a running Mission is going.
---

# Running Genesis blueprints and Missions

A Genesis blueprint is a reusable plan for a kind of data project. Started as a Mission, a Genesis agent works through it step by step and asks the user to approve anything that writes to their systems.

## Find a blueprint

Call `search_tools` with `domain: "blueprints"` and a short description of the project as the `query` (for example `"migrate Power BI reports to Databricks AI/BI"`). Show the user the matching blueprints with one line each and let them choose. To read one in full, make the call in its `recommended_next_action`, and pass the `genesis_thread_id` the search returned so the work stays in one thread.

## Start the work

Hand it to a Genesis agent with `ask_agent`, naming the blueprint and the specifics: the source system, the target catalog or database, and any scope the user gave. For example: "Start the `powerbi_to_databricks` blueprint as a Mission for the Sales workspace, targeting catalog `analytics_dev`."

- The agent may come back with a plan or a question that needs the user's answer. Show it to the user and pass the answer back on the same thread (`call_tool` `name: "thread_continue"` with the `genesis_thread_id` it returned). Do not approve a plan or a write on the user's behalf.
- Long work keeps running on the Genesis server. Check on it later with `call_tool` `name: "thread_get"` or `thread_wait_for_change` on the same `genesis_thread_id`.

## Report back

Give the Mission or thread link Genesis returns, what has been done, and what is waiting on the user. When the work produces migrated tables, offer to prove them with the `prover` skill.
