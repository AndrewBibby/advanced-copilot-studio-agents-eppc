# Lab 6 – Monitoring, Testing & Iteration

**Module 5 · Agent testing, evaluation & operations · ~20 min · 2 exercises (10 min each)**

## Objective

**Test the agent you built** with concrete pass/fail criteria, then think operationally: how will you maintain agents at scale in your organization?

## Prerequisites

- You've completed Labs 1–5 and have a working agent with instructions, knowledge, tools, and ideally a HITL (Human-in-the-Loop) gate.
- You have the agent available to test interactively in the Copilot Studio preview pane.
- Familiarity with your organization's software delivery and governance structures.

## Background

**Testing agents is not optional.** Before any agent goes to production, you need answers to:
1. **Does it answer correctly?** (Does it hallucinate? Does it go out of scope? Does it miss the mark?)
2. **Does it follow the rules you set?** (Does it respect the HITL gate? Does it stay within knowledge boundaries?)
3. **Is it consistent?** (Ask the same question 3 times – do you get the same answer?)

Once it's live, the second big question is: **Who owns maintaining it?** Agents don't stay static. They need review, version control, incident handling, and periodic cleanup.

---

### Exercise 7.1 – Build and run a concrete test baseline (10 min)

*Goal: establish pass/fail criteria for your agent before it goes anywhere.*

1. **Define 3–5 test questions** that represent the core jobs your agent should do. Write them down. Example:

   - Q1: "Can the agent answer a basic policy question correctly?" (Expected: Yes, agent cites the handbook section.)
   - Q2: "Does the agent refuse to answer out-of-scope questions?" (Expected: Agent says "I can't help with that.")
   - Q3: "If the HITL gate is on, does it pause for approval?" (Expected: Agent sends RFI email, pauses.)
   - Q4: "Is the same answer consistent across 2 back-to-back questions?" (Expected: Same substance, similar phrasing.)

2. **Run each test and document the result** (5 min):
   - Open your agent in **Preview**.
   - Ask Q1. Copy the response verbatim. Mark: ✓ Pass / ✗ Fail / ? Needs clarification.
   - Repeat for Q2, Q3, Q4.
   - For consistency tests (Q4), ask the same question twice and compare.

   **Simple test log:**
   ```
   Test ID | Question | Expected | Actual | Pass/Fail | Notes
   Q1      | Policy question? | Cites handbook | ✓ Correct, cited section 2.1 | ✓ PASS |
   Q2      | Out-of-scope? | Refuses politely | ✓ Refused, offered help with... | ✓ PASS |
   Q3      | HITL gate? | Pauses for approval | ? Didn't see RFI email | ? NEEDS SETUP |
   Q4a     | Same Q twice | Consistency | ✓ Both said "policy is X" | ✓ PASS |
   Q4b     | Same Q again | Consistency | ✓ Same answer as Q4a | ✓ PASS |
   ```

3. **Set your pass/fail gate** (documents what "ready for Test" looks like):
   - **Minimum to pass:** All quality tests (Q1, Q2) pass. Consistency tests show no contradictions.
   - **Nice to have:** HITL gate works (if you built one). Agent stays on-topic 100% of the time.
   - **Blocker:** If any quality test fails, agent doesn't go to Test environment. Fix it first.

✅ **Checkpoint:** You have a documented baseline test. You know what "passing" looks like. You can say: *"I tested my agent against 5 concrete questions. 4/5 passed. Blocker: HITL gate setup – need to fix before Test environment."*

---

### Exercise 7.2 – Design how you'll operate agents at scale (10 min)

*Goal: think operationally – who owns it, how do you maintain it, when do you retire it?*

Answer these 3 questions for your organization:

**1. Ownership & Escalation** (3 min)
- **Who owns this agent?** (Name, team, role)
- **If something goes wrong, who do users contact?** (Support ticket? Slack channel? Direct to owner?)
- **Who retires the agent** if it stops being useful? (Owner? Manager? Compliance team?)

**2. Maintenance Sprint** (4 min)
- **How often do you review agents?** (Monthly? Quarterly?)
- **What triggers a review?** (Usage drops? High error rate? Cost spike? User complaints?)
- **What does a maintenance sprint look like?** (Example: Review transcripts, check cost, run your baseline tests again, decide: keep/improve/retire.)

**3. Version Control & Audit** (3 min)
- **How do you track changes?** (Solution export history? GitHub? Spreadsheet?)
- **Can you answer "who changed the instructions and when?"** a year from now?
- **How long do you keep agent versions before deleting?**

**Example maintenance sprint checklist:**

```
Monthly Agent Maintenance Sprint – [Agent Name]

1. USAGE REVIEW (5 min)
   ☐ How many users this month? (Trend up/down?)
   ☐ Any support tickets? (If >2, investigate)
   ☐ Cost trending? (If >50% over budget, audit knowledge/tools)

2. QUALITY CHECK (10 min)
   ☐ Re-run your 5 baseline tests – still passing?
   ☐ Spot-check 3 random transcripts – any issues?
   ☐ Any instruction/knowledge updates needed?

3. DECISION GATE (5 min)
   ☐ KEEP: No changes needed. Schedule next review.
   ☐ IMPROVE: Minor updates to instructions/knowledge. Re-test before pushing to Prod.
   ☐ RETIRE: Agent isn't being used. Turn it off and archive.
```

✅ **Checkpoint:** You've documented who owns your agent and what a monthly maintenance check looks like. Your team knows: "We review agents monthly. If usage drops below X or costs exceed Y, we escalate to [owner]. If consensus is no longer useful, we retire it on [date]."

---

## Key concepts

Agent testing · baseline test questions · pass/fail criteria · HITL gate validation · consistency testing · agent ownership · escalation SLA · maintenance sprint · version control · retirement decision.

## Success criteria

**Exercise 7.1 (Testing):**
- [ ] You defined **3–5 concrete test questions** that represent your agent's core job.
- [ ] You **ran each test** and documented pass/fail results.
- [ ] You established a **pass/fail gate** (e.g., "all quality tests must pass before moving to Test environment").
- [ ] You identified any blockers (HITL not working? Out-of-scope answers?) before production.

**Exercise 7.2 (Operational Model):**
- [ ] You documented **who owns** your agent (name, team, role).
- [ ] You defined the **escalation path** (if something breaks, who gets contacted and when?).
- [ ] You sketched a **monthly maintenance sprint** checklist (usage review, quality check, decision gate).
- [ ] You answered: **Can you version/audit changes to this agent?** (How?)

## Stretch goals

- Run your baseline tests **3 times on different days** to detect consistency issues.
- Build a **"Definition of Ready" checklist** before an agent enters Test environment (e.g.: Baseline tests pass ☐ · HITL gate validated ☐ · Instructions audited ☐ · DLP policy set ☐).
- Create a **Runbook for agent incidents** – if the agent breaks at 2 AM, what's the 15-minute action plan? (Revert? Update? Notify users? Pause?)
- Set up a **simple agent dashboard** (owner, status, cost, last maintenance date, next review) that your team updates monthly.
- Establish a **version control system** for agents (GitHub, solution exports, or spreadsheet) so you can answer "who changed what and when" a year from now.

➡ **[Back to the agenda](../docs/agenda.md)** · **[Artifacts library](../artifacts/)** for checklists & templates
