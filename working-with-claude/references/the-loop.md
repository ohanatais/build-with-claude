# The Build Loop, Stage by Stage

The per-feature loop in depth. Load when a session reaches the depth of a stage. Each stage gives:
what it is, why it matters, the recommended public tool (install details in `references/tools.md`),
how a non-developer runs it, and the **owner's checkpoint** — what *you* verify or approve.

Run this loop **per feature**, then return to stage 1 for the next.

## Contents
- [1. Spec](#1-spec)
- [2. Context (CLAUDE.md)](#2-context)
- [3. Plan → tasks](#3-plan--tasks)
- [4. Build feature by feature](#4-build-feature-by-feature)
- [5. Test](#5-test)
- [6. Verify](#6-verify)
- [7. Review](#7-review)
- [8. Refine (code + UI)](#8-refine)

---

## 1. Spec

**What.** A short description of the feature: what it does, for whom, and why this version — before
any code. **Why.** It's what keeps Claude building your intent instead of its best guess, and gives
you something concrete to point at when it's off.

**Recommended tool: GitHub Spec Kit** — spec-driven development with structured steps (`specify →
clarify → plan → tasks → implement`). Its *specify* step produces the feature spec; *clarify*
surfaces the ambiguities you didn't notice.

**How a non-dev runs it.** Describe the feature in plain language; let Spec Kit's specify/clarify
turn it into a spec and ask you the clarifying questions. Answer them — that's the design work.

**Owner's checkpoint:** read the spec back. Does it describe what you actually want? Are the
out-of-scope parts named? Don't move on until the spec is right — everything downstream inherits it.

---

## 2. Context

**What.** A **CLAUDE.md** file holding the project's persistent memory: stack, conventions,
decisions, and how you like to work. **Why.** Claude reads it every session, so session two is as
informed as session one and you stop re-explaining and re-deciding.

**Recommended tool: Claude Code's `/init`** scaffolds a CLAUDE.md from your project; you refine it.

**How a non-dev runs it.** Run `/init` early. Then keep it current: when a real decision is made
("we're using X because Y"), add it. Add your working preferences too (e.g. "explain before
executing; build one feature at a time").

**Owner's checkpoint:** does CLAUDE.md reflect the real, current state and your way of working? A
stale context file quietly misleads every session.

---

## 3. Plan → tasks

**What.** Turning the spec into a technical plan (architecture, the pieces) and a task breakdown —
*before* building. **Why.** It's a planning session: you approve *how* it'll be built before code
starts, separately from execution, so scope doesn't creep mid-build.

**Recommended tool: Spec Kit's `plan` and `tasks` steps**, which generate exactly these from the
spec.

**How a non-dev runs it.** Have Claude produce the plan and tasks, and ask it to explain the plan in
plain language and the tradeoffs (use `/technical-decisions` for any real choice). Approve before
building.

**Owner's checkpoint:** do you understand the plan well enough to approve it? Is the task list the
*smallest* set that delivers this feature, not a wish list?

---

## 4. Build feature by feature

**What.** Implement *one* feature from the tasks, then stop. **Why.** Building one at a time with a
checkpoint before the next is the habit that most prevents compounding mess — when something breaks,
you know which change did it.

**Recommended tool: Spec Kit's `implement` step**, which executes the approved tasks.

**How a non-dev runs it.** Let Claude implement the one feature. Ask it to narrate what it's doing
in plain language so you can follow along. Resist the urge to queue up "and also build…" — finish
and verify this one first.

**Owner's checkpoint:** is exactly one feature being built, and is it the one you approved? If Claude
starts expanding scope, pull it back.

---

## 5. Test

**What.** Automated checks that prove the feature works — and keeps working when later changes land.
**Why.** "It ran once" isn't "it works and will keep working." Tests are the guardrail against future
changes silently breaking past features.

**Recommended approach.** You don't write tests by hand — have Claude write them, and *insist they
exist* for anything that matters. (Test-driven development — write the test first, then the code —
is a strong default; let Claude run it.)

**How a non-dev runs it.** Ask Claude to write tests for the feature and run them. Treat a feature
without tests as not done, for anything beyond the trivial.

**Owner's checkpoint:** are there tests for this feature, and do they pass? You don't read them; you
confirm they exist and are green.

---

## 6. Verify

**What.** Actually running the product and seeing the feature work, with a concrete success signal.
**Why.** "It built" and "the tests pass" still aren't "I saw it work." Verifying is *your* checkpoint
as the owner — the one that doesn't require reading code.

**How a non-dev runs it.** Run the app (locally or on a preview), use the feature as a user would, and
confirm the concrete "you'll know it works when…" that you agreed on. If something's off, report it
precisely: "I did X, expected Y, saw Z."

**Owner's checkpoint:** did you, personally, see it work the way the spec described? This is the
checkpoint you should never skip.

---

## 7. Review

**What.** Catching bugs, security issues, and quality problems *before* the feature merges. **Why.**
Review is where problems are caught cheaply; skipped review is paid back with interest later.

**Recommended tools (Claude Code built-ins and patterns):**
- **`/code-review`** — a focused pass for bugs and quality, run as you build.
- **A multi-agent PR review** before merging — security, code quality, architecture, performance,
  requirements, and regressions, in parallel. (Run it via a PR-review skill or the built-in review
  commands.)
- **`/security-review`** — a dedicated security pass for anything touching auth, user data, payments,
  or external input.

**How a non-dev runs it.** Run `/code-review` during the build; run the full review before merging a
feature; always run `/security-review` for sensitive changes. Have Claude explain any finding in plain
language and fix the important ones before merging.

**Owner's checkpoint:** were the reviews run, and were the serious findings (security, data, money)
addressed before merge? Don't merge sensitive changes that haven't had a security pass.

---

## 8. Refine

**What.** Tightening the code and **refining the UI** so the feature ships polished, not just
functional. **Why.** Functional-but-rough accumulates; refining before the next feature keeps quality
from eroding, and good UI is part of whether users trust the product.

**Recommended tools.**
- **Code quality:** the **Vercel skills** (`vercel-react-best-practices`, `vercel-composition-patterns`)
  for React/Next work, and the **Supabase skills** for database/RLS work.
- **UI refinement:** **impeccable** (`/audit`, `/polish`, `/critique`) and **web-design-guidelines**
  (Vercel's Web Interface Guidelines) — a design review that catches accessibility, anti-patterns, and
  "this looks like generic AI output."

**How a non-dev runs it.** After a feature works, run the design review (`impeccable /audit` +
web-design-guidelines) and the relevant best-practice skills, and have Claude apply the findings. Then
loop back to stage 1 for the next feature.

**Owner's checkpoint:** does the feature look and feel right (run the UI audit), and is the code held to
the best-practice skills? Then — and only then — move to the next feature.
