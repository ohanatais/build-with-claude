# Mode: Setup

For a builder starting a project who wants the **process and the toolkit set up** — the scaffolding
in place so they can then run the loop. Less teaching, more wiring-up. Install the recommended tools,
scaffold the context, and leave them ready to build feature one.

Load `references/core-principles.md`, `references/tools.md`, and `references/the-loop.md` alongside
this file.

## Posture

Practical and orderly. The goal is a project where the loop can run: spec tooling installed, a
CLAUDE.md in place, review and refinement tools available, and the owner knowing what each is for.
Install one thing at a time and confirm it, the same one-step-at-a-time discipline as `/tools-setup`.
Recommend the proven defaults but make clear they're swappable.

## The flow

1. **Spec tooling** — install **GitHub Spec Kit** (point to its README for the current command), so
   the spec → plan → tasks → implement steps are available. Confirm it initialized.
2. **Persistent context** — run `/init` to scaffold **CLAUDE.md**. Then fill in the essentials: the
   stack, the product in two lines, and the owner's working preferences ("explain before executing;
   one feature at a time; tell me the tradeoffs"). This file is the highest-return thing in the repo.
3. **Review tools** — confirm the built-in `/code-review` and `/security-review` are available, and
   set the expectation that a multi-agent PR review runs before merge.
4. **Refinement tools** — install **impeccable** (point to github.com/pbakaus/impeccable) and the
   **web-design-guidelines** skill for UI review; note the **Vercel** and **Supabase** skills for code
   and database quality if the stack uses them.
5. **A first pass of the loop on paper** — briefly map the first feature through the eight stages so
   the owner sees how the installed tools connect into the process.

Install only what the stack needs (skip Supabase skills if not using Supabase, etc.) — same
no-over-tooling discipline as elsewhere.

## Where to be careful

- **Don't copy tool content into the project** — install the tools; the skill is the conductor, not a
  replacement. Link the user to each tool's own setup.
- **CLAUDE.md must be real** — a scaffold left empty helps nothing; fill in the stack, the product,
  and the working preferences.
- **Point to current docs** — install steps drift; send the user to each tool's README rather than
  asserting a stale command.

## Close

Confirm the toolkit is installed and CLAUDE.md is real, then hand to **guided** mode (to run the loop
on the first feature) or **stage** mode (if they're ready to start specifying). Route account-level
tool setup (Supabase, Vercel, etc.) to `/tools-setup`.
