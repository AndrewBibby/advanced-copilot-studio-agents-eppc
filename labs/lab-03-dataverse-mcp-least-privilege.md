# Lab 4 – Dataverse MCP & Least-Privilege Data Access

**Module 4 · Dataverse MCP & least-privilege data access · ~75 min · 4 exercises (≤20 min each)**

## Objective

Give your agent real business data by wiring **Dataverse through the MCP server**, then scope its tools to least privilege so it can read what it needs and nothing more.

## Prerequisites

- Lab 0 complete, with a developer environment that has **Dataverse**.
- **Generative orchestration** enabled and a **Managed Environment** (the Dataverse MCP server requires these). If your dev tenant can't enable Managed Environments, use the shared lab environment provided on the day.
- A Dataverse table with a few rows to query (the standard **Account**/**Contact** tables are fine, or create a small custom table).

## Background

MCP is a universal adapter that makes capabilities discoverable to the agent at runtime – "MCP connects capabilities; connectors connect systems." The golden rule: **treat an MCP server like an API with administrative access, not like a document.** Every tool can act on behalf of the user, so governance must be intentional. There are **five ways to retrieve Dataverse data** – Knowledge, MCP server, List Rows connector, Search Query, Prompt Tool; this lab uses the MCP path. See [`artifacts/tool-descriptions-examples.md`](../artifacts/tool-descriptions-examples.md).

---

### Exercise 2.1 – Add the Dataverse MCP server (20 min)

*Goal: connect the MCP server and confirm its tools populate.*

1. In your agent → **Tools** → **Add tool** → **New tool** → **MCP**.
2. Provide a clear name, description and the server URL; set authentication appropriately. A good description helps the orchestrator decide when to call it.
3. Create the connection and **Add**. Confirm the server's tools auto-populate as actions.

✅ **Checkpoint:** the Dataverse MCP tools (`search`, `describe`, `read_query`, etc.) appear in the agent's tool list.

### Exercise 2.2 – Discover schema & query data (20 min)

*Goal: get the agent to discover tables before querying, and return real rows.*

1. Add an instruction telling the agent to **`search`/`describe` first** and to **never answer data questions from memory**.
2. In the Test panel, prompt a question that maps to `read_query` (Dataverse SQL `SELECT`) or `search_data`.
3. Confirm the agent inspects the schema, then returns rows from your table.

✅ **Checkpoint:** the test trace shows `search`/`describe` then a query – not a guessed answer.

### Exercise 2.3 – Scope tools to least privilege (20 min)

*Goal: expose only what the agent needs.*

1. Use the **allowed tools** setting to expose only `search`, `describe`, `read_query`/`search_data`.
2. **Turn off** `create_record`, `update_record`, `delete_record`, and the schema-changing tools.
3. Re-test a read question to confirm it still works with the reduced toolset.

✅ **Checkpoint:** only read tools are enabled; write/delete/schema tools are off.

### Exercise 2.4 – Prove writes are gated & test end-to-end (15 min)

*Goal: confirm safety rails and run a realistic query.*

1. (Optional) Temporarily enable one write and confirm `delete_record`/`delete_table` require **explicit user approval**, and that **RBAC** stops the agent seeing data the signed-in user can't.
2. Run a natural-language question end-to-end – e.g. "How many active accounts are in London?" – and confirm the agent uses the tool rather than guessing.
3. Turn writes back off.

✅ **Checkpoint:** you can state which retrieval pattern (of the five) you'd choose for a different question and why.

---

## Key concepts

Dataverse MCP · tool scoping (allowed-clients & allowed-tools) · least-privilege data access · `search`/`describe`/`read_query`/`search_data` · write vs. read tools · RBAC · HITL checkpoints around create/update.

## Success criteria

- [ ] The agent answers a data question by **calling the MCP tool** (visible in the test trace), not from memory.
- [ ] Only **read** tools are exposed; write/delete/schema tools are off.
- [ ] You can articulate which retrieval pattern you'd choose for a different question and why.

## Stretch goals

- Add a **Prompt Tool** for reasoning over a pre-filtered set (<~1,000 rows).
- Bring in a **Microsoft Foundry** model (BYOM) or a connected Foundry agent and compare answer quality/cost.
- Add a second **connected agent** specialising in a different table and let the orchestrator route between them (sets up Lab 5).

➡ Next: **[Lab 5 – Authentication, DLP & Entitlement](lab-04-auth-dlp-entitlement.md)**
