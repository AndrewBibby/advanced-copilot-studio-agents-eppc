# Lab 2 — Extend with Dataverse MCP & Tools

**Module 2 · Extending agents — tools & data · ~75 min**

## Objective

Give your agent real business data by wiring **Dataverse through the MCP server**, then scope its tools to least privilege so it can read what it needs and nothing more.

## Prerequisites

- Lab 0 complete, with a developer environment that has **Dataverse**.
- **Generative orchestration** enabled and a **Managed Environment** (the Dataverse MCP server requires these). If your dev tenant can't enable Managed Environments, use the shared lab environment provided on the day.
- A Dataverse table with a few rows to query (the standard **Account**/**Contact** tables are fine, or create a small custom table).

## Background (why this matters)

MCP is a universal adapter that makes capabilities discoverable to the agent at runtime — "MCP connects capabilities; connectors connect systems." The golden rule: **treat an MCP server like an API with administrative access, not like a document.** Every tool can act on behalf of the user, so governance must be intentional. The Dataverse MCP server exposes named tools with a clear contract; you'll expose only the ones you need.

There are **five ways to retrieve Dataverse data** — Knowledge, MCP server, List Rows connector, Search Query, Prompt Tool. This lab uses the MCP path; the others are summarised in [`docs/agenda.md`](../docs/agenda.md#module-2--extending-agents--tools--data).

## Tasks

1. **Add the Dataverse MCP server.** In your agent → **Tools** → **Add tool** → **New tool** → **MCP**. Provide a clear name, description and the server URL; set authentication appropriately. A good description helps the orchestrator decide when to call it.
2. **Discover the schema.** Use `search` and `describe` to find tables and inspect their columns *before* querying. Add an instruction telling the agent to **search/describe first** and to **never answer data questions from memory**.
3. **Query data.** Run a natural-language question that maps to `read_query` (Dataverse SQL `SELECT`) or `search_data`. Confirm the agent returns rows from your table.
4. **Scope the tools (least privilege).** Use the **allowed tools** setting to expose only `search`, `describe`, `read_query`/`search_data`. **Turn off** `create_record`, `update_record`, `delete_record`, and the schema-changing tools unless a task needs them.
5. **Prove writes are gated.** If you do enable a write, confirm that `delete_record`/`delete_table` require **explicit user approval**, and that **RBAC** stops the agent seeing data the signed-in user can't see.
6. **Test natural-language queries** end-to-end in the Test panel — e.g. "How many active accounts are in London?" — and confirm the agent uses the tool rather than guessing.

## Key concepts

Dataverse MCP · tool scoping (allowed-clients & allowed-tools) · least-privilege data access · `search`/`describe`/`read_query`/`search_data` · write vs. read tools · RBAC · HITL checkpoints around create/update.

## Success criteria

- [ ] The agent answers a data question by **calling the MCP tool** (visible in the test trace), not from memory.
- [ ] Only **read** tools are exposed; write/delete/schema tools are off.
- [ ] You can articulate which retrieval pattern (of the five) you'd choose for a different question and why.

## Stretch goals

- Add a **Prompt Tool** for reasoning over a pre-filtered set (<~1,000 rows).
- Bring in a **Microsoft Foundry** model (BYOM) or a connected Foundry agent and compare answer quality/cost.
- Add a second **connected agent** specialising in a different table and let the orchestrator route between them (sets up Lab 4).

➡ Next: **[Lab 3 — Secure agent tools & connections](lab-03-secure-agent-tools.md)**
