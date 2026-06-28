# Lab 6 – Workflow Approval Gates: HITL for Critical Actions

**Module 6 · Human-in-the-loop (HITL) approval gates · ~20 min · 1 exercise**

## Objective

Wire a **workflow approval gate** so the agent pauses before a critical write action and waits for human review before proceeding.

## Prerequisites

- Lab 4 complete (an agent with a Dataverse MCP tool that can create/update records).
- Access to **Workflows** in Copilot Studio and an Outlook mailbox to receive approval requests.

## Background

Any create/update/delete the agent performs should have a **human checkpoint** — either pre-approval or post-audit, depending on risk. The **Request for Information (RFI)** action is a workflow node that pauses, emails a named reviewer, collects structured input, and resumes when approved. This is the simplest HITL pattern: agent → workflow → human approval → write.

---

### Exercise 6.1 – Build and test an approval gate workflow (20 min)

*Goal: create a workflow the agent can invoke that pauses for human approval.*

1. **Create the workflow:**
   - Open **Flows** → **New workflow** (redesigned canvas).
   - Name it `Account Write Approval`.
   - Add input parameters: `accountName` (text), `accountIndustry` (text), `requestedBy` (email).

2. **Add the approval gate:**
   - Insert a **Request for Information** action.
   - Configure:
     - **Reviewer:** your email (or a test reviewer)
     - **Input fields:** 
       - `Approve account creation?` (Yes/No)
       - `Comments?` (text, optional)
     - **Timeout:** 1 hour (default)
   - The RFI pauses the workflow and sends an email to the reviewer with the structured input form.

3. **Branch on the response:**
   - Add a **Condition** after the RFI: `If response == Yes`
   - **Yes branch:** Call **Dataverse connector** → Create a record in Accounts table with the inputs.
   - **No branch:** Stop and return "Request rejected."
   - Capture the reviewer's comments in the final response message for audit.

4. **Test end-to-end:**
   - Publish the workflow.
   - Go to your agent, manually trigger the workflow by calling it with test parameters (or add it as an agent tool).
   - Check your Outlook: you should receive an RFI email with the Yes/No buttons and comment field.
   - Click **Approve** → the workflow continues, creates the account, and returns success to the agent.
   - (Optional) Test **Reject** to confirm the No branch works.

✅ **Checkpoint:** The workflow pauses for human approval; the account write only happens on approval; the reviewer's response and comments are captured for audit.

---

## Why this matters: HITL (Human-In-The-Loop)

- **Automation ≠ full autonomy.** Writes (create/update/delete) should have a human gate, especially when money, contracts, or compliance are involved.
- **RFI is the minimal HITL.** Email approval form, first responder wins, structured input, audit trail. No fancy AI approval needed—the human is the decider.
- **Async approval.** The workflow pauses; the human reviews on their schedule; the workflow resumes when they respond. The agent doesn't block.

---

## Key concepts

Request for Information (RFI) · human-in-the-loop (HITL) · approval branching · structured input · audit trail · workflow gates · async approval.

## Success criteria

- [ ] Workflow pauses and **sends an RFI email** to a human.
- [ ] The flow **branches correctly** on approve (create) vs. reject (stop).
- [ ] **Comments are captured** from the reviewer for audit.
- [ ] The agent can **invoke the workflow** and show the approval outcome.

## Stretch goals

- Add a second reviewer and observe **first-responder-wins** behaviour (first approval ends the flow).
- Add a **timeout** and handle the "no response after 24 hours" case (auto-reject or escalate).
- Wire the **approval outcome back into the agent's reply** so the end user sees "Your account request was approved on [date] by [reviewer]."
- Explore **AI Approvals** to auto-approve routine requests and escalate exceptions.

➡ Next: **[Lab 7 – Monitoring, Testing & Iteration](lab-06-monitoring-testing-iteration.md)** · See also **[Lab 8 – the same HITL task in the new UI](lab-07-old-vs-new-ui.md)**
