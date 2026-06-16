# build-with-claude

> You don't need to become a developer. You need to understand what's being decided — and why.

Part of the [build-from-zero](https://github.com/ohanatais/build-from-zero) ecosystem.

Claude Code can build your product. But if you don't understand what it's building, you can't make good decisions, catch mistakes, or know when something is going wrong. And it will go wrong — not because Claude is bad, but because technical decisions have tradeoffs, and tradeoffs require judgment.

This repo is the missing layer between "Claude, build my product" and actually shipping something that works, that you understand, and that you can maintain and evolve.

---

## What's inside

### Technical decisions explained
Every technical decision that comes up in a typical product build — explained in plain language.

When Claude Code says "I'll use Supabase for the database" or "we'll need to handle authentication here" or "this should be an environment variable," you need to know what that means before you say yes.

This guide covers the decisions that come up most often, in the order they tend to appear:

- **Database** — what it is, why it matters, why Supabase specifically, and what you'd be giving up with each alternative
- **Authentication** — what happens when a user logs in, what "auth providers" are, what you need to decide before Claude starts building
- **Environment variables** — what they are, why they exist, what happens if you handle them wrong
- **APIs** — what an API actually is, when your product needs one, and when it doesn't
- **Deploy and hosting** — the difference between "it works on my machine" and "it works for real users"
- **Domain and DNS** — what happens between buying a domain and having a real URL that works
- **Frontend vs. backend** — what the split means, which one Claude is touching in any given moment, and why it matters

Each entry answers: what is this, why does it exist, what was decided and why, what are the tradeoffs, and what do you need to know before approving this decision.

### Claude Code for non-technical builders
How to work with Claude Code effectively when you don't have a technical background.

Claude Code is powerful. It's also easy to misuse — not because you'll break something irreparably, but because bad prompts produce bad code, and bad code accumulates into a product that's hard to maintain and harder to change.

- **How to write a CLAUDE.md that actually works** — what context Claude needs to be useful across sessions, and how to keep it updated as your product evolves
- **The feature-by-feature method** — why you should never ask Claude to build more than one thing at a time, and how to structure each session so nothing gets lost
- **Planning sessions vs. execution sessions** — the difference, why it matters, and how to run each one
- **How to ask Claude to explain before it executes** — the exact phrasing that gets you explanations, not just actions
- **How to read what Claude is doing** — how to follow along with what's being built without needing to read code
- **What to do when something breaks** — the mindset and the steps, in order

### Tools setup guide
Step-by-step setup for every tool that typically comes up in a solo product build.

Official documentation assumes you already know things. This doesn't.

Each guide covers: what the tool is and why you need it, how to create an account, what each setting means when you encounter it, how to connect it to your project, and what to do when the setup doesn't work.

Tools covered:
- **GitHub** — repositories, commits, what version control actually means in practice
- **Supabase** — database setup, tables, how to connect it to your project
- **Vercel** — deploying your product so real people can access it
- **Stripe** — setting up payments, test mode vs. live mode, what a webhook is
- **Resend / email providers** — sending emails from your product

---

## How this fits into the build process

You don't read this repo before you start building. You reference it as you go.

When Claude Code introduces a concept you don't recognize, come here. When you need to set up a new tool, come here. When something breaks and you don't know what layer it's in, come here.

The goal isn't for you to become technical. It's for you to have enough understanding to make good decisions alongside Claude — and to know when to slow down and ask more questions before approving what's being built.

**Claude Code skills** that support the build process live directly in this repo — one folder per topic, each with its own SKILL.md, references/, and README.md, following the pattern set by [product-thinking](https://github.com/ohanatais/product-thinking) and [brand-and-copy](https://github.com/ohanatais/brand-and-copy).

- [`technical-decisions`](technical-decisions) — explain and pressure-test the technical decisions in a build, in plain language
- [`tools-setup`](tools-setup) — step-by-step setup of the tools a build needs (GitHub, Supabase, Vercel, Stripe, email)

---

## Status

| Content | Status |
|---|---|
| Technical decisions explained | ✅ Skill available in [`technical-decisions`](technical-decisions) |
| Claude Code for non-technical builders | 📋 Planned |
| Tools setup (GitHub, Supabase, Vercel, Stripe, email) | ✅ Skill available in [`tools-setup`](tools-setup) |

---

## Part of the ecosystem

| Repo | Focus |
|---|---|
| [build-from-zero](https://github.com/ohanatais/build-from-zero) | End-to-end hub |
| [product-thinking](https://github.com/ohanatais/product-thinking) | Market research, validation, personas, PRD |
| [brand-and-copy](https://github.com/ohanatais/brand-and-copy) | Brand identity, tone, copy |
| **build-with-claude** | You are here |
| [go-to-market](https://github.com/ohanatais/go-to-market) | Launch strategy, first users |
| [pm-skills](https://github.com/ohanatais/pm-skills) | Claude Code skills for product-management day-to-day · PT-BR |

---

Made by [Ohana Taís](https://github.com/ohanatais) · [![LinkedIn](https://img.shields.io/badge/LinkedIn-ohanatais-blue?style=flat&logo=linkedin)](https://linkedin.com/in/ohana-taís)
