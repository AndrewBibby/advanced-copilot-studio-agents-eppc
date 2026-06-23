# Multi-agent orchestration checklist

Ten rules that keep delegation clean, plus a ship-ready checklist. The central idea is the **Single Response Principle**: only ONE agent — the parent — talks to the user per turn. Sub-agents are researchers, not responders.

## When to split one agent into many

Split when a single agent has **too many tools (~30–40+)** and can't reliably pick the right one. First **improve the tool descriptions**; only split if routing still fails. Don't split just because you can.

- **Child agents** share the parent's context — best for tight, internal logic.
- **Connected agents** are standalone, independently governed, invoked as tools — best for shared, reusable capabilities or multi-team ownership.
- **Hybrid** — inline children for custom logic + connected agents for shared capabilities.

## The ten rules

1. **Single Response Principle** — tell the parent: "you are the only agent that talks to the user; combine all child findings into one reply."
2. **Sub-agents declare their role** — "you are a sub-agent; do NOT reply to the user — return findings to the parent."
3. **Strong, unambiguous language** — use MUST / NEVER / ONLY. Avoid soft phrasing.
4. **One knowledge source per sub-agent** — distinct, non-overlapping (CA-1 = HR, CA-2 = IT).
5. **Accurate & distinct descriptions** — the parent routes on descriptions; make each specific and unique.
6. **Parent defines the pattern** — invoke → wait for all → combine → deliver exactly one response.
7. **Pass "no direct reply" in the task** — when delegating, include "return findings only; do not reply to the user."
8. **No catch-all routing rules** — scope each rule to its domain; no broad fallback that swallows specialist queries.
9. **Test with domain-mismatch queries** — ask off-domain questions; verify graceful "both found nothing".
10. **Prefer ask over inform for follow-ups** — "ask" is two-way and waits; "inform" sends the reply back as a brand-new query.

## Ship-ready checklist

- [ ] Parent instructions state "only I respond to the user".
- [ ] Every sub-agent says "do not reply to the user directly".
- [ ] Instructions use strong directive language (MUST, NEVER, ONLY).
- [ ] Each sub-agent has a unique, non-overlapping knowledge source.
- [ ] Sub-agent descriptions are accurate, distinct and specific.
- [ ] Parent defines the full pattern (invoke → wait → combine → respond).
- [ ] Parent passes "no direct reply" in the delegated task context.
- [ ] No catch-all routing rules that swallow other agents' queries.
- [ ] Tested with domain-mismatch queries.
- [ ] Ask vs. inform distinction is correct in sub-agent instructions.

## Remember

- **Specialists over generalists** — scope each agent to a clear job; easier to test, troubleshoot and improve.
- **Architecture over prompts** — when prompts get long, that's a signal to split the agent, not to add more instructions.
- **Design for handoffs** — clean handoff points so work flows between specialists without dropping context.
- **Governance and ownership** — every agent needs an accountable owner for its whole lifecycle.
