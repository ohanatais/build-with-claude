---
name: working-with-claude
description: >
  The process of building a product with Claude Code, for a non-technical builder — the
  pipeline from spec to shipped: spec-driven development, persistent project context, building
  feature by feature with validation checkpoints, git and branches, testing, running and
  verifying, code and PR review, and refining both code and UI. It's a conductor: it teaches
  the loop and points to the recommended public tools (GitHub Spec Kit, impeccable, the Vercel
  and Supabase skills, and Claude Code's built-in review commands) to install and use at each
  stage — it recommends and references them, it does not replace them.

  Make sure to use this skill whenever the user invokes /working-with-claude or is asking how
  to actually *work* with Claude Code to build something, not what to build — "what's the
  process / workflow", "how do I build this without it becoming a mess", "what's spec-driven
  development", "how do I set my project up before coding", "planning session vs execution
  session", "how do I do feature-by-feature", "how do I review / test / refine with Claude",
  "how do I keep Claude on track across sessions", or "Claude built the wrong thing, how do I
  structure this". Also trigger when a build is about to start and the owner needs the working
  method, not the next feature.

  Do NOT use for: explaining a specific technical decision or tradeoff (use
  /technical-decisions); setting up a specific tool's account and connection (use /tools-setup);
  or product, brand, and go-to-market work (those have their own skills). This skill is the
  *process* of building with Claude Code, and the toolkit that supports it.
---

# Working with Claude Code

Claude Code can build your product. Whether what comes out is something you understand, can
maintain, and can evolve — or an accumulating mess — depends almost entirely on the *process*
you build it with. Most non-technical builders don't have a process, so they get the mess: one
giant request, no spec, no review, no idea what changed, and a product that's hard to touch a
month later.

This skill is the process. It teaches the **build loop** — from describing what you want to
shipping it — and points you to the proven, public tools that support each stage. Think of it as
a conductor: it doesn't replace the tools; it tells you which to install and when to use each, so
a non-technical builder can run a real engineering workflow without being an engineer.

## Language rule

**Always respond in the user's language.** If the user writes in Portuguese (including
Brazilian Portuguese), explain the whole process in Portuguese. The point of this skill is to
make a professional build process accessible; a second language is one more barrier it should
remove.

## A conductor, not a copy — install the real tools

The stages below lean on excellent open-source and built-in tools. This skill **references and
recommends** them; it never copies their content. Where a stage names a tool, the move is to
*install that tool* (links in `references/tools.md`) and use it — they're maintained by their
authors and far better than anything reinvented here. The tools are recommendations you can
swap; the *loop* is the durable part.

## The build loop (one feature at a time)

The whole method, in one picture. You run this loop **per feature**, not once for the whole
product — building one feature at a time is the single most important habit.

```
1. Spec        →  Describe what & why before any code (spec-driven development)
2. Context     →  Persistent project memory so Claude is consistent across sessions (CLAUDE.md)
3. Plan → tasks→  Turn the spec into an architecture and a task breakdown before building
4. Build       →  Implement one feature at a time, with a validation checkpoint before the next
5. Test        →  Tests as a guardrail; know what "it works" means, provably
6. Verify      →  Run it and see it work — "you'll know it works when…"
7. Review      →  Code review during, multi-agent PR review + security review before merge
8. Refine      →  Tighten the code, and refine the UI (design review) before it ships
   → then loop back to 1 for the next feature
```

Why a loop and why per-feature: a spec keeps Claude building the right thing; review and tests
catch what goes wrong; refining before the next feature stops mess from compounding. Asking Claude
for ten features at once skips all the checkpoints and is how builds rot.

Load `references/core-principles.md` for the working mindset (explain-before-execute, planning vs
execution sessions, reading along, what to do when it breaks). Load `references/the-loop.md` for
each stage in depth, and `references/tools.md` for the recommended tools to install.

## Entry point: where is the user?

**Signal 1 — starting a project?** They want the whole method and the tools set up. → **setup**
mode (scaffold the process) or **guided** mode (learn it as they go).

**Signal 2 — mid-build, at a specific stage?** "I have a spec, now what?" / "how do I do the
review part?" → **stage** mode for that stage.

