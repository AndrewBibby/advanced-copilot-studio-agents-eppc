# Lab 3 – Instruction Tuning & Grounding

**Module 3 · Instruction tuning & grounding · ~20 min · 2 exercises (≤10 min each)**

## Objective

Improve accuracy and consistency by applying the four-block instruction pattern at the **agent level** and configuring grounding dials, then observe the difference.

## Prerequisites

- Lab 1 complete (agent designed): [Lab 1 – Designing an Agent for a Use Case](lab-01-agent-design.md)
- Lab 2 complete (agent created): [Lab 2 – Creating an Agent](lab-02-creating-an-agent.md)

## Background

Most hallucinations come from vague instructions and over-broad knowledge, not from the model. You'll apply the **Role / Objective / Tool-usage / Reasoning & grounding** instruction pattern and the **grounding & moderation dials** to make answers traceable and consistent. See [`artifacts/agent-instructions-template.md`](../artifacts/agent-instructions-template.md) and [`artifacts/grounding-moderation-checklist.md`](../artifacts/grounding-moderation-checklist.md).

---

### Exercise 2.1 – Rewrite agent instructions using the four-block pattern (10 min)

*Goal: apply the four-block instruction pattern to your agent and capture a "before vs after".*

1. **Baseline.** Ask your agent 3 representative questions (include 1 it *shouldn't* be able to answer). Save the answers – this is your "before".
2. **Rewrite agent instructions** using the four blocks:
   - **Role** - one clear identity and the single job it owns.
   - **Objective & task flow** - the steps; check after each tool call whether the objective is met.
   - **Tool-usage rules** - when to call which tool; "read each tool description and follow it exactly".
   - **Reasoning & grounding rules** - reason step by step; *never answer from general knowledge - always retrieve*; on error, surface and retry.

   **Example** (for the fraud/AML use case):
   ```
   **ROLE**
   You are a Fraud & AML Case Assistant. Your single job is to help compliance officers investigate and document suspected fraud and money laundering cases according to bank policies.

   **OBJECTIVE & TASK FLOW**
   1. When a user reports a case, retrieve the relevant case details and policies from the knowledge base.
   2. Guide the user through the investigation workflow (evidence gathering, risk assessment, escalation decision).
   3. After each retrieval, confirm whether we have enough information to move to the next step. If not, ask clarifying questions.
   4. When complete, summarize findings and next steps with citations to policy.

   **TOOL-USAGE RULES**
   - Use SearchCases to find existing cases (never reason about case history from memory).
   - Use CompliancePolicy to retrieve procedures (read the policy exactly; do not paraphrase or generalize).
   - Use DocumentEvidence to log investigation steps (always log before proceeding to the next step).
   - Do not use general knowledge to advise on AML thresholds or regulatory requirements—retrieve them.

   **REASONING & GROUNDING RULES**
   - Always retrieve the specific bank policy for each investigative step before advising.
   - Never answer "I think this should be escalated" without first retrieving the escalation criteria.
   - If a tool returns no results, surface the gap ("I cannot find a matching policy for this scenario") and ask the user to confirm the case details or context.
   - On error, retry the search with refined criteria and explain what you tried.
   ```

3. Re-ask the same 3 questions and note the difference in response quality and consistency.

✅ **Checkpoint:** instructions have four clearly labelled blocks; responses are more consistent and traceable.

### Exercise 2.2 – Set grounding dials & verify citations (10 min)

*Goal: make answers traceable and stop fallback to general model knowledge.*

1. In **Generative AI settings**, turn on **Use only specified knowledge**.
2. Set the **Moderation level** (raise for stricter, more conservative answers).
3. Enable **Return citations**.
4. Add an explicit **fallback** message for "no good answer found" in a Generative Answers topic.
5. Re-ask your 3 baseline questions and confirm citations now appear. Confirm the out-of-scope question returns an honest "I can't answer that" rather than a fabricated answer.

✅ **Checkpoint:** factual answers show a citation; an out-of-scope question no longer invents an answer.

---

## Key concepts

Four-block instruction pattern · agent-level instructions · topic-level generative answers · moderation level · grounding · "use only specified knowledge" · citations · designing for failure (explicit fallback).

## Success criteria

- [ ] Every factual answer now shows a **citation** to your source.
- [ ] Out-of-scope questions get an honest **"I can't answer that"** rather than a plausible fabrication.
- [ ] Answers to the same question are **consistent** across repeats.
- [ ] You can point to the specific instruction block that changed each behaviour.

## Stretch goals

- Reduce response length in Generative AI settings and observe the effect on quality.
- Capture your 3 questions as the seed of a **test set** you'll automate in [Lab 7 – Monitoring, Testing & Iteration](lab-06-monitoring-testing-iteration.md).

➡ Next: **[Lab 4 – Dataverse MCP & Least-Privilege Data Access](lab-03-dataverse-mcp-least-privilege.md)** · See also **[Lab 8 – the same prompt-refinement task in the new UI](lab-07-old-vs-new-ui.md)**
