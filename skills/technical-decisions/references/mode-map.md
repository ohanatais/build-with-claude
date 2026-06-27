# Mode: Map

For when the owner is about to start (or restart) a build and wants to see the technical
decisions coming, so none of them ambush mid-build. The job: lay out the decisions this
specific product will hit, flag which are one-way doors, and let the owner pre-think the ones
that matter.

Load `references/core-principles.md` and `references/decisions.md` alongside this file.

## Posture

Calm and orienting. The owner isn't deciding everything now — they're getting a map so the
build feels less like a series of surprises. Reassure that most decisions are two-way doors
they can approve quickly; the point of the map is to spotlight the *few* that deserve thought
up front.

## The flow

1. **Understand the product in 2–3 sentences** — what it does, for whom, and the rough shape
   (a content site, a data-heavy tool, something real-time, something with payments). The
   shape determines which decisions are live and which don't apply.
2. **List the decisions this build will actually hit** — pull the relevant cards from
   `references/decisions.md`. Skip what's irrelevant (a simple site may never need its own
   API; a free tool may skip payments). Don't dump the whole catalog — curate to the product.
3. **Sort by reversibility** — clearly separate:
   - **Decide-with-care (one-way doors):** data model, auth provider, anything with money or
     stored personal data, the core framework. Flag these as the ones worth a real
     conversation before building.
   - **Wave-through (two-way doors):** styling, component choices, email/analytics tools, most
     UI. Reassure these can be approved fast and changed later.
4. **For each one-way door, plant the question** — the one or two things the owner should have
   an answer to before that decision arrives (from the card's "before you approve"). They
   don't have to answer now; they just shouldn't be blindsided.
5. **A rough order** — which decisions tend to come first (data model and auth usually early,
   since much hangs off them; domain/deploy nearer launch).

## Output

- **The product, one paragraph.**
- **Decisions ahead**, grouped into *decide-with-care* and *wave-through*, each with a
  one-line "what it is."
- **The questions to pre-think** for the one-way doors.
- **A rough sequence** so the owner knows what's coming when.
- **Next step:** start the build; pull `/technical-decisions` in **explain** or **review** mode
  when each real decision lands, and `/tools-setup` when it's time to set a tool up.

## The reassurance to leave them with

Most of this build is two-way doors — which means moving fast is usually the right call, and
careful attention is reserved for a handful of choices. Knowing *which* handful is the whole
advantage. The owner should leave the map feeling oriented, not overwhelmed.
