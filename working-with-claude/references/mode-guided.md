# Mode: Guided

For a builder learning and running the whole loop for the first time — or one whose build is
becoming a mess and needs the process introduced from where they are. Walk the loop, explaining the
why at each stage, and point to the tool for each. The goal: they can run the loop themselves on the
next feature.

Load `references/core-principles.md`, `references/the-loop.md`, and `references/tools.md` alongside
this file.

## Posture

Teaching and reassuring. A non-technical builder often feels the process is "too much engineering."
Lead with *why* each stage saves them pain (a spec stops Claude guessing; review catches bugs cheap;
one-feature-at-a-time prevents the mess they may already be in). Recommend the tools, but make clear
the loop is the durable part and the tools are swappable. Keep it concrete — tie everything to their
actual feature.

## The flow

Walk the loop on **one real feature** of theirs, so it's concrete, not abstract:

1. **Spec** — describe the feature; introduce SDD and Spec Kit; produce and confirm the spec.
2. **Context** — set up or update CLAUDE.md (`/init`); explain why persistent memory matters.
3. **Plan → tasks** — turn the spec into a plan and tasks; approve them (a planning session).
4. **Build** — implement the *one* feature; have Claude narrate; hold the line against scope creep.
5. **Test** — have Claude write and run tests; explain why "it ran once" isn't enough.
6. **Verify** — run it and see it work; agree the success signal.
7. **Review** — `/code-review`, the PR review, `/security-review` for sensitive parts; fix findings.
8. **Refine** — UI audit (impeccable + web-design-guidelines) and the best-practice skills; then loop
   back for the next feature.

## Checkpoints

At each stage, name the **owner's checkpoint** (from `the-loop.md`) and make sure they do it — the
process only works if the owner stays in the loop, not just Claude. The two non-negotiables to drill:
*explain before execute* and *one feature at a time, verified*.

## If the build is already a mess

Start where they are, don't demand a restart. Introduce the loop from the next feature forward:
"let's not fix everything at once — let's build the *next* thing properly, with a spec and a review,
and stop the pile from growing." Retrofitting tests/specs onto past features can come later.

## Close

Deliver the **Output always includes** set from SKILL.md. Leave them able to run the loop on the next
feature alone. Hand to `/technical-decisions` for choices that arise, and `/tools-setup` for any tool
that needs account-level setup.
