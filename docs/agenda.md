# Agenda & module overview

A full day, structured into five modules that follow the lifecycle of an agent – **design → extend → govern → keep humans in the loop → operate & improve**. Each module is paired with a hands-on lab, and **every lab is split into exercises of no more than 20 minutes** so there's always a clean stopping point.

| # | Module | Lab | Duration | Exercises |
|---|--------|-----|----------|-----------|
| – | New Copilot Studio UI – changes & new features | – | 15 min | – |
| 01 | Designing reliable agents | Lab 1 – Instruction Tuning & Grounding | 60 min | 3 × 20 min |
| 02 | Extending agents – tools & data | Lab 2 – Dataverse MCP & Least-Privilege Data Access | 75 min | 4 × ≤20 min |
| 03 | Governing & securing agents | Lab 3 – Authentication, DLP & Entitlement | 60 min | 3 × 20 min |
| 04 | Workflow checkpoint & orchestration | Lab 4 – Workflow Approval Gates | 45 min | 3 × ≤20 min |
| 05 | Test, monitor, evaluate & improve | Lab 5 – Monitoring, Testing & Iteration | 60 min | 3 × 20 min |
| ✦ | Old UI → New UI (cross-cutting / optional) | Lab 6 | 60 min | 3 × ≤20 min |

---

## Orientation – the new Copilot Studio UI (15 min)

Copilot Studio's 2026 authoring experience reshapes the building blocks. Three new concepts replace the familiar ones:

| New building block | Replaces | Use when |
|---|---|---|
| **Skill** | Topics | Written instructions the agent follows directly; plain-English steps are enough. |
| **Workflow** | Agent Triggers | Hybrid steps — fixed logic mixed with AI classification and inline agent calls; you need control *plus* smarts. |
| **Connected agent** | Child agents | A separate specialist with its own tools and knowledge; the task needs a full sub-agent. |

Other changes worth knowing on day one:

- **Generative orchestration by default** – a code-based runtime with deeper reasoning replaces the classic orchestrator. Classic still exists for deterministic control, but **there is no supported migration path between Classic and New**, and agents built in one mode don't appear as connected agents in the other.
- **Knowledge slimmed, Memory added** – fewer built-in knowledge sources in the New UI (SharePoint, OneDrive, files and public web supported today; Dataverse, M365 Graph and connectors not yet). A new **Memory** persists across chats and sessions.
- **Settings gotcha** – set the **Solution** and **language** *before* you save an agent for the first time; this is still buggy.

---

## Module 1 – Designing reliable agents (60 min)

*Instructions, grounding & context that reduce hallucinations.*

**Core ideas**

- **Specialists over generalists.** One agent, one job. When prompts get long, that's a signal to split the agent, not to add instructions.
- **Anatomy of good instructions** – Role, Objective & task flow, Tool-usage rules, Reasoning & grounding rules. Keep it tight (up to 8,000 chars, but start simple and iterate).
- **Grounding & moderation dials** – scope knowledge narrowly, "use only specified knowledge", set moderation level, return citations, add per-topic custom instructions.
- **Choosing the right tool** – Agent Builder vs. Copilot Studio vs. Microsoft Foundry; declarative vs. custom-engine agents; conversational vs. autonomous.
- **Multi-agent design** – orchestrator + specialists; child vs. connected agents; the "Russian doll" pattern.

➡ **[Lab 1 – Instruction Tuning & Grounding](../labs/lab-01-instruction-tuning-grounding.md)**

---

## Module 2 – Extending agents – tools & data (75 min)

*MCP, Dataverse, Foundry models and multi-agent reach.*

**Core ideas**

