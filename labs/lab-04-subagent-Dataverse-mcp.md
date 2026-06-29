# Lab 4 – Creating a Subagent & Adding Dataverse MCP

**Module 4 · Subagent design & Dataverse MCP integration · ~20 min · 1 exercise**

## Objective

Create a specialist subagent (narrow, single-table focus) and wire it to a Dataverse MCP server so the parent orchestrator can delegate data queries to it.

## Prerequisites

- Lab 0 complete, with a developer environment that has **Dataverse**.
- Lab 3 complete (you have a working agent with instructions).
- **Generative orchestration** enabled and a **Managed Environment** (required for the Dataverse MCP server).
- A Dataverse table with a few rows (standard **Account**/**Contact** tables or a small custom table).

## Background

A **subagent** is a specialist child agent designed to do one job. It's tied to a parent orchestrator, inherits the parent's security context, and is invoked by the parent when that job is needed. The golden rule for subagents: **scope = one table, one responsibility, one knowledge source.** Subagents fail when they try to be generalists. MCP is the bridge that connects the subagent to Dataverse at runtime—treat it like an API with full access, scoped by the agent's instructions and allowed tools.

### What matters most when building subagents:

1. **Narrow role, narrow knowledge.** If your subagent owns "Accounts," it should *only* read Account fields. Resist the urge to add "also query Contacts" – create a second subagent instead.
2. **Least-privilege tools.** Expose only the tools it needs: `search` (find tables), `describe` (schema), `read_query` (SELECT). Turn off create/update/delete—writes go through the parent or explicit human approval.
3. **Clear invocation intent in parent instructions.** The orchestrator needs explicit instructions on *when* to hand off to this subagent. Vague routing leads to wrong tool calls.
4. **Inherit security, don't bypass it.** Subagents run as the signed-in user. If the user can't see a field in Dataverse, the agent can't either (RBAC applies at data layer). Don't add workarounds.
5. **One MCP server per data domain.** Each subagent gets its own MCP connection to Dataverse. Don't share one MCP server across multiple subagents—it makes scoping and troubleshooting harder.

---

### Exercise 4.1 – Create a specialist subagent and wire Dataverse MCP (20 min)

*Goal: build a single-table subagent, connect it to Dataverse via MCP, and test one query.*

1. **Create the subagent:**
   - In your orchstrastor agent, navigate to **Agents** → **New child agent**.
   - Name it clearly (e.g., `Account Specialist`) and give it a tight role: *"You are an Account Specialist. Your single job is to retrieve and summarize Account records from Dataverse based on user questions. Always search the schema first, then query. Never invent data."*
   - Save it in the same **solution** as your orchestrator agent.

2. **Add the Dataverse MCP server:**
   - In the subagent → **Tools** → **Add tool** → **MCP**.
   - Provide:
     - **Name:** `Dataverse Account Lookup`
     - **Description:** `Access Account table data. Use search/describe to explore schema, read_query to retrieve records.`
     - **Server URL:** (your Dataverse MCP server endpoint)
   - Create and confirm the MCP tools appear in the tool list.

3. **Scope to read-only:**
   - In **Tools**, turn on **allowed tools** filter.
   - Select only: `search`, `describe`, `read_query` (or `search_data` if your MCP exposes it).
   - **Turn off** `create_record`, `update_record`, `delete_record`, and any schema-altering tools.

4. **Test end-to-end:**
   - Open the **Test panel** and ask a question tied to Accounts (e.g., "Show me all active accounts in the Redmond region" or "What is the industry of account ABC?").
   - Confirm the trace shows:
     1. `search` or `describe` (agent exploring the schema)
     2. `read_query` (agent querying Accounts)
     3. A real row returned (not a guessed answer)

5. **Publish the subagent:**
   - Select **Publish** in the agent.
   - Wait for the publish confirmation to complete before continuing.

✅ **Checkpoint:** The subagent retrieves real data via MCP; only read tools are exposed; and the subagent is published.

---

## Key concepts

Subagent architecture · scope (one table, one responsibility) · least-privilege tools · MCP server as runtime adapter · RBAC enforcement · parent → subagent delegation.

## Success criteria

- [ ] Subagent has a **single-table role** and tight instructions (no generalist sprawl).
- [ ] Dataverse MCP tools appear in the tool list; **only read tools are allowed**.
- [ ] A test query returns **real rows from Dataverse**, not a fabricated answer.
- [ ] The test trace shows **schema discovery then query execution**.
- [ ] The subagent is **published** after testing.
- [ ] The parent agent can **delegate account lookups** to this subagent.
- [ ] You can articulate why subagents fail when scoped too broadly.

## Stretch goals

- Add a second specialist subagent for a different table (e.g., `Contact Specialist`) and manually invoke both from the orchestrator's Test panel.
- Enable one write tool (e.g., `create_record`) and add a **HITL (Human-in-the-Loop) checkpoint** in the parent to approve writes before delegation.
- Measure query cost and latency; compare MCP vs. other Dataverse retrieval patterns (Knowledge, Search Query, Prompt Tool).
- If you want to learn more about workflows in the new UI, complete **[Lab 7 – Monitoring, Testing & Iteration](lab-06-monitoring-testing-iteration.md)**.

➡ Next: **[Lab 5 – Auth, DLP & Entitlement](lab-05-auth-dlp-entitlement.md)**
