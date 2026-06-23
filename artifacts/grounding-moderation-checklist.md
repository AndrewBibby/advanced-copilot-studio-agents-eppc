# Grounding & moderation checklist

The levers that cut hallucinations on day one. Work top to bottom — most wins come from **scoping knowledge narrowly** before touching anything else.

## Scope the knowledge

- [ ] Define the knowledge base **narrowly** — one clear source per job. Narrow scope = fewer wrong answers.
- [ ] Verify retrieval returns the *right* chunk before tuning prompts. Wrong/too-broad knowledge defeats the best instructions.
- [ ] Match the **source to the question** — SharePoint/OneDrive (permission-respecting docs), uploaded docs (safest), public web/Bing (block by default or allow-list), Azure AI Search (large corpora), Dataverse (structured data).
- [ ] Endpoint-filter SharePoint to **approved sites** only.

## Set the dials (Generative AI settings)

- [ ] **Use only specified knowledge** = ON — stop fallback to general model knowledge for factual questions.
- [ ] **Moderation level** set deliberately — raise for stricter, more conservative answers; lower for broader generative coverage. Tune per use case.
- [ ] **Return citations** = ON — show sources with every generated answer.
- [ ] **Response length** set to match the use case (short keeps agents concise; long for detailed how-tos).

## Instructions

- [ ] Add "**cite your source**" to agent instructions.
- [ ] "**Never answer factual questions from general knowledge — always retrieve.**"
- [ ] Add **per-topic custom instructions** to tighten specific conversation paths.
- [ ] Define an explicit **fallback** for "no good answer found" — an honest "I don't know" beats a plausible fabrication.

## Defeating over-summarisation

*Symptom:* the agent summarises instead of citing; answers feel plausible but can't be traced.

- [ ] Narrow knowledge scope to approved sources (overlapping sources cause averaging).
- [ ] Enable **Return citations**.
- [ ] Use a **custom prompt tool** for retrieval-heavy answers.

## Before you ship

- [ ] Build a **test set** (seed it from real questions) and add a regression check for every instruction change.
- [ ] Include **out-of-scope** questions in the test set and confirm an honest refusal.
- [ ] Re-test after each change; compare before/after.
