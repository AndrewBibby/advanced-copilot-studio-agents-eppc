# Lab 4 — Human-in-the-Loop Checkpoint

**Module 4 · Human-in-the-loop & orchestration · ~45 min**

## Objective

Insert a **human decision point** so the agent pauses before a critical action, using a **Request for Information (RFI)** action and an **AI Approval** stage with a human override.

## Prerequisites

- Lab 2 complete (an agent with at least one tool/action worth gating).
- Access to **Workflows** in Copilot Studio and an Outlook mailbox to receive the RFI request.

## Background (why this matters)

Automation should stop and ask a human wherever judgment must gate the process — claims triage, finance verification, quality sign-off, legal review. **RFI** pauses a workflow, emails a named reviewer, collects structured input, then resumes. **AI Approvals** auto-approve low-risk requests and escalate the rest, while a human keeps final authority with the reason captured for audit. Build HITL checkpoints around any create/update/delete the agent can perform (recall the Dataverse write tools from Lab 2).

## Tasks

1. **Create or open a Workflow** that the agent can call (use the redesigned Workflows canvas; node-level testing lets you test one step without running the whole flow).
2. **Add a Request for Information action.** Configure:
   - the named reviewer(s),
   - structured input types (text / number / email / yes-no / date; single- or multi-select; required),
   - what happens on response. Requests go via Outlook and the **first responder wins**.
3. **Branch on the response.** If approved → continue to the action (e.g. the Dataverse `create_record`/`update_record`); if rejected → stop and message the user.
4. **Add an AI Approval stage.** Give it decision criteria and inputs (a document/knowledge), let it decide *with an explanation*, auto-approve low-risk and escalate exceptions to a person.
5. **Test end-to-end.** Trigger the flow from the agent, respond to the RFI email, and confirm the branch and the captured approval explanation.

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

➡ Next: **[Lab 5 — Monitor in Copilot Studio + Agent 365, then iterate](lab-05-monitor-evaluate-iterate.md)**
