# Lab 3 — Secure Agent Tools & Connections

**Module 3 · Governing & securing agents · ~60 min · 3 exercises (≤20 min each)**

## Objective

Lock down **how your agent authenticates** and **which tools it can reach**, so users only ever see data they're entitled to.

## Prerequisites

- Lab 2 complete (agent with a Dataverse tool).
- Admin access to the **Power Platform admin center (PPAC)** for the dev environment, or use the shared lab tenant.

## Background (why this matters)

"No authentication" is the fastest demo and the worst production choice. The authentication ladder runs **No auth → Entra ID → SSO → On-behalf-of (OBO) → web channel security**, and OBO is the key pattern — the agent calls downstream connectors *as the signed-in user*, so existing M365 permissions and RBAC apply automatically. **DLP** then governs which connectors and endpoints the agent can touch at all. See [`artifacts/dlp-environment-strategy-checklist.md`](../artifacts/dlp-environment-strategy-checklist.md).

---

### Exercise 3.1 — Require auth & configure On-behalf-of (20 min)

*Goal: force Entra sign-in and make tool calls run as the user.*

1. In the agent's **Settings → Security**, disable unauthenticated access and require **Microsoft Entra ID** authentication.
2. For a connector your agent uses, configure **On-behalf-of (OBO)** so calls run as the signed-in user.
3. Note a test question you'll re-run as a low-privilege user in Exercise 3.3.

✅ **Checkpoint:** the agent requires Entra sign-in; a connector is set to OBO.

### Exercise 3.2 — Apply DLP & endpoint filtering (20 min)

*Goal: restrict which connectors/endpoints the agent can reach.*

1. In **PPAC → Policies → Data policies**, confirm/define a policy for the environment that **blocks connectors the agent doesn't need**.
2. Apply **endpoint filtering** to restrict a connector (e.g. SharePoint) to approved sites/URLs only.
3. Block public web / Bing knowledge where it isn't needed.

✅ **Checkpoint:** a DLP policy with endpoint filtering is applied to the environment.

### Exercise 3.3 — Restrict channels & verify entitlement (20 min)

*Goal: prove the agent honours user permissions.*

1. Limit publishing channels and restrict knowledge sources to approved endpoints.
2. Sign in as a **low-privilege test user** and re-run the question from Exercise 3.1.
3. Confirm the agent **cannot** surface data that user has no rights to. Capture before/after.

✅ **Checkpoint:** a low-privilege user is demonstrably blocked from data they shouldn't see.

---

## Key concepts

Microsoft Entra ID · SSO · on-behalf-of (OBO) · DLP policies · endpoint filtering · channel restrictions · least privilege · M365 permission inheritance · Entra Agent ID.

## Success criteria

- [ ] Unauthenticated access is **off**; the agent requires Entra sign-in.
- [ ] A connector runs **on-behalf-of** the user and respects their permissions.
- [ ] A **DLP policy with endpoint filtering** is applied to the environment.
- [ ] A low-privilege user is demonstrably **blocked** from data they shouldn't see.

## Stretch goals

- Map the **four-tier environment strategy** (Dev / Test / Internal Prod / External Prod) to your own org and note the DLP differences — especially the **Direct Line** conflict for external-facing agents.
- Estimate the agent's **Copilot Credits** with the usage estimator and identify the biggest cost lever.
- Enable a **Managed Environment** sharing control and observe what it prevents.

➡ Next: **[Lab 4 — Human-in-the-loop checkpoint](lab-04-human-in-the-loop.md)**
