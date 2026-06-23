# Lab 3 — Secure Agent Tools & Connections

**Module 3 · Governing & securing agents · ~60 min**

## Objective

Lock down **how your agent authenticates** and **which tools it can reach**, so users only ever see data they're entitled to.

## Prerequisites

- Lab 2 complete (agent with a Dataverse tool).
- Admin access to the **Power Platform admin center (PPAC)** for the dev environment, or use the shared lab tenant.

## Background (why this matters)

"No authentication" is the fastest demo and the worst production choice. The authentication ladder runs **No auth → Entra ID → SSO → On-behalf-of (OBO) → web channel security**, and OBO is the key pattern for secure tool access — the agent calls downstream connectors *as the signed-in user*, so existing M365 permissions and RBAC apply automatically. **DLP** then governs which connectors and endpoints the agent can touch at all. See [`artifacts/dlp-environment-strategy-checklist.md`](../artifacts/dlp-environment-strategy-checklist.md).

## Tasks

1. **Require authentication.** In the agent's **Settings → Security**, disable unauthenticated access and require **Microsoft Entra ID** authentication.
2. **Configure On-behalf-of.** For a connector your agent uses, configure **OBO** so calls run as the signed-in user. Verify a low-privilege test user sees fewer rows than an admin for the same question.
3. **Apply DLP.** In **PPAC → Policies → Data policies**, confirm/define a policy for the environment that:
   - Blocks connectors the agent doesn't need,
   - Uses **endpoint filtering** to restrict a connector (e.g. SharePoint) to approved sites/URLs only.
4. **Restrict channels & knowledge.** Limit publishing channels and restrict knowledge sources to approved endpoints (block public web / Bing where not needed).
5. **Verify entitlement.** Sign in as the low-privilege user and confirm the agent **cannot** surface data that user has no rights to. Capture the before/after.

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
