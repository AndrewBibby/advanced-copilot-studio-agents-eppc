# Designing, Governing and Operating Advanced Copilot Studio Agents

**A full-day, Level 300 workshop – Copilot and Agentic Platforms**

[![Level](https://img.shields.io/badge/level-300%20(Advanced)-blue)](#) [![Track](https://img.shields.io/badge/track-Developer-success)](#) [![Platform](https://img.shields.io/badge/platform-Copilot%20Studio-purple)](#)

This repository contains the hands-on labs, sample artifacts and reference material for the workshop *"Designing, Governing and Operating Advanced Copilot Studio Agents."* It is aimed at technical makers, developers and solution architects who already use Copilot Studio and want to build agents that work reliably in real-world, production scenarios.

---

## About the session

This full-day workshop is aimed at technical makers, developers and solution architects who already use Copilot Studio and want to build agents that work reliably in real-world scenarios. We start with agent design – prompt guidance, context management and grounding techniques that reduce hallucinations and improve consistency from day one – so attendees leave with design patterns they can apply immediately.

From there we move into the challenges that appear once agents leave the demo stage and reach production. Based on real-world projects, we cover authentication and authorisation, cost control and usage limits, and how to design effective human-in-the-loop flows. You will also learn how to use Dataverse with an MCP server, and how to bring services like Microsoft Foundry and Azure AI Search into Copilot Studio in a controlled, practical way. The day follows the natural lifecycle of an agent – design → testing → operation → evaluation.

The workshop is structured into clear modules, each supported by hands-on labs and guided exercises. Labs cover instruction tuning and grounding, Dataverse MCP access, identity and DLP controls, workflow approval gates, and monitoring plus iterative improvement.

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

Every lab is split into **short exercises of no more than 20 minutes each**, so you always have a clean stopping point.

| # | Module | Lab | Duration | Exercises |
|---|--------|-----|----------|-----------|
| – | New Copilot Studio UI – changes & new features | – | 15 min | – |
| 01 | [Designing reliable agents](docs/agenda.md#module-1) | [Lab 1 – Instruction Tuning & Grounding](labs/lab-01-instruction-tuning-grounding.md) | 60 min | 3 × 20 min |
| 02 | [Extending agents – tools & data](docs/agenda.md#module-2) | [Lab 2 – Dataverse MCP & Least-Privilege Data Access](labs/lab-02-dataverse-mcp-least-privilege.md) | 75 min | 4 × ≤20 min |
| 03 | [Governing & securing agents](docs/agenda.md#module-3) | [Lab 3 – Authentication, DLP & Entitlement](labs/lab-03-auth-dlp-entitlement.md) | 60 min | 3 × 20 min |
| 04 | [Workflow checkpoint & orchestration](docs/agenda.md#module-4) | [Lab 4 – Workflow Approval Gates](labs/lab-04-workflow-approval-gates.md) | 45 min | 3 × ≤20 min |
| 05 | [Test, monitor, evaluate & improve](docs/agenda.md#module-5) | [Lab 5 – Monitoring, Testing & Iteration](labs/lab-05-monitoring-testing-iteration.md) | 60 min | 3 × 20 min |
| ✦ | Old UI → New UI (cross-cutting) | [Lab 6](labs/lab-06-old-vs-new-ui.md) | 60 min | 3 × ≤20 min |

> **Before you arrive:** complete **[Lab 0 – Environment Setup](labs/lab-00-environment-setup.md)** to provision a free Power Apps Developer Plan environment (with Dataverse) and a Copilot Studio trial. This takes ~20–30 minutes and removes the biggest source of delay on the day.

> **Publishing note:** only attendees using provided lab credentials can publish agents in the workshop lab environment (this is optional, not required). Attendees using their own tenant can still complete the labs, but publishing depends on their own tenant/licensing/policy setup and isn't supported by the workshop team.

> **Optional / time-permitting:** **[Lab 6 – Old UI → New UI](labs/lab-06-old-vs-new-ui.md)** re-creates Lab 1 and Lab 4 in the new agent experience so attendees see exactly how the new Build surface, Skills and Workflows map to the Classic topics/flows they already know.

---

## Repository map

```
advanced-copilot-studio-training/
├── README.md                  ← you are here
├── docs/
│   └── agenda.md              ← module-by-module overview & timing
├── labs/
│   ├── lab-00-environment-setup.md     ← DO THIS FIRST (trial sign-up)
│   ├── lab-01-instruction-tuning-grounding.md
│   ├── lab-02-dataverse-mcp-least-privilege.md
│   ├── lab-03-auth-dlp-entitlement.md
│   ├── lab-04-workflow-approval-gates.md
│   ├── lab-05-monitoring-testing-iteration.md
│   └── lab-06-old-vs-new-ui.md         ← redo Lab 1 & Lab 4 in the new UI
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

1. **Attendees:** start with [Lab 0](labs/lab-00-environment-setup.md) **before the workshop**. On the day, work through Labs 1–5 in order; each maps to the module being presented.
2. **Facilitators:** the [agenda](docs/agenda.md) carries timing and the key concepts behind each module. The [artifacts](artifacts/) are the copy-ready material attendees reuse during labs.
3. **After the day:** the artifacts double as a starter kit for your own production agents – reuse the instruction template, the orchestration checklist and the DLP/environment strategy in your own tenant.

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
