# Lab 1 – Instruction Tuning & Grounding

**Module 1 · Instruction tuning & grounding · ~60 min · 4 exercises (≤20 min each)**

## Objective

Improve accuracy and consistency by tuning instructions at the **agent level** and Generative Answers at the **topic level**, then measure the difference before and after.

## Prerequisites

- Lab 0 complete (Copilot Studio trial + developer environment): <https://copilotstudio.microsoft.com>

## Background

Most hallucinations come from vague instructions and over-broad knowledge, not from the model. You'll apply the **Role / Objective / Tool-usage / Reasoning & grounding** instruction pattern and the **grounding & moderation dials** to make answers traceable and consistent. See [`artifacts/agent-instructions-template.md`](../artifacts/agent-instructions-template.md) and [`artifacts/grounding-moderation-checklist.md`](../artifacts/grounding-moderation-checklist.md).

---

### Exercise 1.1 – Start from a prompt to create an agent (15 min)

*Goal: create your first draft agent directly from a natural-language prompt*

1. Open Copilot Studio: <https://copilotstudio.microsoft.com>.
2. Create a solution before creating the agent:
   - Open **Solutions** by clicking on the three dots under **Tools** and selecting **Solutions**.
   - Select **+ New solution**.
   - Enter **Display name** (for example, `EPPC Agents` or `EPPC 2026`), then create and confirm **Publisher**.
   - Select **Create**
3. Navigate back to <https://copilotstudio.microsoft.com> and click the **settings wheel** to select your new solution. 

![alt text](../Assets/E1_1.png)

4. Use this starter prompt or use your own use case:

```text
Assist bankers in identifying, investigating, and managing potential fraud and anti-money laundering cases. Help users gather information, understand internal procedures, coordinate investigative activities, and ensure cases are handled consistently and in accordance with bank policies.

```


5. Click on the **right arrow** to create the agent. Save the generated agent and confirm your core authoring surfaces are available for editing: **Instructions**, **Knowledge**, **Tools** and **Model** etc.


**New UI equivalent (optional):** In Copilot Studio (<https://copilotstudio.microsoft.com>) -> **New experience**, you would do the same setup on the **Build** tab without the prompt to describe the agent. 

![alt text](../Assets/E1_2.png)

✅ **Checkpoint:** you have created a solution and an agent from a prompt

### Exercise 1.2 – Baseline & rewrite agent instructions (15 min)

*Goal: capture a "before" and apply the four-block instruction pattern.*

1. **Baseline.** Ask your agent 5 representative questions (include 1-2 it *shouldn't* be able to answer). Save the answers - this is your "before".
2. **Rewrite agent instructions** using the template's four blocks:
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

✅ **Checkpoint:** instructions now have four clearly labelled blocks and a one-line identity.

### Exercise 1.3 – Set the grounding & moderation dials (15 min)

*Goal: make answers traceable and stop fallback to general model knowledge.*

1. In **Generative AI settings**, turn on **Use only specified knowledge**.
2. Set the **Moderation level** (raise for stricter, more conservative answers).
3. Enable **Return citations**.
4. Re-ask 2-3 of your baseline questions and confirm citations now appear.

✅ **Checkpoint:** factual answers show a citation; an out-of-scope question no longer invents an answer.

### Exercise 1.4 – Per-topic instructions & compare (15 min)

*Goal: tighten one conversation path and measure the overall improvement.*

1. **Add per-topic custom instructions** to one triggered topic (Generative Answers) to tighten behaviour on that path.
2. Add an explicit **fallback** message for "no good answer found".
3. **Compare.** Re-ask the same 5 questions from Exercise 1.2. Note improved citations, fewer fabrications, and a clean "I don't know" on the out-of-scope questions.

✅ **Checkpoint:** you can point to the specific instruction block or dial that changed each behaviour.

---

## Key concepts

Agent instructions · prompt-first agent creation · connected-agent pattern (orchestrator + specialists) · topic-level generative answers · moderation level · grounding · "use only specified knowledge" · citations · designing for failure (explicit fallback).

## Success criteria

- [ ] Every factual answer now shows a **citation** to your source.
- [ ] Out-of-scope questions get an honest **"I can't answer that"** rather than a plausible fabrication.
- [ ] Answers to the same question are **consistent** across repeats.
- [ ] I can explain how this setup maps to the **new UI Build tab** (including **Connected agents**) and why I'd split work into specialists.
- [ ] You can point to the specific instruction block that changed each behaviour.

## Stretch goals

- Reduce response length in Generative AI settings and observe the effect on quality.
- Capture your 5 questions as the seed of a **test set** you'll automate in Lab 5.

➡ Next: **[Lab 2 – Dataverse MCP & Least-Privilege Data Access](lab-02-dataverse-mcp-least-privilege.md)** · See also **[Lab 6 – the same prompt-refinement task in the new UI](lab-06-old-vs-new-ui.md)**
