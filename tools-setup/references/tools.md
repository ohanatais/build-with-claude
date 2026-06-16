# The Tool Setup Cards

Setup guidance for the tools a typical solo build needs. Each card teaches the **goal** of
each step (durable against UI redesigns), not exact click-paths. Read the card for the tool
you're setting up. Set up only what the product actually needs now.

A natural order for a web product: **GitHub → Supabase → Vercel → (Stripe if you charge) →
(email if you send mail).**

## Contents
- [GitHub (version control)](#github)
- [Supabase (database, auth, storage)](#supabase)
- [Vercel (hosting & deploy)](#vercel)
- [Stripe (payments)](#stripe)
- [Email — Resend (transactional email)](#email--resend)

---

## GitHub

**What it is and why.** GitHub stores your code and its history in the cloud. Version control
means every change is saved and reversible, and it's how your code gets to your host. It's the
backbone the other tools connect to.

**Create the account.** A free personal account is enough to start. Then create a
**repository** (a "repo") — the container for this project's code. Private is the safe default
unless you want it public.

**Settings that matter.** Very few at setup. The meaningful choice is **public vs. private**
(private keeps your code unseen). Leave the rest at default.

**Connect it to the project.** Your local project gets linked to the repo so changes you (or
Claude) make can be "pushed" up. Claude Code can handle the git commands; you mainly need the
repo to exist and be connected.

**Verify it worked.** You'll know it's connected when a change you push shows up in the repo on
github.com.

**Common gotchas.**
- **Secrets in the repo.** Never commit API keys or passwords. A `.gitignore` file tells git to
  skip files like `.env` — confirm secrets aren't being pushed. (This is the big one.)
- **Public by accident.** If the repo is public, anyone can read it; make sure that's intended.

---

## Supabase

**What it is and why.** Supabase is a managed backend: a real Postgres **database**, plus
**authentication** (user login) and **file storage**, with no servers for you to run. For a
solo builder it covers several needs in one place.

**Create the account & project.** Sign up, create a **project** (this provisions your
database). You'll set a **database password** — save it somewhere safe immediately; it's a
secret. Pick a **region** close to your users for speed.

**Settings that matter.**
- **API keys / project URL** — your app needs these to talk to Supabase. There's a *publishable
  (anon)* key for client-side use and a *secret (service-role)* key that must stay server-side
  only. Know which is which.
- **Row Level Security (RLS)** — the rules that decide which user can see which data. This is
  security-critical for any app with user data; it should be on and configured, not skipped.
  (If unsure, this is a good moment for `/technical-decisions`.)

**Connect it to the project.** Put the project URL and keys into **environment variables** (not
in code). Claude wires the app to read them.

**Verify it worked.** You'll know it's connected when the app can read/write data and you see
rows appear in the Supabase table view.

**Common gotchas.**
- **Leaking the service-role key** — it must never reach the browser/frontend. Server-side env
  var only.
- **RLS left off** — data everyone can read when they shouldn't. Don't ship user data without it.
- **Lost database password** — save it at creation; recovering later is a hassle.

---

## Vercel

**What it is and why.** Vercel hosts your site and **deploys** it automatically: you push to
GitHub, Vercel builds it and puts it live, with preview links and one-click rollbacks. It
removes server management.

**Create the account & connect GitHub.** Sign up (you can use your GitHub account), then
**import the repo**. Vercel watches that repo and redeploys on each push.

**Settings that matter.**
- **Environment variables** — this is the big one. Every secret your app uses locally must also
  be set here, or the live site breaks. Vercel has a dedicated place for them.
- **Framework/build settings** — usually auto-detected; leave at default unless told otherwise.

**Connect it to the project.** It's connected by importing the repo. The first deploy happens
automatically.

**Verify it worked.** You'll know it worked when your Vercel URL loads the live site, and a new
push updates it.

**Common gotchas.**
- **Missing env vars in production** — the number-one cause of "works locally, breaks live."
  Mirror every local secret into Vercel.
- **Expecting instant** — a deploy takes a moment to build; "not live yet" is often just that.
- **A bad deploy** — use Vercel's rollback to return to the last working version instead of
  panicking.

---

## Stripe

**What it is and why.** Stripe handles payments — taking cards securely so you never store card
data yourself. Use it only if you charge money.

**Create the account.** Sign up. You can build entirely in **test mode** before providing
business details; going live requires verifying your business (and in some places, an entity —
some founders use Stripe Atlas for that, but it's optional and separate).

**Settings that matter.**
- **Test mode vs. live mode** — the most important concept. Test mode uses fake cards and no
  real money; build and verify here first. Each mode has its **own API keys.**
- **API keys** — a *publishable* key (safe in frontend) and a *secret* key (server-side env var
  only).
- **Webhooks** — how Stripe tells your app "this payment succeeded." You register a URL Stripe
  calls; your app listens. This trips people up, so verify it deliberately.

**Connect it to the project.** Keys into env vars (secret key server-side). Set up the webhook
endpoint and confirm Stripe can reach it.

**Verify it worked.** In test mode, a test card completes a purchase and your app receives the
webhook and reacts (grants access, records the order).

**Common gotchas.**
- **Test vs. live key mix-ups** — test keys live = no real charges; live keys while developing =
  real charges. Always know your mode.
- **Webhook not verified** — payments succeed at Stripe but your app never hears about it. Test
  the webhook explicitly.
- **Secret key in frontend** — never. Server-side only.

---

## Email — Resend

**What it is and why.** A transactional email provider sends the emails your app produces —
sign-up confirmations, password resets, receipts. Sending mail straight from your own server
lands in spam; a provider handles deliverability. Use it once your app needs to send mail.

**Create the account & verify your domain.** Sign up, then **verify your sending domain** by
adding DNS records (the provider gives them; you add them where your domain lives). This proves
you own the domain and is what keeps your mail out of spam.

**Settings that matter.**
- **Domain verification (DNS records)** — the core step; until it's verified and propagated,
  sending is limited or untrusted.
- **API key** — server-side env var only.
- **From address** — an address on your verified domain.

**Connect it to the project.** API key into an env var; the app calls the provider to send.

**Verify it worked.** A test email actually arrives in an inbox (not spam) from your domain.

**Common gotchas.**
- **DNS not propagated yet** — verification can take time after you add the records; "not
  verified yet" is often just waiting.
- **Sending before verification** — mail goes to spam or is blocked. Verify the domain first.
- **API key exposed** — server-side only, like every other secret.
