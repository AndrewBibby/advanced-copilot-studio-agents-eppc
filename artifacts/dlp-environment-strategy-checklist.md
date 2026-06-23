# DLP & environment strategy checklist

Separate environments by **audience and risk** — not just "dev / test / prod". All tiers should be **Managed Environments**. Treat MCP servers like APIs with administrative access; governance must be intentional.

## Four-tier environment strategy

| Tier | Audience | DLP posture | Key controls |
|---|---|---|---|
| **Dev** (Managed) | Makers build & iterate | Loose — Teams + SharePoint only | No real data; no external publishing; sharing limited to maker group |
| **Test** (Managed) | Integration & acceptance | Production-equivalent (minus live data) | Run Copilot Studio Kit test sets; solution checker enforced |
| **Internal Prod** (Managed) | Employees | Strict — Direct Line blocked | Entra ID auth required on all agents; sharing controls + telemetry |
| **External Prod** (Managed) | Customers / partners | Direct Line **allowed** (isolated here) | Stricter knowledge scoping (no internal SharePoint); dedicated capacity + audit |

> **Why one environment is never enough:** a tenant-wide DLP policy that blocks **Direct Line** (correctly stopping makers publishing to public websites) also blocks the externally-facing customer agent you legitimately need. Isolate Direct Line in a dedicated **External Prod** environment instead of weakening the tenant policy.

## DLP policy checklist

- [ ] Define connector policies **before** makers start building.
- [ ] Block connectors agents don't need; block HTTP, skills and direct endpoint access where not required.
- [ ] Use **endpoint filtering** for URL-level control (e.g. SharePoint → approved sites only).
- [ ] Block **public website / Bing** knowledge by default; allow-list where justified.
- [ ] Block **preview / non-certified** connectors in production.
- [ ] Remember enforcement: agents violating DLP are **suspended** until compliant.

## Tenant settings (PPAC) — set before anyone builds

- [ ] **Who can create environments** — restrict to admins (stops ungoverned sandboxes).
- [ ] **Who can create agents** — all users vs. specific security groups (Copilot Studio author setting).
- [ ] **Generative AI features** — opt in/out, including Bing-grounded answers and cross-region data movement.
- [ ] **Copilot Studio capacity** — allocate prepaid Copilot Credit capacity per environment to prevent run-away dev spend.
- [ ] **AI Builder credits** — assign capacity for prompt nodes and document processing.
- [ ] **MCP server access** — enable/restrict which clients (Copilot Studio, GitHub Copilot, Claude, etc.) can reach the Dataverse MCP endpoint (Managed Environment required).
- [ ] **Agent sharing controls** — restrict broad sharing via Managed Environments.

## ALM (parameterise everything)

- [ ] **Environment variables** for per-environment config (URLs, site addresses, feature flags) — no hardcoding.
- [ ] **Connection references** so credentials swap per environment at deploy time.
- [ ] **Pipelines** to promote dev → test → prod with approval gates; targets must be Managed Environments.

## Authentication ladder

`No auth (block in prod)` → `Entra ID` → `SSO` → **`On-behalf-of (OBO)`** → `web channel security`.
OBO is the key pattern: the agent calls downstream connectors **as the signed-in user**, so M365 permissions and RBAC apply automatically.

## Cost control (Copilot Credits)

- [ ] Estimate first with the **agent usage estimator** (type, traffic, orchestration, knowledge, tools).
- [ ] Allocate capacity per environment; remember unused credits **don't carry over** monthly.
- [ ] Design levers that move consumption: orchestration style, knowledge breadth, tool calls, autonomous runs — measure, then optimise.

## Governance recommendations (the six)

1. **DLP policies** — block sensitive data in prompts/responses; define before building.
2. **Environment strategy** — separate dev/test/prod; route makers to Managed Environments, never the default.
3. **Settings & guardrails** — disable unauthenticated access; restrict channels; limit knowledge to approved endpoints.
4. **Define responsibility** — every agent has an accountable owner for config, security and lifecycle.
5. **Scheduled reviews** — monthly/quarterly: usage, orphaned status, security posture.
6. **Governance board** — cross-functional (IT, security, business) to approve agents and set policy.
