# technical-decisions

> Claude Code can build your product. But if you don't understand what it's building, you can't catch a mistake, weigh a tradeoff, or know when a decision is a big deal. This skill is the understanding — not the code.

Part of the [build-with-claude](https://github.com/ohanatais/build-with-claude) skill set, within the [build-from-zero](https://github.com/ohanatais/build-from-zero) ecosystem.

---

## What this skill does

Explains the technical decisions that come up in a typical product build — database, authentication, environment variables, APIs, deploy and hosting, domain and DNS, frontend vs. backend, build-vs-buy — in **plain language, for a non-technical builder**. For each decision it gives: what it is, why it exists, the realistic options, the tradeoffs, whether it's reversible, and what to ask before approving.

The goal isn't to make you a developer. It's to get you to exactly the altitude where you can make a good call alongside Claude, and know when to slow down.

---

## The one idea that makes it manageable

You don't need to understand every decision equally. Sort by how hard it is to undo:

- **Two-way door (reversible)** — most decisions. Move fast, approve, change later if needed.
- **One-way door (hard to undo)** — the data model, auth provider, anything with money or stored personal data. Slow down and understand it.

Spend your attention on the few one-way doors; wave through the many two-way doors. That's the whole strategy.

---

## Every decision gets explained as a card

```
1. What it is            →  plain language, with an analogy if it helps
2. Why it exists         →  the problem it solves
3. What's being decided  →  the actual choice and the real options
4. The tradeoffs         →  what each option gives and costs (this is the real content)
5. Reversible?           →  two-way door or one-way door, stated outright
6. Before you approve    →  the question(s) whose answers should change the decision
```

It never ends on "so we'll use X." It ends on the tradeoff and what would make the other choice better — so you can actually disagree.

---

## Three modes, one interface

| Mode | When to use | Output |
|---|---|---|
| **explain** | A term or decision came up; explain it before approving | A clear, proportionate explanation + a yes/no |
| **review** | A choice is on the table; pressure-test it | Tradeoffs side by side + recommendation + questions to ask |
| **map** | Starting a build; see the decisions coming | Decisions ahead, sorted by reversibility, with a rough sequence |

---

## How to install

```bash
cp -r technical-decisions /your-project/.claude/skills/
```

---

## How to trigger

```
/technical-decisions
```

It also triggers on plain phrasing — "what's a database / API / environment variable", "Claude wants to use Supabase, is that right", "should I use X or Y", "what am I giving up", "explain this before I approve it" — even without technical words.

---

## The relationship to the rest

This skill *explains and weighs* decisions. Its companion [`tools-setup`](../tools-setup) handles the step-by-step of actually setting a tool up once you've decided. Together they're the bridge between "Claude, build my product" and shipping something you understand.

---

Made by [Ohana Taís](https://github.com/ohanatais) · part of [build-from-zero](https://github.com/ohanatais/build-from-zero)
