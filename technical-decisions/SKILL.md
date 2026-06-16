---
name: technical-decisions
description: >
  Explain the technical decisions that come up in a typical product build — in plain
  language, for a non-technical builder who wants to understand what's being decided and
  why before approving it. Covers database, authentication, environment variables, APIs,
  deploy and hosting, domain and DNS, frontend vs. backend, and build-vs-buy. For each: what
  it is, why it exists, what's being decided and why, the tradeoffs, and what you need to
  know before saying yes — organized around whether a decision is reversible (move fast) or
  hard to undo (slow down and understand it).

  Make sure to use this skill whenever the user invokes /technical-decisions or, in plain
  terms, needs a technical choice explained or sanity-checked without being a developer —
  "what's a database / API / environment variable", "Claude wants to use Supabase, is that
  right", "should I use X or Y", "what am I giving up if we do this", "do I even need an
  API", "what does this setting mean", "explain what just happened before I approve it", or
  "is this decision a big deal or not". Also trigger when Claude Code (or a developer) is
  about to make an architectural choice and the non-technical owner should understand it
  first.

  Do NOT use for: the step-by-step setup of a specific tool — creating accounts, clicking
  through configuration (use /tools-setup); writing or debugging the actual code; or product,
  brand, and go-to-market decisions (those have their own skills). This skill explains and
  pressure-tests technical *decisions*; it doesn't implement them.
---

# Technical Decisions

Claude Code can build your product. But if you don't understand what it's building, you
can't make good decisions, catch mistakes, or know when something is about to go wrong. And
some things will go wrong — not because Claude is bad, but because technical decisions have
tradeoffs, and tradeoffs need judgment that only you (the person who knows the product and
the business) can supply.

This skill is the missing layer between "Claude, build my product" and actually understanding
what's being decided. The goal is **not** to make you technical. It's to give you exactly
enough understanding to make a good call alongside Claude — and to know when a decision is
small enough to wave through versus big enough to slow down and ask more questions.

## Language rule

**Always respond in the user's language.** If the user writes in Portuguese (including
Brazilian Portuguese), explain everything in Portuguese — plain, jargon-free, in their words.
This skill exists to remove the language barrier of tech; it would defeat the purpose to
explain a database in a second language the user has to translate in their head.

## The one idea that makes this manageable: two-way doors vs. one-way doors

You do not need to understand every technical decision equally. The useful filter (from
decision-making practice — Amazon's "two-way / one-way door" idea) is **how hard the decision
is to undo:**

- **Two-way door (reversible).** If this turns out wrong, you can change it later without much
  pain. Most decisions in a solo build are these: a button library, a styling approach, which
  email provider, most UI choices. **Move fast. Approve and keep going.** Understanding the
  gist is enough.
- **One-way door (hard to undo).** Changing this later means rewriting a lot, migrating data,
  or re-teaching users. A few decisions are these: your data model (how information is
  structured), your authentication provider (users are tied to it), your core framework, and
  anything touching money or stored user data. **Slow down. Understand the tradeoffs. Ask the
  questions in this skill before you approve.**

The whole point of understanding technical decisions is to spend your attention where it pays
off — on the few one-way doors — and not agonize over the many two-way doors. When a decision
comes up, the first question is always: *is this reversible?*

Load `references/core-principles.md` for the mindset (explain-before-execute, the right
altitude of understanding, why the tradeoff is the real content). Load `references/decisions.md`
for the catalog of specific decisions, each explained as a card.

## Entry point: what does the user need right now?

**Signal 1 — a term they don't recognize.** Claude or a dev said "we'll use Supabase / handle
auth / set an environment variable" and they want to know what that means before approving.
→ **explain** mode.

**Signal 2 — a choice on the table.** A decision was proposed (X vs. Y) and they want to
pressure-test it: tradeoffs, the reversibility question, what to ask. → **review** mode.

**Signal 3 — planning a build.** They're about to start and want to see the decisions coming
so none surprise them mid-build. → **map** mode.

Route:

| Mode | When | Reference |
|---|---|---|
| **explain** | A concept or decision came up; explain it plainly before approving | `references/mode-explain.md` |
| **review** | A choice is on the table; pressure-test it and surface the questions to ask | `references/mode-review.md` |
| **map** | Starting a build; walk the decisions ahead so none are a surprise | `references/mode-map.md` |

If unsure, ask: "Do you want me to explain something that just came up, help you weigh a
choice, or map out the decisions your build is going to hit?"

## The decision card (how every decision gets explained)

Whatever the mode, explain any technical decision in this shape — it's the format that gives
a non-developer exactly what they need to approve with confidence:

1. **What it is** — in one or two plain sentences, with a real-world analogy if it helps.
2. **Why it exists** — the problem it solves. (You can't judge a solution without the problem.)
3. **What's being decided** — the actual choice, and the realistic options.
4. **The tradeoffs** — what each option gives and costs. *This is the real content.* A
   decision presented without tradeoffs is just an opinion wearing a lab coat.
5. **Reversible?** — two-way door or one-way door, stated explicitly. This sets how much the
   user should care.
6. **What to know before you approve** — the one or two questions whose answers should change
   the decision, phrased so the user can actually ask them.

Never end on "so we'll use X." End on "here's the tradeoff and why X fits *your* situation —
and what would make Y the better call instead." The user should be able to disagree.

## Universal by design — fit the user's product, not a house stack

There are sensible defaults for a solo builder (a managed database, a hosting platform that
deploys on git push, a payments provider with a test mode). This skill can recommend them —
but always *with the tradeoff and the "when to choose otherwise."* A real-time multiplayer
game, a data-heavy analytics tool, and a simple content site genuinely want different
choices. Derive the recommendation from *this* product's needs, budget, and the owner's
comfort, and say plainly when the default doesn't fit. A recommendation the user can't
interrogate isn't understanding — it's a new black box.

## Output always includes

1. **The decision, in card form** — what / why / options / tradeoffs / reversible? / what to
   know before approving.
2. **A plain recommendation** — what fits this product and why, stated as a judgment the user
   can challenge, not a verdict.
3. **The reversibility call** — explicitly, so the user knows how much to care.
4. **The question(s) to ask** — what they should ask Claude or a dev before approving, in
   their own words.
5. **Next step** — approve and move on, or (for a one-way door) a beat to confirm before
   building. If setup follows, hand to `/tools-setup`.

## The posture that matters most

The most valuable thing you can do for a non-technical builder is **explain before you
execute, and make the tradeoff visible.** A fast "yes, using X" teaches nothing and hides the
moment where judgment was needed. A slower "here's what we're choosing, what it costs, and
whether it's a big deal" builds an owner who can steer the build for months — which is worth
far more than saving two minutes now.
