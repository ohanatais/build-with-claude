# tools-setup

> Official documentation assumes you already know things. This doesn't. One step at a time, every setting explained, nothing assumed.

Part of the [build-with-claude](https://github.com/ohanatais/build-with-claude) skill set, within the [build-from-zero](https://github.com/ohanatais/build-from-zero) ecosystem.

---

## What this skill does

Walks a non-technical builder through setting up the tools a typical product build needs — GitHub, Supabase, Vercel, Stripe, and an email provider like Resend — step by step. For each tool: make the account, understand what each setting means, connect it to the project, verify it worked, and get unstuck when it doesn't (it often doesn't, and that's normal).

It's built to be **durable**: it teaches *what you're trying to accomplish* at each step rather than exact click-paths that go stale when a tool gets redesigned — and it keeps your secrets safe the whole way.

---

## How it works

**One step at a time, confirmed, then the next.** No 20-step walls. Each setting is explained before you touch it, and you're told which ones to just leave at default (most of them).

**Secrets safety, every time.** API keys and passwords go into environment variables, never into code or GitHub. The skill flags this every time a key appears — it's the highest-stakes habit in the whole process.

**Verify before moving on.** Each tool ends with a concrete "you'll know it worked when…" so nothing fails silently later.

---

## Three modes, one interface

| Mode | When to use | Output |
|---|---|---|
| **setup** | Setting up and connecting a specific tool | Step-by-step setup, each setting explained, verified |
| **troubleshoot** | A setup isn't working | Symptom → layer → usual suspects → the one fix |
| **plan** | Starting out, unsure which tools you need | The minimal kit for your product, in order |

---

## The tools covered

GitHub (version control) · Supabase (database, auth, storage) · Vercel (hosting & deploy) · Stripe (payments) · Resend (transactional email). Each as a card: what it is and why, create the account, the settings that matter, connect it, verify it, common gotchas. **Set up only what your product actually needs now** — over-tooling is its own debt.

---

## How to install

```bash
cp -r tools-setup /your-project/.claude/skills/
```

---

## How to trigger

```
/tools-setup
```

It also triggers on plain phrasing — "set up Supabase / Vercel / Stripe", "how do I connect X to my project", "I'm stuck on this setup", "my deploy / webhook isn't working", "which tools do I even need".

---

## The relationship to the rest

This skill handles the hands-on setup. Its companion [`technical-decisions`](../technical-decisions) handles *deciding* whether to use a tool and weighing the tradeoffs. Decide there, set it up here.

---

Made by [Ohana Taís](https://github.com/ohanatais) · part of [build-from-zero](https://github.com/ohanatais/build-from-zero)