- **MCP as a capability layer** – a universal adapter that makes enterprise capabilities discoverable to agents at runtime. Treat MCP servers "like APIs with administrative access, not like documents."
- **The Dataverse MCP server** – named tools (`search`, `describe`, `read_query`, `search_data`, `create_record`, `update_record`, `delete_record`, schema and file tools). Scope which tools are exposed; `delete_*` requires explicit approval; RBAC always applies.
- **Five ways to retrieve Dataverse data** – Knowledge, MCP server, List Rows connector, Search Query, Prompt Tool. Pick the pattern, not just the first button.
- **Prompts as tools**, entities & slot filling, variables, skills (code-based and new-UI markdown skills).
- **Bring Microsoft Foundry in** – Foundry models (BYOM) and connected Foundry agents.
- **Multi-agent orchestration** – the Single Response Principle and ten rules that keep delegation clean.

➡ **[Lab 2 – Dataverse MCP & Least-Privilege Data Access](../labs/lab-02-dataverse-mcp-least-privilege.md)**

---

## Module 3 – Governing & securing agents (60 min)

*Identity, DLP, environments and cost control.*

**Core ideas**

- **Authentication patterns that ship** – No auth (block in prod) → Entra ID → SSO → On-behalf-of (the key pattern for secure tool access) → web channel security.
- **Microsoft Entra Agent ID** – every agent gets its own identity; govern agents like employees.
- **DLP for Copilot Studio** – environment-level connector policies, endpoint filtering, enforcement (violating agents are suspended).
- **Environment strategy** – tier by audience and risk: Dev, Test, Internal Prod, External Prod – all Managed Environments. Plus the Direct Line / external-agent DLP conflict and why one environment is never enough.
- **ALM** – environment variables, connection references, Managed Environments, Pipelines.
- **Cost control** – Copilot Credits, the agent usage estimator, design levers that move consumption.
- **Visibility** – Copilot Dashboard, PPAC analytics, Agent 365, Purview, Sentinel.

➡ **[Lab 3 – Authentication, DLP & Entitlement](../labs/lab-03-auth-dlp-entitlement.md)**

---

## Module 4 – Workflow checkpoint & orchestration (45 min)

*Approvals, RFI and AI-driven workflows.*

**Core ideas**

- **Workflows in 2026** – redesigned canvas with native AI actions, agent nodes and node-level testing; Classic Workflows (formerly "Agent Flows") live side-by-side.
- **Request for Information (RFI)** – pause a workflow, ask a named human via Outlook, collect structured input, resume.
- **AI Approvals** – auto-approve low-risk requests, escalate exceptions, keep a human override with captured explanations for audit.
- **Express Mode** for agent-triggered workflows that must finish within the 2-minute limit.

➡ **[Lab 4 – Workflow Approval Gates](../labs/lab-04-workflow-approval-gates.md)**

---

## Module 5 – Test, monitor, evaluate & improve (60 min)

*Closing the agent lifecycle loop.*

**Core ideas**

- **Copilot Studio Kit** – batch testing, test types (response/attachment/topic/generative match), rubrics for scoring generative answers, Compliance Hub & KPIs.
- **Eval gates in CI/CD** – run Kit test sets in a pipeline; fail the build when scores drop below threshold; pair with `pac` ALM commands.
- **Monitor in two places** – per-agent Copilot Studio analytics and fleet-wide Agent 365 observability.
- **The agentic improvement loop** – Analyze → Adjust → Re-test → Ship & repeat.

➡ **[Lab 5 – Monitoring, Testing & Iteration](../labs/lab-05-monitoring-testing-iteration.md)**

---

## ✦ Cross-cutting (optional) – Old UI → New UI

*The same tasks in the new agent experience.*

The 2026 new experience replaces topics/triggers/node logic with a single instructions-driven agent on one surface (**Build · Preview · Evaluate · Monitor**). This optional lab re-creates **Lab 1** (instruction tuning and grounding, using **Instructions + a Skill** instead of topics) and **Lab 4** (workflow approval gates, using the new **Workflows** designer + **agent node**), so attendees can map what they already know in Classic onto the new UI – and decide which experience to use for which job. Remember: **no migration path** between Classic and New.

➡ **[Lab 6 – Old UI → New UI](../labs/lab-06-old-vs-new-ui.md)**
