# The Recommended Toolkit

The public tools this skill points to, one per area of the loop. **These are recommendations to
install and use — not content this skill copies.** Each is maintained by its authors and is better
than anything reinvented here. A builder can swap any of them for an equivalent; the loop still holds.

When guiding a user, link them to the tool and explain *what it's for* and *when in the loop to reach
for it* — then let them install and run it themselves.

> Note: tool commands and install steps change over time. Treat the specifics below as a starting
> point and point the user to each tool's own README for the current instructions.

## Contents
- [Spec-driven development — GitHub Spec Kit](#spec-kit)
- [Persistent context — CLAUDE.md / built-in init](#claude-md)
- [Code & PR review — built-in review commands](#review)
- [Code quality — Vercel skills](#vercel-skills)
- [Database — Supabase skills](#supabase-skills)
- [UI refinement — impeccable & web design guidelines](#ui-refinement)

---

## Spec Kit

**Area:** stages 1–4 (spec → clarify → plan → tasks → implement).
**What:** GitHub's open-source toolkit for spec-driven development — structure for describing what to
build before building it, with templates and cross-artifact checks.
**Where:** github.com/github/spec-kit
**Install (starting point):** a Python CLI, typically bootstrapped with something like
`uvx --from git+https://github.com/github/spec-kit.git specify init <project>` — check the repo README
for the current command. It adds `/speckit.*` commands to your AI coding tool.
**When to use:** at the start of every feature (specify, clarify) and before building (plan, tasks,
implement).

---

## CLAUDE.md

**Area:** stage 2 (persistent context).
**What:** Claude Code's project memory file, read every session. Not a third-party install — a
built-in concept.
**How:** run `/init` in Claude Code to scaffold one from your project, then keep it current as
decisions are made.
**When to use:** create it early; update it whenever a real decision or convention is set.

---

## Review

**Area:** stage 7 (review).
**What:** Claude Code's built-in review commands, plus a multi-agent PR review pattern.
**How:**
- **`/code-review`** — built into Claude Code; a focused bug/quality pass during the build.
- **`/security-review`** — built into Claude Code; a dedicated security pass for sensitive changes.
- **Multi-agent PR review** — a parallel review across security, quality, architecture, performance,
  requirements, and regressions before merge. Available as PR-review skills in the Claude Code
  ecosystem; or compose it from the built-in commands.
**When to use:** `/code-review` as you build; the full PR review before merging a feature;
`/security-review` whenever auth, data, payments, or external input are involved.

---

## Vercel skills

**Area:** stage 8 (code quality, for React/Next.js builds).
**What:** Vercel's public Claude Code skills for performance and composition.
- **`vercel-react-best-practices`** — performance patterns (data fetching, bundle size, re-renders).
- **`vercel-composition-patterns`** — component composition that scales.
**Where:** available in the Claude Code plugin/skill ecosystem (Vercel).
**When to use:** when writing or refining React/Next.js components and pages.

---

## Supabase skills

**Area:** stage 8 (database quality), if the project uses Supabase.
**What:** Supabase's public skills for correct, secure database work.
- **`supabase`** — general Supabase usage (auth, queries, SSR integration).
- **`supabase-postgres-best-practices`** — Postgres performance, RLS, indexes, avoiding N+1.
**Where:** available in the Claude Code skill ecosystem (Supabase); see supabase.com/docs for the
agent skills.
**When to use:** any change touching the database, migrations, or row-level security.

---

## UI refinement

**Area:** stage 8 (UI refinement).
**What:** a design review that catches accessibility issues, anti-patterns, and generic-AI-output look.
- **impeccable** — an open-source Claude Code design skill (Paul Bakaus) with steering commands like
  `/audit`, `/polish`, and `/critique`, plus curated anti-patterns. Where: github.com/pbakaus/impeccable
- **web-design-guidelines** — a skill that reviews UI against Vercel's Web Interface Guidelines
  (accessibility and interface best practices).
**When to use:** after a feature works, before moving to the next — run the audit and apply the findings.

---

## How to present these to a user

Don't dump the whole list. Name the *one or two* tools relevant to the stage they're at, link them,
say what the tool does and when to use it, and let them install it. The skill's job is to be the index
and the conductor — pointing to the right tool at the right moment — not to reproduce what these tools
already do well.
