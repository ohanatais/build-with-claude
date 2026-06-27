# working-with-claude

> Claude Code can build your product. Whether what comes out is something you understand and can evolve — or an accumulating mess — depends almost entirely on the process you build it with.

Part of the [build-with-claude](https://github.com/ohanatais/build-with-claude) skill set, within the [build-from-zero](https://github.com/ohanatais/build-from-zero) ecosystem.

---

## What this skill does

Teaches the **process of building a product with Claude Code**, for a non-technical builder — the pipeline from spec to shipped: spec-driven development, persistent project context, building feature by feature with validation checkpoints, testing, running and verifying, code and PR review, and refining both code and UI.

It's a **conductor, not a copy**: it teaches the loop and points you to the proven public tools to install and use at each stage — GitHub Spec Kit, impeccable, the Vercel and Supabase skills, and Claude Code's built-in review commands. It recommends and references them; it doesn't replace them.

The skill is **universal by design**: the *loop* is the durable part (it's how disciplined software gets built), and the *tools* are strong recommendations you can swap for equivalents. The point is never rigid ceremony — it explains *why* each stage earns its keep, so the discipline sticks.

---

## The build loop (one feature at a time)

```
1. Spec        →  Describe what & why before any code (spec-driven development)
2. Context     →  Persistent project memory across sessions (CLAUDE.md)
3. Plan → tasks→  Turn the spec into a plan and a task breakdown, and approve it
4. Build       →  Implement one feature at a time, with a checkpoint before the next
5. Test        →  Tests as a guardrail; know "it works" provably
6. Verify      →  Run it and see it work — "you'll know it works when…"
7. Review      →  Code review during; PR review + security review before merge
8. Refine      →  Tighten the code, refine the UI — then loop back for the next feature
```

The two non-negotiable habits underneath it: **explain before execute**, and **one feature at a time, verified**.

---

## The recommended toolkit (install, don't copy)

| Stage | Tool | Source |
|---|---|---|
| Spec, plan, tasks | **GitHub Spec Kit** | github.com/github/spec-kit |
| Context | **CLAUDE.md** via `/init` | Claude Code built-in |
| Review | **`/code-review`, `/security-review`** + a multi-agent PR review | Claude Code built-ins |
| Code quality | **Vercel skills** (react-best-practices, composition-patterns) | Vercel |
| Database | **Supabase skills** | Supabase |
| UI refinement | **impeccable** + **web-design-guidelines** | github.com/pbakaus/impeccable · Vercel |

---

## Three modes, one interface

| Mode | When to use | Output |
|---|---|---|
| **guided** | Learning and running the whole loop, first project | Walk the loop on a real feature, explaining the why |
| **setup** | Scaffold the process and install the tools for a project | The toolkit installed + a real CLAUDE.md |
| **stage** | At a specific point in the loop, want help with that stage | That stage run well + the owner's checkpoint |

---

## How to install

```bash
cp -r working-with-claude /your-project/.claude/skills/
```

---

## How to trigger

```
/working-with-claude
```

It also triggers on natural phrasing — "what's the process", "how do I build this without it becoming a mess", "what's spec-driven development", "planning vs execution sessions", "how do I review / test / refine with Claude", "Claude built the wrong thing" — even without naming the skill.

---

## The relationship to the rest

This skill is the *process*. Its companions in this repo: [`technical-decisions`](../technical-decisions) explains *what* gets decided along the way, and [`tools-setup`](../tools-setup) handles the account-level setup of the tools. Together they're the bridge between "Claude, build my product" and shipping something you understand.

---

Made by [Ohana Taís](https://github.com/ohanatais) · part of [build-from-zero](https://github.com/ohanatais/build-from-zero)
