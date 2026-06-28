# Lab 5 – DLP & Entitlement: See the Risk, Then Lock It Down

**Module 5 · DLP governance & OBO authentication · ~20 min · 1 exercise**

## Objective

See how open your environment is (no DLP = full connector freedom), create a restrictive DLP policy, watch it block tools in your agent, then configure OBO so the agent respects user permissions.

## Prerequisites

- Lab 4 complete (agent with a Dataverse subagent and MCP tools).
- Admin access to the **Power Platform admin center (PPAC)** and your agent's editor.

## Background

**The pain:** Environments are too open by default. Makers can add any connector—HTTP, Bing, external APIs—without restriction. **The fix:** Design DLP policies with a "block everything, allow-list only what you need" mindset. **The key pattern:** On-behalf-of (OBO) authentication means the agent calls connectors *as the signed-in user*, so existing M365 and Dataverse RBAC apply automatically. Together, DLP + OBO = least privilege.

See [`artifacts/dlp-environment-strategy-checklist.md`](../artifacts/dlp-environment-strategy-checklist.md) for the full governance framework.

⚠️ **Important:** Just because there's no DLP blocking a connector doesn't mean your agent should use it. In dev, you have the freedom to add any tool, but you still need to follow least-privilege principles yourself. If you add HTTP, Bing, or SharePoint to an agent that only needs Dataverse, you've created an unnecessary attack surface—even if DLP isn't enforcing it. **Design for least privilege; DLP is the safety net, not the primary defense.**

---

### Exercise 5.1 – Audit, restrict, and verify (20 min)

*Goal: see the risk of an open environment, apply DLP, and watch your agent's tool options shrink.*

**Part A – See the risk (5 min):**

1. Go to **Power Platform admin center → Policies → Data policies** for your environment.
2. Check if a **Data Loss Prevention (DLP) policy** is already applied. If not, you're seeing the default state: **no restrictions**. Any maker can use any connector.
3. Note: Your agent can currently add HTTP, Bing, Skills, external web APIs, SharePoint, Teams—everything.

**Part B – Create a restrictive DLP policy (7 min):**

1. In **PPAC → Policies → Data policies**, select **New Policy**.
2. Name it (e.g., `Dev - Dataverse Only`).
3. Under **Connectors**, use the **Block all** approach:
   - Add **Dataverse** to the **Allow** list.
   - Add **Teams** and **SharePoint** to the **Allow** list *only if* your agent uses them for knowledge or connectors.
   - **Block everything else** (HTTP, Bing, Skills, preview connectors, external web APIs).
4. Add **endpoint filtering** to SharePoint (if allowed) to restrict it to approved sites only.
5. **Save and apply** the policy to your environment.

**Part C – See the impact in your agent (5 min):**

1. Go back to your agent → **Tools → Add tool**.
2. Try to add **HTTP** or **Bing** — you should see them **unavailable, blocked by DLP**.
3. Try to add **Dataverse MCP** — still available (in allow list).
4. Notice: Your agent's freedom has shrunk to exactly what it needs. This is intentional and good.

**Part D – Configure OBO on Dataverse connector (3 min):**

1. In your agent, find the **Dataverse MCP connector** (or any Dataverse tool).
2. Open its settings and set authentication to **On-behalf-of (OBO)**.
3. This means: the agent calls Dataverse *as the signed-in user*, so if you can't access a record, the agent can't either. No extra permission grants needed; RBAC is automatic.
4. Test: Ask the agent a data question and confirm it returns rows you have access to.

✅ **Checkpoint:** DLP policy is applied and blocks unnecessary connectors; agent's tool options reflect the restricted set; Dataverse connector is OBO-authenticated.

---

## Why this matters: Separate environments & separate DLPs

- **Dev environment** (this one): Loose for makers to iterate, but *still* restricted to avoid defaults (Dataverse only, block HTTP/Bing).
- **Test environment**: Production-equivalent DLP + read-only Dataverse + no external publishing.
- **Internal Prod**: Strict DLP, OBO on all connectors, audit logging enabled.
- **External Prod** (if needed): Separate tier with Direct Line allowed (isolated from tenant policy), stricter knowledge scoping, dedicated capacity.

The *same* DLP policy cannot safely cover both dev makers and external-facing agents. That's why you need separate environments—each with its own DLP posture, matching its audience and risk.

---

## Common pitfalls & things to remember

