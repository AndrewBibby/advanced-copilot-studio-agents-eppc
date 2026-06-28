# Designing, Governing and Operating Advanced Copilot Studio Agents

**A full-day, Level 300 workshop – Copilot and Agentic Platforms**

[![Level](https://img.shields.io/badge/level-300%20(Advanced)-blue)](#) [![Track](https://img.shields.io/badge/track-Developer-success)](#) [![Platform](https://img.shields.io/badge/platform-Copilot%20Studio-purple)](#)

This repository contains the hands-on labs, sample artifacts and reference material for the workshop *"Designing, Governing and Operating Advanced Copilot Studio Agents."* It is aimed at technical makers, developers and solution architects who already use Copilot Studio and want to build agents that work reliably in real-world, production scenarios.

---

## About the session

**Aimed at experienced builders** who've already built agents in Copilot Studio and want to take them to production. This condensed workshop (~2.5 hours, modular) covers the full lifecycle: **design → extend → govern → keep humans in the loop → monitor & improve**.

We start with agent design – job framing and architecture decisions that set you up for success. From there, we move into instruction tuning and grounding (the knobs that reduce hallucinations), then into the production challenges: **authentication patterns, DLP governance, HITL approval gates, and continuous improvement loops**. 

A key focus is **DLP and environment security** – a governance pain point we address through a discovery-based exercise: "see the risk (no DLP) → fix it (create DLP) → verify impact (DLP blocks tools)" plus a **connector reference matrix** (10 connectors × 4 environment tiers with Clear Allow/Block/Conditional guidance). We also cover Dataverse with MCP servers, showing you how to build specialist subagents that respect RBAC through OBO authentication. The day follows the natural lifecycle of an agent – design → build → govern → test → operate.

Each lab is 20 minutes max, so there's always a clean stopping point. Labs stand alone – pick what you need for your scenario.

### Key takeaways

- **Design** agents with clear boundaries and guidance to improve accuracy and ensure consistent results.
- **Govern** – apply governance, security and human-in-the-loop patterns to run agents safely in production.
- **Operate** – use a lifecycle approach to test, monitor and continuously improve agent behaviour over time.

---

## Speakers

| | |
|---|---|
| **Cathrine Bruvold** | Head of Power Platform at Point Taken, Norway · Microsoft Business Applications MVP |
| **Andrew Bibby** | Consulting Director at Proximo 3, United Kingdom · Microsoft Business Applications MVP |

---

## Agenda

**Condensed for experienced builders: 8 focused labs (~20 min each) covering the full agent lifecycle (~2.5 hours total, modular – pick what you need).** Each lab is capped at 20 minutes. Every lab stands alone; prerequisites are listed.

| # | Module | Lab | Duration | 
|---|--------|-----|----------|
| 0 | **Setup** | [Lab 0 – Environment Setup](labs/lab-00-environment-setup.md) | ~15 min |
| 1 | **Design & Build** | [Lab 1 – Agent Design](labs/lab-01-agent-design.md) · [Lab 2 – Creating an Agent](labs/lab-02-creating-an-agent.md) | 17 + 20 = ~37 min |
| 2 | **Extend with Tools & Data** | [Lab 3 – Instruction Tuning & Grounding](labs/lab-03-instruction-tuning-grounding.md) · [Lab 4 – Subagent & Dataverse MCP](labs/lab-04-subagent-Dataverse-mcp.md) | 20 + 20 = ~40 min |
| 3 | **Govern & Secure** | [Lab 5 – Auth, DLP & Entitlement](labs/lab-05-auth-dlp-entitlement.md) | ~20 min |
| 4 | **HITL Approval Gates** | [Lab 6 – Workflow Approval Gates](labs/lab-07-workflow-approval-gates.md) | ~20 min |
| 5 | **Monitor & Improve** | [Lab 7 – Monitoring, Testing & Iteration](labs/lab-06-monitoring-testing-iteration.md) | ~20 min |
| ✦ | **Optional: UI Choice** | [Lab 8 – Old UI → New UI](labs/lab-08-old-vs-new-ui.md) | ~20 min |

> **Before you arrive:** complete **[Lab 0 – Environment Setup](labs/lab-00-environment-setup.md)** to provision a free Power Apps Developer Plan environment (with Dataverse) and a Copilot Studio trial. This takes ~20–30 minutes and removes the biggest source of delay on the day.

> **Publishing note:** only attendees using provided lab credentials can publish agents in the workshop lab environment (this is optional, not required). Attendees using their own tenant can still complete the labs, but publishing depends on their own tenant/licensing/policy setup and isn't supported by the workshop team.

> **Optional / time-permitting:** **[Lab 8 – Old UI → New UI](labs/lab-08-old-vs-new-ui.md)** is a quick concept map showing how Classic topics/triggers/flows map to the new Build, Skills and Workflows, so you can decide which experience to use for your next project.

---

## Repository map

```
advanced-copilot-studio-training/
├── README.md                  ← you are here
├── docs/
│   └── agenda.md              ← module-by-module overview & timing
├── labs/
│   ├── lab-00-environment-setup.md                    ← DO THIS FIRST (trial sign-up)
│   ├── lab-01-agent-design.md
│   ├── lab-02-creating-an-agent.md
│   ├── lab-03-instruction-tuning-grounding.md
│   ├── lab-04-subagent-Dataverse-mcp.md
│   ├── lab-05-auth-dlp-entitlement.md
│   ├── lab-07-workflow-approval-gates.md
│   ├── lab-06-monitoring-testing-iteration.md
│   └── lab-08-old-vs-new-ui.md                       ← optional: decide Classic vs. New UI
└── artifacts/                 ← copy-ready templates & checklists
    ├── agent-instructions-template.md
    ├── prompt-tool-templates.md
    ├── tool-descriptions-examples.md
    ├── grounding-moderation-checklist.md
    ├── multi-agent-orchestration-checklist.md
    └── dlp-environment-strategy-checklist.md
```

---

## How to use this repo

1. **Attendees:** start with [Lab 0](labs/lab-00-environment-setup.md) **before the workshop**. On the day, work through Labs 1–7 in sequence; each is 20 min and stands alone. Labs 3–5 are strongly recommended for governance/security best practices.
2. **Pick-and-choose:** each lab is independent (prerequisites listed in each). Skip what you know; deep-dive what's new for your scenario.
3. **Facilitators:** the [agenda](docs/agenda.md) carries timing, key concepts and module structure. The [artifacts](artifacts/) are the copy-ready templates attendees reuse during labs.
4. **After the day:** the artifacts are a starter kit for your own production agents – reuse the instruction template, the orchestration checklist and the DLP/environment strategy guidance in your own tenant.

---

## Prerequisites at a glance

- A **workshop-provided Microsoft Entra login** (default and supported path).
- **Experienced-user exception:** you may use your own work login if you already have Power Apps, Copilot Studio, and a developer environment with Dataverse in your work tenant.
- For the own-tenant path, **personal email accounts** (outlook.com, gmail.com, etc.) are not supported by the sign-up flows; see **Lab 0** for details and alternatives.
- If you choose your own work login/environment, workshop support is limited for tenant-specific issues.
- A modern browser (Chrome 91+, Edge, Firefox 89+, or Safari 16.4+).
- Completion of **Lab 0** – a Power Apps Developer Plan environment with Dataverse, plus a Copilot Studio trial.

---

## Notes on platform versions

Copilot Studio shipped a significantly redesigned authoring experience in 2026 (new building blocks – **Skills**, **Workflows** and **Connected agents** – replacing Topics, Agent Triggers and Child agents; generative orchestration by default; a new Memory feature). The labs note where the **New UI** and the **Classic UI** differ so you can follow along whichever experience your tenant defaults to. There is currently **no supported migration path** between Classic and New – see the module notes for detail.

---

## License

Released under the [MIT License](LICENSE). Workshop content © Cathrine Bruvold & Andrew Bibby. "Copilot Studio", "Power Platform", "Dataverse", "Microsoft Foundry" and related names are trademarks of Microsoft.
