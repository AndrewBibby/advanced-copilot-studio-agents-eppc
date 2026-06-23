# Prompt-tool templates

A **Prompt Tool** is a named, reusable LLM call you build in the prompt builder and expose as a tool. The orchestrator decides when to invoke it based on its **name and description** — so write those carefully, or the tool never fires.

> Limits to remember: prompt tools **can't be called from Classic topics**, and each has **one output variable**.

---

## Anatomy of a prompt tool

| Field | Guidance |
|---|---|
| **Name** | Verb-led and specific: `summarise_support_ticket`, not `helper`. |
| **Description** | The single most important field — the orchestrator reads it to decide when to call. State *what it does*, *what inputs it needs*, and *when to use it*. |
| **Inputs** | Define each with a clear name and type. Keep to what's needed. |
| **Output** | One output variable. Name it for what it contains. |
| **Model & temperature** | Lower temperature for consistency; raise for creative drafting. |
| **Instructions** | The prompt itself — same Role/Objective discipline as the agent template. |

---

## Template 1 — Summarise

```text
Name: summarise_{{thing}}
Description: Summarises a {{thing}} into {{N}} bullet points covering
{{aspects}}. Use when the user asks for a summary, recap, or "TL;DR" of a
{{thing}}. Requires the full {{thing}} text as input.

Inputs:  source_text (string)
Output:  summary (string)

Instructions:
Summarise the {{thing}} in {{source_text}} into {{N}} concise bullet points.
Cover {{aspects}}. Do not add information that is not present in the source.
If the source is empty or unreadable, return "No content to summarise."
```

## Template 2 — Classify / route

```text
Name: classify_{{item}}
Description: Classifies a {{item}} into one of: {{A}}, {{B}}, {{C}}. Use to
decide routing before taking an action. Requires the {{item}} text.

Inputs:  item_text (string)
Output:  category (string)

Instructions:
Read {{item_text}} and return exactly one of: {{A}}, {{B}}, {{C}}.
Return only the category word, nothing else. If unsure, return "{{C}}".
```

## Template 3 — Extract structured fields

```text
Name: extract_{{record}}_fields
Description: Extracts {{field list}} from free text. Use before creating or
updating a record. Requires the raw text.

Inputs:  raw_text (string)
Output:  extracted (string, JSON)

Instructions:
From {{raw_text}}, extract: {{field list}}. Return a single JSON object with
those keys. Use null for any field not found. Do not invent values.
```

---

## If a prompt tool never fires

It's almost always the **description**. Make it specific and unambiguous about *when* to call it and *what* it needs. Vague descriptions = never called; precise descriptions = reliable execution.
