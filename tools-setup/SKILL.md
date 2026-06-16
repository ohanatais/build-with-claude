---
name: tools-setup
description: >
  Walk a non-technical builder through setting up the tools a typical product build needs —
  GitHub, Supabase, Vercel, Stripe, and an email provider like Resend — step by step, one at
  a time, explaining what each setting means and connecting each tool to the project. Built
  to be durable: it teaches *what you're trying to accomplish* at each step (and the common
  gotchas) rather than exact click-paths that go stale, and it keeps secrets safe along the
  way.

  Make sure to use this skill whenever the user invokes /tools-setup or needs to actually set
  up or connect a tool — "set up Supabase / Vercel / Stripe / GitHub / email", "how do I
  connect X to my project", "create a [tool] account", "I'm stuck on this setup", "what does
  this setting mean while I'm configuring this", "my deploy / webhook / database connection
  isn't working", or "which tools do I even need". Also trigger right after a tool is chosen
  (often via /technical-decisions) and it's time to make it real.

  Do NOT use for: deciding *whether* to use a tool or weighing alternatives (use
  /technical-decisions); writing or debugging application code; or anything product, brand,
  or go-to-market. This skill is the hands-on setup, not the decision and not the build.
---

# Tools Setup

Official documentation assumes you already know things. This skill doesn't. It walks a
non-technical builder through setting up each tool a typical build needs — making the account,
understanding what each setting means, connecting it to the project, and getting unstuck when
the setup doesn't work the first time (it often doesn't, and that's normal).

The promise is calm, one-step-at-a-time setup where nothing is assumed and every setting is
explained before you touch it.

## Language rule

**Always respond in the user's language.** If the user writes in Portuguese (including
Brazilian Portuguese), guide the entire setup in Portuguese. Someone setting up a tool for the
first time should not also be translating instructions in their head.

## A note on durability (read this first)

Tool interfaces change constantly — buttons move, screens get redesigned. So this skill
deliberately teaches **what you're trying to accomplish** and **what each setting means**,
not "click the blue button in the top-right." When guiding, describe the *goal* of a step
("you're looking for where the project's API keys live — usually under settings") so the
instruction survives a redesign, and ask the user what they see rather than assuming the
screen. If the exact location has moved, the user can still find it because they know what
they're looking for and why.

## The setup posture: one step, confirmed, then the next

The fastest way to overwhelm a non-technical builder is a 20-step wall. Instead:

1. **One step at a time.** Give a step, wait for the user to do it and confirm, then the next.
2. **Say what each setting means before they set it** — and which ones are safe to leave at
   default (most are). Decision fatigue comes from treating every field as a choice.
3. **Protect secrets as you go.** API keys, database passwords, and tokens go into environment
   variables, never pasted into code or committed to GitHub. Flag this every time a secret
   appears — it's the highest-stakes habit in the whole process.
4. **Verify the connection** at the end of each tool — a concrete "you'll know it worked when
   you see X." Setup that's never verified tends to fail silently later.

Load `references/core-principles.md` for the mindset and the cross-cutting gotchas (secrets,
test vs. live mode, propagation, "works locally not live"). Load `references/tools.md` for the
per-tool setup cards.

## Entry point: what does the user need?

**Signal 1 — set up a specific tool.** They name one (or were just told to use one). →
**setup** mode for that tool.

**Signal 2 — something's broken.** A setup isn't working — deploy fails, webhook silent,
database won't connect. → **troubleshoot** mode.

**Signal 3 — which tools, in what order?** They're starting and don't know what they need. →
**plan** mode (and resist over-tooling).

Route:

| Mode | When | Reference |
|---|---|---|
| **setup** | Setting up and connecting a specific tool | `references/mode-setup.md` + the tool's card in `references/tools.md` |
| **troubleshoot** | A setup isn't working; diagnose and fix | `references/mode-troubleshoot.md` |
| **plan** | Starting out; decide which tools are needed and in what order | `references/mode-plan.md` |

If unsure, ask: "Do you want to set a specific tool up, fix one that's misbehaving, or figure
out which tools you actually need?"

## Each tool is set up as a card

`references/tools.md` covers GitHub, Supabase, Vercel, Stripe, and email (Resend) — each in
the same shape:

1. **What it is and why you need it** — one or two sentences.
2. **Create the account** — what to make, and any plan/tier note.
3. **The settings that matter** — what each meaningful setting does, and what to leave alone.
4. **Connect it to the project** — how it plugs into the build (usually keys into env vars).
5. **Verify it worked** — the concrete signal of success.
6. **Common gotchas** — the handful of things that trip people up, and the fix.

## Universal by design — only the tools this product needs

There's a common default kit (version control, database, hosting, payments if you charge,
email if you send mail). But a free content site needs no payments; a tool with no accounts
needs no auth/email yet. **Set up only what the product actually needs now**, and add tools
when a real pain point appears, not preemptively. Over-tooling is its own kind of debt — more
accounts, more bills, more things to break. Fit the kit to the product.

## Output always includes

1. **A short setup plan** — the steps for this tool (or the ordered list of tools), so the
   user sees the shape before starting.
2. **Step-by-step guidance** — one step at a time, each setting explained, confirmed as they
   go.
3. **Secret-safety checks** — every key or password routed into an environment variable, never
   into code or git.
4. **A verification** — the concrete "you'll know it worked when…" for each tool.
5. **Gotcha flags** — the known traps for that tool, surfaced before they bite.
6. **Next step** — the next tool, or back to building. If a *decision* surfaces ("which plan?",
   "do I even need this?"), hand to `/technical-decisions`.

## When setup breaks (it will)

A failed setup is normal and almost always one small thing — a missed setting, a key in the
wrong place, a value not yet propagated. Treat breakage as a clue about *which* step, not a
verdict on the user. The most useful thing the user can report is "I did X, expected Y, saw Z"
— that localizes the problem far faster than "it's not working." Stay calm, isolate the step,
fix the one thing.
