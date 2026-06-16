# Core Principles

Loaded for every working-with-claude session. The mindset that makes building with Claude Code
produce something you understand and can evolve — not a black box that rots.

## Explain before you execute

The highest-leverage habit for a non-technical owner: have Claude explain *what* it's about to do
and *why* before it does it, and approve with understanding. This costs a few minutes and saves
weeks. An owner who understood each step can catch a wrong turn, answer "should we change this?"
later, and brief the next session. An owner who waved everything through is a passenger. Ask Claude
explicitly: "before you build this, tell me what you're going to do, why, and what the alternatives
were."

## Planning sessions vs. execution sessions

Treat planning and building as *different sessions* with different mindsets.

- **Planning session:** decide what to build and how — the spec, the architecture, the task
  breakdown. No code yet. The goal is a plan the owner understands and approves.
- **Execution session:** build the approved plan. The goal is to implement what was decided, not
  to re-litigate it.

Blurring the two — deciding and building in one breathless go — is how scope creeps and the owner
loses the thread. Separating them keeps the owner in control of *what* gets built before *how*
swallows the conversation.

## One feature at a time, verified before the next

The single habit that most separates a clean build from a mess: build **one feature**, verify it
works, *then* start the next. Never let Claude emend the next feature onto an unverified one,
because when something breaks you won't know which change caused it, and unverified work piles up
into a tangle no one can debug. A validation checkpoint after each feature — the owner actually
seeing it work — is the brake that keeps the build under control.

## A spec keeps Claude building the right thing

Claude is excellent at building; it can only guess at *what* you meant. A short spec — what you're
building, for whom, and why this version — removes the guessing. Spec-driven development isn't
bureaucracy for a solo builder; it's the difference between Claude implementing your intent and
Claude implementing its best guess at your intent. The spec is also what lets you say "that's not
what I asked for" with something concrete to point at.

## Persistent context is what makes session two as good as session one

Without a memory, every session starts cold and Claude re-derives (and re-decides) things you
already settled. A **CLAUDE.md** file — the project's persistent context: stack, conventions,
decisions, how you like to work — is read every session and keeps the build consistent over time.
Keep it updated as real decisions are made; stale context is its own kind of bug. This is the
cheapest, highest-return file in the whole project.

## Tests and review are guardrails, not ceremony

A non-technical owner is tempted to skip tests and review ("it works, ship it"). They're not
overhead — they're how you find out something is wrong *while it's cheap to fix*, and how you keep
a future change from silently breaking a past feature. You don't write tests or do reviews by hand;
you have Claude do them and you insist they happen. Treat "it built" and "it ran once" as *not yet
done* — done is tested, reviewed, and verified.

## Read along, even without reading code

You don't need to read code to follow what Claude is building. You can follow the *plan* (the spec
and tasks), the *story* of each change ("I added X so that Y"), and the *verification* (seeing it
work). Ask Claude to narrate what it's doing in plain language. Following along is what lets you
steer — a build you're not following is a build you've handed off entirely.

## When it breaks, localize — don't panic

Things break; it's normal and not a verdict on you. The useful response is to treat breakage as
information about *which* part has a problem (the spec? a specific feature? the data? the deploy?).
The most helpful thing you can give Claude is a precise "I did X, expected Y, saw Z" — that
localizes the problem far faster than "it's all broken." Calm and specific beats panicked and
vague, every time.

## Recommend tools, explain why, let the builder adapt

This skill points to strong public tools, but the goal is never blind ceremony. Explain *why* each
stage matters — once a builder understands why a spec, a review, or a UI audit earns its keep,
they'll keep doing it and adapt the tools to their stack. A process followed by rote is abandoned
the first time it's inconvenient; a process understood is kept. The loop is the principle; the
tools are how you currently run it.
