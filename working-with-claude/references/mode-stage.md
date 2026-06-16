# Mode: Stage

For a builder who is mid-build, at a specific point in the loop, and wants help with *that stage* —
"I have a spec, now what?", "how do I do the review part?", "Claude built it, how do I verify?". The
job: locate them in the loop, run that stage well, and point to the next.

Load `references/core-principles.md`, `references/the-loop.md`, and `references/tools.md` alongside
this file.

## Posture

Quick and located. Don't re-teach the whole loop — find where they are, do that stage properly, and
set them up for the next. Pull the matching section from `the-loop.md` for the method, and name the
tool for that stage from `tools.md`. Always include the **owner's checkpoint** for the stage so they
don't skip their part.

## The flow

1. **Locate them.** Which stage are they at? (spec / context / plan-tasks / build / test / verify /
   review / refine). If they're unsure, the symptom usually tells you: "Claude's building the wrong
   thing" → spec; "it works but looks rough" → refine; "I'm scared to merge" → review.
2. **Run that stage** using its section in `the-loop.md`: what to do, the recommended tool (link it
   from `tools.md`), and how a non-dev runs it.
3. **Do the owner's checkpoint.** Make sure they perform their part — approve the spec, see it work,
   confirm the security review ran. The stage isn't done until the owner's checkpoint is met.
4. **Point to the next stage** — and, after refine, back to the spec for the next feature.

## Common stage-specific help

- **"I have a spec, now what?"** → plan → tasks (Spec Kit), approve them, then build the one feature.
- **"Claude built it, how do I know it's good?"** → verify (run it, see it work) → review
  (`/code-review`, PR review, `/security-review` if sensitive).
- **"How do I make it not look like generic AI UI?"** → refine: run **impeccable** `/audit` and
  **web-design-guidelines**, apply findings.
- **"It broke."** → localize: "what did you do, expect, and see?" Identify the stage that owns the
  problem; fix the one thing; re-verify.
- **"Claude keeps adding stuff I didn't ask for."** → you skipped or lost the spec/scope; pull back to
  the approved tasks and the one-feature-at-a-time rule.

## Close

Finish the stage with its owner-checkpoint met, name the next stage and the tool for it, and offer
**guided** mode if they want to learn the whole loop rather than stage-by-stage. Route real decisions
to `/technical-decisions` and account-level tool setup to `/tools-setup`.
