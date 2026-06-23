# Lab 1 — Refine Prompts: Agent & Topic Level

**Module 1 · Designing reliable agents · ~60 min**

## Objective

Improve accuracy and consistency by tuning instructions at the **agent level** and Generative Answers at the **topic level**, then measure the difference before and after.

## Prerequisites

- Lab 0 complete (Copilot Studio trial + developer environment).
- A simple agent grounded on **one** narrow knowledge source (a SharePoint site, a couple of uploaded PDFs, or an allow-listed website). Keep the scope deliberately small.

## Background (why this matters)

Most hallucinations come from vague instructions and over-broad knowledge, not from the model. You'll apply the **Role / Objective / Tool-usage / Reasoning & grounding** instruction pattern and the **grounding & moderation dials** to make answers traceable and consistent. See [`artifacts/agent-instructions-template.md`](../artifacts/agent-instructions-template.md) and [`artifacts/grounding-moderation-checklist.md`](../artifacts/grounding-moderation-checklist.md).

## Tasks

1. **Baseline.** Ask your agent 5 representative questions (include 1–2 it *shouldn't* be able to answer). Record the answers — this is your "before".
2. **Rewrite agent instructions** using the template's four blocks:
   - **Role** — one clear identity and the single job it owns.
   - **Objective & task flow** — the steps; check after each tool call whether the objective is met.
   - **Tool-usage rules** — when to call which tool; "read each tool description and follow it exactly".
   - **Reasoning & grounding rules** — reason step by step; *never answer from general knowledge — always retrieve*; on error, surface and retry.
3. **Set the grounding dials** in Generative AI settings:
   - Turn on **Use only specified knowledge** (don't fall back to general model knowledge).
   - Set the **Moderation level** (raise for stricter, more conservative answers).
   - Enable **Return citations**.
4. **Add per-topic custom instructions** to one triggered topic (Generative Answers) to tighten behaviour on a specific conversation path.
5. **Compare.** Re-ask the same 5 questions. Note improved citations, fewer fabricated answers, and a clean "I don't know" on the out-of-scope questions.

## Key concepts

Agent instructions · topic-level generative answers · moderation level · grounding · "use only specified knowledge" · citations · designing for failure (explicit fallback).

## Success criteria

- [ ] Every factual answer now shows a **citation** to your source.
- [ ] Out-of-scope questions get an honest **"I can't answer that"** rather than a plausible fabrication.
- [ ] Answers to the same question are **consistent** across repeats.
- [ ] You can point to the specific instruction block that changed each behaviour.

## Stretch goals

- Add a fallback message for "no good answer found".
- Reduce response length in Generative AI settings and observe the effect on quality.
- Capture your 5 questions as the seed of a **test set** you'll automate in Lab 5.

➡ Next: **[Lab 2 — Extend with Dataverse MCP & tools](lab-02-dataverse-mcp-tools.md)**
