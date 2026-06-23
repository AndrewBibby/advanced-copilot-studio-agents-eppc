# Lab 5 — Monitor in Copilot Studio + Agent 365, then Iterate

**Module 5 · Test, monitor, evaluate & improve · ~60 min**

## Objective

Watch your agent the way you would in production, then run a **structured improvement loop**: analyse → adjust → re-test → ship.

## Prerequisites

- An agent you've been building through Labs 1–4 with some test traffic against it.
- Access to **Copilot Studio analytics**; access to the **Agent 365** workspace and the **Copilot Studio Kit** if available in your tenant (otherwise follow along on the shared environment).

## Background (why this matters)

Quality isn't a one-time tuning step — it's a loop. **Copilot Studio analytics** shows per-agent engagement, resolution and generated-answer rate plus transcripts; **Agent 365** is the fleet control plane (unified observability across every agent). The **Copilot Studio Kit** turns ad-hoc checks into repeatable **test sets with rubrics**, which you can wire into a CI/CD **eval gate** so regressions never reach production. The closing loop: **Analyze → Adjust → Re-test → Ship & repeat.** See [`artifacts/grounding-moderation-checklist.md`](../artifacts/grounding-moderation-checklist.md) for what to tighten when you adjust.

## Tasks

1. **Review analytics.** In your agent's **Analytics**, look at engagement, resolution rate and generated-answer rate. Open **transcripts** and find low-confidence or unanswered questions.
2. **Check the fleet view.** Open the agent in the **Agent 365** workspace and note what observability/governance it adds beyond the single-agent view (telemetry, policies, activity).
3. **Build a test set.** In the **Copilot Studio Kit**, configure your agent and a test set seeded from your Lab 1 questions. Add tests of different types (response match, topic match, generative answers).
4. **Add a rubric.** Score generative answers against a **user-defined rubric** (e.g. "cites a source", "stays in scope", "no fabrication") rather than exact-match only.
5. **Run, then iterate.** Run the batch; read the aggregates and latencies. Pick the worst-performing area and **adjust** (instructions, knowledge scope, or a tool description). **Re-test** and compare versions side by side.

## Key concepts

Copilot Studio analytics · transcripts · Agent 365 observability · Copilot Studio Kit (batch testing, test types, rubrics) · eval gates in CI/CD · the agentic improvement loop · ALM (`pac copilot-studio export/import/publish`).

## Success criteria

- [ ] You found at least one concrete gap from **transcripts/analytics**.
- [ ] You ran a **Kit test set with a rubric** and read the aggregate scores.
- [ ] You made one **targeted adjustment** and showed a measurable improvement on re-test.
- [ ] You can describe how this test set would act as an **eval gate** before publish.

## Stretch goals

- Define a pass/fail threshold and sketch the **Azure DevOps / GitHub Actions** pipeline step that would gate a release on it.
- Run a **monthly agent maintenance sprint** dry-run: inventory (PPAC / M365 registry / Agent 365) → review (orphaned, usage, security) → clean up & harden.
- Compare cost before/after your adjustment using the **Copilot Credits** view.

➡ Back to the **[agenda](../docs/agenda.md)** · or reuse the **[artifacts](../artifacts/)** in your own tenant.
