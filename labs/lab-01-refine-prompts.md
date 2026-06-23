# Lab 1 — Refine Prompts: Agent & Topic Level

**Module 1 · Designing reliable agents · ~60 min · 3 exercises (≤20 min each)**

## Objective

Improve accuracy and consistency by tuning instructions at the **agent level** and Generative Answers at the **topic level**, then measure the difference before and after.

## Prerequisites

- Lab 0 complete (Copilot Studio trial + developer environment).
- A simple agent grounded on **one** narrow knowledge source (a SharePoint site, a couple of uploaded PDFs, or an allow-listed website). Keep the scope deliberately small.

## Background (why this matters)

Most hallucinations come from vague instructions and over-broad knowledge, not from the model. You'll apply the **Role / Objective / Tool-usage / Reasoning & grounding** instruction pattern and the **grounding & moderation dials** to make answers traceable and consistent. See [`artifacts/agent-instructions-template.md`](../artifacts/agent-instructions-template.md) and [`artifacts/grounding-moderation-checklist.md`](../artifacts/grounding-moderation-checklist.md).

---

### Exercise 1.1 — Baseline & rewrite agent instructions (20 min)

*Goal: capture a "before" and apply the four-block instruction pattern.*

1. **Baseline.** Ask your agent 5 representative questions (include 1–2 it *shouldn't* be able to answer). Save the answers — this is your "before".
2. **Rewrite agent instructions** using the template's four blocks:
   - **Role** — one clear identity and the single job it owns.
   - **Objective & task flow** — the steps; check after each tool call whether the objective is met.
   - **Tool-usage rules** — when to call which tool; "read each tool description and follow it exactly".
   - **Reasoning & grounding rules** — reason step by step; *never answer from general knowledge — always retrieve*; on error, surface and retry.

✅ **Checkpoint:** instructions now have four clearly labelled blocks and a one-line identity.

### Exercise 1.2 — Set the grounding & moderation dials (20 min)

*Goal: make answers traceable and stop fallback to general model knowledge.*

1. In **Generative AI settings**, turn on **Use only specified knowledge**.
2. Set the **Moderation level** (raise for stricter, more conservative answers).
3. Enable **Return citations**.
4. Re-ask 2–3 of your baseline questions and confirm citations now appear.

✅ **Checkpoint:** factual answers show a citation; an out-of-scope question no longer invents an answer.

### Exercise 1.3 — Per-topic instructions & compare (20 min)

*Goal: tighten one conversation path and measure the overall improvement.*

1. **Add per-topic custom instructions** to one triggered topic (Generative Answers) to tighten behaviour on that path.
2. Add an explicit **fallback** message for "no good answer found".
3. **Compare.** Re-ask the same 5 questions from Exercise 1.1. Note improved citations, fewer fabrications, and a clean "I don't know" on the out-of-scope questions.

✅ **Checkpoint:** you can point to the specific instruction block or dial that changed each behaviour.

---

## Key concepts

Agent instructions · topic-level generative answers · moderation level · grounding · "use only specified knowledge" · citations · designing for failure (explicit fallback).

## Success criteria

- [ ] Every factual answer now shows a **citation** to your source.
- [ ] Out-of-scope questions get an honest **"I can't answer that"** rather than a plausible fabrication.
- [ ] Answers to the same question are **consistent** across repeats.
- [ ] You can point to the specific instruction block that changed each behaviour.

## Stretch goals

- Reduce response length in Generative AI settings and observe the effect on quality.
- Capture your 5 questions as the seed of a **test set** you'll automate in Lab 5.

➡ Next: **[Lab 2 — Extend with Dataverse MCP & tools](lab-02-dataverse-mcp-tools.md)** · See also **[Lab 6 — the same prompt-refinement task in the new UI](lab-06-old-vs-new-ui.md)**