- **DLP is environment-scoped, not agent-scoped.** The policy affects *all* agents in that environment. Don't assume it's protecting only one agent.
- **Managed Environment must be on *before* adding MCP.** If you add MCP first, then enable Managed Environment, the tools can disappear. Order matters.
- **OBO doesn't work on all connectors.** HTTP, Bing, Skills, and preview connectors often don't support On-behalf-of. Using them means shared/admin credentials—you lose user permission inheritance. Choose intentionally.
- **Policy promotions fail silently.** An agent works in Dev (loose DLP), but breaks in Test (strict DLP) because a tool is blocked. Always run **Solution Checker** before promoting to a stricter environment.
- **Start restrictive, add only what works.** Don't start with "allow everything" and hope to tighten later. By then, 20 agents are using HTTP incidentally. Begin with Dataverse-only, test thoroughly, then add connectors.
- **Audit logging isn't on by default.** If something breaks, you have no trail. Enable it or document why you haven't.
- **Align DLP across tiers, document the gaps.** Dev can be looser than Test/Prod, but those gaps should be intentional and documented.

---

## Connector reference matrix for Copilot Studio

Use this matrix to decide what to allow and block in your DLP policies. Start with the strict baseline; add only what your agent actually needs.

### Default recommendations by environment tier

| Connector | Dev | Test | Internal Prod | External Prod | Notes |
|-----------|-----|------|---------------|---------------|-------|
| **Dataverse** | ✅ Allow | ✅ Allow | ✅ Allow | ✅ Allow | Primary data source; always required |
| **SharePoint** | ✅ Allow (any site) | ⚠️ Filtered | ⚠️ Filtered | ⚠️ Filtered (external sites only) | Use endpoint filtering to restrict to approved sites |
| **Teams** | ✅ Allow | ⚠️ Allow | ⚠️ Read-only | ❌ Block | User context; tighten read-only in Prod |
| **Outlook / OneDrive** | ✅ Allow | ⚠️ Allow | ⚠️ Allow | ❌ Block | For user identity/context; not needed externally |
| **HTTP** | ❌ Block | ❌ Block | ❌ Block | ❌ Block | Use specific certified connectors instead |
| **Bing / Web Search** | ❌ Block | ❌ Block | ❌ Block | ❌ Block | Uncontrolled knowledge; no RBAC |
| **Skills / Direct connector** | ❌ Block | ❌ Block | ❌ Block | ❌ Block | Hard to audit; use certified connectors |
| **Social media** (Twitter, FB) | ❌ Block | ❌ Block | ❌ Block | ❌ Block | Data exfiltration risk |
| **Preview connectors** | ⚠️ Allow (controlled) | ❌ Block | ❌ Block | ❌ Block | Dev only; audit before using |
| **Custom connectors** | ⚠️ Allow (reviewed) | ❌ Block | ❌ Block (unless approved) | ❌ Block | Requires explicit approval & audit trail |

**Legend:**  
✅ Allow  |  ⚠️ Conditional / filtered  |  ❌ Block

### Why the tiers differ

- **Dev**: Makers iterate; some looseness acceptable. Still block HTTP, Bing, Skills to enforce good habits.
- **Test**: Mirrors Prod to catch agent failures early. Endpoint filtering enforced; no global SharePoint access.
- **Internal Prod**: RBAC enforced, OBO required, audit logging on. No external data sources.
- **External Prod**: Isolated from tenant policy (Direct Line allowed here). No internal SharePoint/Teams. Stricter knowledge scoping. Dedicated capacity.

### How to apply endpoint filtering (example: SharePoint)

If your agent needs SharePoint for knowledge:
1. Add **SharePoint** to Allow list
2. Click **Endpoint filtering** 
3. Select **Approved sites** 
4. Add specific site URLs (e.g., `https://contoso.sharepoint.com/sites/KnowledgeBase`)
5. Block everything else

This prevents the agent from accessing personal OneDrive files or unrelated sites.

---

## Key concepts

DLP policies · block-all mindset · endpoint filtering · On-behalf-of (OBO) authentication · RBAC inheritance · least privilege · four-tier environment strategy · connector scoping.

## Success criteria

- [ ] You've seen the **default open state** (no DLP = all connectors available).
- [ ] You've created a **restrictive DLP policy** (block all except Dataverse + essentials).
- [ ] Blocked connectors (HTTP, Bing) are now **unavailable in the agent's tool picker**.
- [ ] Dataverse connector is set to **On-behalf-of** authentication.
- [ ] Test confirms the agent respects your Dataverse access level.

## Stretch goals

- Compare your current DLP policy to a **Test environment policy** — what's tighter in Test? (Hint: no HTTP, no external web, solution checker enforced.)
- Map the **four-tier strategy** to your org: where do you need Direct Line, and does it conflict with tenant DLP?
- Document the **exception list** — if you had to allow SharePoint or Teams, what endpoints and why?

➡ Next: **[Lab 6 – Workflow Approval Gates](lab-06-workflow-approval-gates.md)**
