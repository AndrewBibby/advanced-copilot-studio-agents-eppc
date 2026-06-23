# Lab 4 — Workflow Approval Gates

**Module 4 · Workflow approval gates · ~45 min · 3 exercises (≤20 min each)**

## Objective

Insert a **workflow decision point** so the agent pauses before a critical action, using a **Request for Information (RFI)** action and an **AI Approval** stage with a human override.

## Prerequisites

- Lab 2 complete (an agent with at least one tool/action worth gating).
- Access to **Workflows** in Copilot Studio and an Outlook mailbox to receive the RFI request.

## Background (why this matters)

Automation should stop and ask for review wherever judgment must gate the process — claims triage, finance verification, quality sign-off, legal review. **RFI** pauses a workflow, emails a named reviewer, collects structured input, then resumes. **AI Approvals** auto-approve low-risk requests and escalate the rest, while a human keeps final authority with the reason captured for audit. Build checkpoints around any create/update/delete the agent can perform (recall the Dataverse write tools from Lab 2).

---

### Exercise 4.1 — Build a workflow with a Request for Information (20 min)

*Goal: pause automation and ask a named human.*

1. Open **Flows** → create a **New workflow** (the redesigned canvas with node-level testing) the agent can call.
2. Add a **Request for Information** action. Configure:
   - the named reviewer(s),
   - structured input types (text / number / email / yes-no / date; single- or multi-select; required),
   - what happens on response. Requests go via Outlook and the **first responder wins**.
3. Test just that node to confirm the email is sent.

✅ **Checkpoint:** the workflow pauses and sends an RFI email to a human.

### Exercise 4.2 — Branch on the human response (15 min)

*Goal: route the flow on approve vs reject.*

1. Add a condition on the RFI response.
2. **Approved →** continue to the gated action (e.g. the Dataverse `create_record`/`update_record`).
3. **Rejected →** stop and message the user.

✅ **Checkpoint:** the gated write only happens on the approved branch.

### Exercise 4.3 — Add an AI Approval stage & test end-to-end (15 min)

*Goal: auto-handle the routine, escalate the exceptions, keep a human override.*

1. Add an **AI Approval** stage: give it decision criteria and inputs (a document/knowledge), let it decide *with an explanation*, auto-approve low-risk and escalate exceptions to a person.
2. Trigger the flow from the agent, respond to the RFI email, and confirm the branch and the captured approval explanation.

✅ **Checkpoint:** the AI Approval records a reason/explanation for audit, and a human can override.

---

## Key concepts

Request for Information (RFI) · structured inputs · AI Approvals · multi-stage routing · human override · escalation · Express Mode (2-minute limit) · node-level testing.

## Success criteria

- [ ] The workflow **pauses** and sends an RFI to a human before the gated action.
- [ ] The flow **branches correctly** on approve vs. reject.
- [ ] The AI Approval stage records a **reason/explanation** for audit.
- [ ] The gated Dataverse write only happens **after** approval.

## Stretch goals

- Add a second reviewer and observe first-responder-wins behaviour.
- Add an "ask vs. inform" follow-up and note the difference (ask = two-way and waits; inform = one-way).
- Wire the approval outcome back into the agent's reply so the user sees the decision and reason.

➡ Next: **[Lab 5 — Monitoring, Testing & Iteration](lab-05-monitoring-testing-iteration.md)** · See also **[Lab 6 — the same HITL task in the new UI](lab-06-old-vs-new-ui.md)**
