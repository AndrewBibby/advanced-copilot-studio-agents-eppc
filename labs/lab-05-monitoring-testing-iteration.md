# Lab 5 – Monitoring, Testing & Iteration

**Module 5 · Monitoring, testing & iteration · ~60 min · 3 exercises (≤20 min each)**

## Objective

Watch your agent the way you would in production, then run a **structured improvement loop**: analyse → adjust → re-test → ship.

## Prerequisites

- An agent you've been building through Labs 1–4 with some test traffic against it.
- Access to **Copilot Studio analytics**; access to the **Agent 365** workspace and the **Copilot Studio Kit** if available in your tenant (otherwise follow along on the shared environment).

## Background

Quality isn't a one-time tuning step – it's a loop. **Copilot Studio analytics** shows per-agent engagement, resolution and generated-answer rate plus transcripts; **Agent 365** is the fleet control plane. The **Copilot Studio Kit** turns ad-hoc checks into repeatable **test sets with rubrics**, which you can wire into a CI/CD **eval gate** so regressions never reach production. The closing loop: **Analyze → Adjust → Re-test → Ship & repeat.**

---

### Exercise 5.1 – Review analytics, transcripts & the fleet view (20 min)

*Goal: find a concrete gap from real signals.*

1. In your agent's **Analytics**, review engagement, resolution rate and generated-answer rate.
2. Open **transcripts** and find low-confidence or unanswered questions; note one gap to fix.
3. Open the agent in the **Agent 365** workspace and note what observability/governance it adds beyond the single-agent view (telemetry, policies, activity).

✅ **Checkpoint:** you've identified at least one concrete gap to improve.

### Exercise 5.2 – Build a test set with a rubric (20 min)

*Goal: make quality measurable and repeatable.*

1. In the **Copilot Studio Kit**, configure your agent and a test set seeded from your Lab 1 questions.
2. Add tests of different types (response match, topic match, generative answers).
3. Add a **rubric** to score generative answers (e.g. "cites a source", "stays in scope", "no fabrication") rather than exact-match only.

✅ **Checkpoint:** a rubric-scored test set runs and produces aggregate scores.

### Exercise 5.3 – Run, adjust & re-test (20 min)

*Goal: close the loop with a measurable improvement.*

1. Run the batch; read the aggregates and latencies.
2. Pick the worst-performing area and **adjust** one thing (instructions, knowledge scope, or a tool description).
3. **Re-test** and compare versions side by side.

✅ **Checkpoint:** one targeted change shows a measurable improvement on re-test.

---

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
