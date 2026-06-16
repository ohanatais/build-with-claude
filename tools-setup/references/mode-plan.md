# Mode: Plan

For a user who is starting out and doesn't know which tools they need or in what order. The
job: figure out the minimal kit this product actually needs, sequence it, and resist
over-tooling.

Load `references/core-principles.md` and `references/tools.md` alongside this file.

## Posture

Orienting and restraining. New builders tend to want to set up everything at once; the more
useful move is to set up the few tools the product needs *now* and add others only when a real
need appears. Every extra tool is another account, bill, and failure point. Give the user a
short, ordered path, not a 12-tool checklist.

## The flow

1. **Understand the product in 2–3 sentences** — what it does, whether it has user accounts,
   whether it charges money, whether it sends email. These answers decide the kit.
2. **Select the minimal kit** from the tool cards:
   - **Almost always:** GitHub (version control) + a host (Vercel) — you need to store code and
     put the site online.
   - **If it stores user data / has accounts:** a backend with database + auth (Supabase).
   - **Only if it charges money:** Stripe — and not until you're near taking payments.
   - **Only if it sends mail:** an email provider (Resend) — and not until the app needs to send.
   Skip anything the product doesn't need yet, and say so explicitly.
3. **Order them** — the natural sequence: GitHub → Supabase (if needed) → Vercel → Stripe (if
   charging) → email (if sending). Earlier tools are foundations the later ones connect to.
4. **Flag the decisions hiding in the setup** — a couple of these (which database/auth, whether
   to charge) are really `/technical-decisions` questions; note them so they're not made by
   accident.

## Output

- **The product, one paragraph.**
- **The minimal kit** — the tools needed now, each with a one-line "why," and an explicit list
  of what's being *skipped* for now and when to revisit.
- **The order** to set them up.
- **Next step:** start with the first tool in **setup** mode; pull `/technical-decisions` for
  any real choice along the way.

## The restraint to leave them with

The right number of tools at the start is the smallest that lets the product work. Adding tools
is easy and can wait; removing a tool you wired in prematurely is annoying. Set up what you
need, build, and let real pain points pull in the rest.