**Signal 3 — the build is becoming a mess?** No process yet, features piling up, nothing
reviewed. → **guided** mode to introduce the loop, starting from where they are.

Route:

| Mode | When | Reference |
|---|---|---|
| **guided** | Learning and running the whole loop, first project | `references/mode-guided.md` |
| **setup** | Scaffold the process and install the recommended tools for a project | `references/mode-setup.md` |
| **stage** | At a specific point in the loop and wants help with that stage | `references/mode-stage.md` |

If unsure, ask: "Are you setting up a new project's process, learning the whole workflow, or at a
specific point and want help with that stage?"

## How each stage works (the short version)

**1. Spec.** Describe *what* you're building and *why* before any code — **spec-driven development
(SDD)**. The recommended tool is **GitHub Spec Kit**, which turns this into structured steps
(specify → clarify → plan → tasks → implement). A spec is what keeps Claude building the right
thing instead of guessing.

**2. Context.** Give the project a persistent memory — a **CLAUDE.md** file Claude reads every
session — so decisions, stack, and conventions don't reset each time. Claude Code can scaffold one
with `/init`. This is what makes session two as informed as session one.

**3. Plan → tasks.** Before building, have Claude turn the spec into a technical plan and a task
breakdown, and *approve them* — this is a planning session, separate from execution. Spec Kit's
plan/tasks steps do exactly this.

**4. Build feature by feature.** Implement one feature, then **stop and validate it works** before
starting the next. Never let Claude emend the next feature onto an unverified one. This single
habit prevents most compounding mess.

**5. Test.** Tests are how you *know* something works and stays working, not just that it ran once.
You don't write them by hand — you have Claude write them — but you insist they exist for anything
that matters, as a guardrail against future changes silently breaking things.

**6. Verify.** Run the product and see the feature work, with a concrete success signal. "It
built" is not "it works." Verifying each feature is your checkpoint as the owner.

**7. Review.** Before merging a feature: a **code review** (Claude Code's built-in `/code-review`),
a **multi-agent PR review** across security, quality, architecture, performance, and regressions,
and a dedicated **security review** (`/security-review`) for anything touching auth, data, or
money. Review is not optional ceremony — it's where problems are caught cheaply.

**8. Refine.** Tighten the code (review passes, the Vercel and Supabase best-practice skills for
React/Next and database work), and **refine the UI** with a design review — **impeccable**
(`/audit`, `/polish`) and **web-design-guidelines** — so what ships doesn't look like generic AI
output. Then loop back to the spec for the next feature.

## Universal by design — the loop is fixed, the tools are yours

The *loop* (spec → context → plan → build → test → verify → review → refine) is the durable,
universal part — it's how disciplined software gets built, whoever you are. The *tools* are strong
recommendations, not requirements: Spec Kit, impeccable, the Vercel and Supabase skills, and the
built-in review commands are excellent defaults, but a builder can swap any of them for an
equivalent and the loop still holds. Recommend the proven tools, explain *why* each stage matters,
and let the builder adapt the toolkit to their stack and taste. Never make the process feel like a
rigid ceremony — explain the why, and the discipline follows.

## Output always includes

1. **The loop, oriented to where they are** — which stage they're at and what comes next.
2. **The recommended tool for the stage(s) in play** — named, with how to install it (from
   `references/tools.md`) and how a non-developer uses it.
3. **What to actually do next** — the concrete next action in their build.
4. **The owner's checkpoint** — what *they* should verify or approve at this stage (validation,
   review sign-off), since the process only works if the owner stays in the loop.
5. **Next step** — the next stage, or back to the spec for the next feature. Hand to
   `/technical-decisions` when a real choice arises mid-loop, and `/tools-setup` when a tool needs
   account-level setup.

## The posture that matters most

The two habits that save a non-technical build: **explain before execute** (understand each step
before approving it) and **one feature at a time, verified** (never pile the next on an
unverified last). Everything else in the loop serves those two. A builder who holds them — even
loosely — ends up with a product they understand and can evolve, instead of a black box they're
afraid to touch.
