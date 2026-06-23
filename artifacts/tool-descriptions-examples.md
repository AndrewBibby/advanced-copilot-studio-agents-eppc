# Tool description examples — vague vs. specific

The orchestrator reads **tool descriptions** to decide which tool to call. Vague = never called (or called at the wrong time). Specific and unambiguous = reliable execution. Below are before/after rewrites you can adapt.

> Rule of thumb: a good description says **what the tool does**, **what inputs it needs**, and **when the orchestrator should choose it** (and, where useful, when *not* to).

---

| ❌ Vague | ✅ Specific |
|---|---|
| "Gets data." | "Returns open sales orders for a given account ID from Dataverse. Use when the user asks about an account's current or pending orders. Requires `account_id`." |
| "Customer tool." | "Looks up a customer's contact record (name, email, phone, account owner) by email address. Use to identify a caller before any account action. Requires `email`." |
| "Sends email." | "Sends a templated order-confirmation email to a customer. Use ONLY after an order is created and the user has confirmed the recipient. Requires `order_id` and `recipient_email`." |
| "Search." | "Full-text search across the knowledge base of product FAQs. Use for how-to and policy questions. Do NOT use for live account data — use the Dataverse tools for that." |
| "Create record." | "Creates a new support case in Dataverse. Use after the issue is described and the user confirms. Requires `subject`, `description`, `priority`. This is a write action — gate it behind human approval." |

---

## Dataverse MCP tool descriptions (reference)

When you scope the Dataverse MCP server, the named tools already carry a clear contract. Keep descriptions aligned with this intent and expose only what you need:

| Tool | Purpose | Notes |
|---|---|---|
| `search` | Find table schemas and business skills by keyword | Always call before querying. |
| `describe` | Get details for tables, records, schemas, skills, apps | Inspect columns before `read_query`. |
| `read_query` | Run Dataverse SQL `SELECT` queries | Read-only. |
| `search_data` | Search structured and unstructured data | Good for fuzzy lookups. |
| `create_record` | Insert a new row (returns GUID) | Write — gate behind approval. |
| `update_record` | Update an existing row | Write — gate behind approval. |
| `delete_record` | Delete a row | **Requires explicit user approval by design.** |
| `create/update/delete_table` | Scaffold or evolve schema | `delete` requires explicit approval. Rarely exposed to agents. |

---

## Checklist for any new tool description

- [ ] States the **action** in one clear verb phrase.
- [ ] Lists the **required inputs** by name.
- [ ] Says **when to choose** this tool (and when not to).
- [ ] Flags **write/irreversible** actions so they can be gated.
- [ ] Is **distinct** from every other tool's description (no overlap that confuses routing).
