# The Decision Catalog

The technical decisions that come up most often in a solo product build, each as a **decision
card**: what it is, why it exists, the options, the tradeoffs, whether it's reversible, and
what to know before approving. Read the one you need; you don't need them all at once.

Recommendations here are sensible defaults for a typical solo-builder web product — always
presented with the tradeoff and the case where another choice wins. Fit them to the actual
product.

## Contents
- [The data model (the most important one)](#the-data-model)
- [Database](#database)
- [Authentication](#authentication)
- [Environment variables](#environment-variables)
- [APIs](#apis)
- [Deploy and hosting](#deploy-and-hosting)
- [Domain and DNS](#domain-and-dns)
- [Frontend vs. backend](#frontend-vs-backend)
- [Build vs. buy](#build-vs-buy)

---

## The data model

**What it is.** How your product's information is structured: what "things" exist (users,
posts, orders), what details each one holds, and how they relate. The blueprint under
everything.

**Why it exists.** Every feature reads or writes data. The model decides what's easy to build
later and what becomes a wall.

**What's being decided.** The shape of your core entities and their relationships — e.g. "a
user has many projects, a project has many entries."

**Tradeoffs.** Model it too loosely and features get hacky; too rigidly and change is
painful. The honest move early is to model what you actually know now and keep it simple.

**Reversible?** **One-way door — the hardest to undo.** Once real user data lives in a shape,
changing it means a migration (moving and reshaping existing data without losing or corrupting
it). This is the decision most worth slowing down for.

**Before you approve, ask:** "What happens to existing data if we need to change this later?"
and "Is this the simplest structure that supports the features in my MVP — not every future
idea?"

---

## Database

**What it is.** Where your product's data lives and is queried — a well-organized, searchable
filing cabinet that many users hit at once.

**Why it exists.** You need data to persist (survive a refresh), be queried fast, and stay
consistent when many people use the app together. Files on a server can't do that reliably.

**What's being decided.** Which database, and usually managed vs. self-hosted.

**Options & tradeoffs.**
- **Managed Postgres (e.g. Supabase)** — recommended default for solo builders. You get a
  real relational database plus auth, file storage, and auto-generated APIs, with no servers
  to run. Tradeoff: you're on their platform and pricing.
- **Other managed databases** — fine; similar tradeoff.
- **Self-hosting your own database** — maximum control, but you now do backups, scaling, and
  security. For a solo non-technical builder, this is usually a trap.

**Reversible?** Switching database *providers* later is painful (a migration) — lean one-way.
The *data model* inside it is the harder lock-in (see above).

**Before you approve, ask:** "Does this give me auth and storage too, or are those separate
decisions?" and "What's the cost when I have 100 users vs. 10,000?"

---

## Authentication

**What it is.** How the product knows *who* a user is — sign-up, log-in, sessions, "stay
logged in." ("Authorization" is the cousin: what a logged-in user is *allowed* to do.)

**Why it exists.** The moment users have their own data, you must reliably and securely tell
them apart. Auth is security-critical: getting it wrong leaks accounts.

**What's being decided.** Which auth provider, and which login methods (email/password, Google
and other social logins, magic links).

**Options & tradeoffs.**
- **Your platform's built-in auth (e.g. Supabase Auth)** — recommended default; integrates
  with your database and handles the dangerous parts (password hashing, sessions, resets).
- **A dedicated auth provider** — more features (enterprise SSO, advanced flows); another bill
  and integration.
- **Rolling your own auth** — almost never the right call for a solo builder. Security
  edge-cases are deep; use a provider.

**Reversible?** **One-way door.** Users get tied to the provider; migrating accounts later is
delicate. Choose deliberately.

**Before you approve, ask:** "Which login methods do my users actually expect?" and "Is the
provider handling password security and sessions for me, so I'm not?"

---

## Environment variables

**What it is.** Settings and secrets kept *outside* your code — API keys, database passwords,
config that differs between your laptop and the live site. The keys you keep off the public
keychain.

**Why it exists.** Two reasons. **Security:** secrets in code get pushed to GitHub and leak;
env vars keep them out. **Flexibility:** the same code can point at a test database locally
and the real one in production, just by changing a variable.

**What's being decided.** Usually not "if" but "this value is a secret, so it goes in an env
var, not in the code."

**Tradeoffs.** Almost pure upside; the only cost is remembering to set them in each place
(your machine, the host). Forgetting one is a common, easily-fixed cause of "works locally,
breaks live."

**Reversible?** Two-way door — easy to add or change.

**Before you approve, ask:** "Is any secret about to be written directly into the code?" (the
answer should be no) and "Where do I set these for the live site?"

---

## APIs

**What it is.** A way for two pieces of software to talk through a defined menu of requests —
a waiter who takes your order to the kitchen and brings back the dish, so you never enter the
kitchen yourself. Your app calls other services' APIs (Stripe, an email provider, an AI
model); sometimes your app exposes its own.

**Why it exists.** You don't rebuild payments or email — you call a service that does it, via
its API. And your frontend often talks to your backend through an API.

**What's being decided.** Which external APIs to use, and whether *your* product needs to
expose its own API (often it doesn't, early).

**Tradeoffs.** Using an external API saves enormous work but adds a dependency (their uptime,
pricing, and rules become yours). Building your own API adds power and complexity — usually
unnecessary until you have other apps or partners consuming your data.

**Reversible?** Using an external API is fairly reversible (you can swap providers with work).
Designing your own public API for others is closer to one-way once people depend on it.

**Before you approve, ask:** "Do I actually need our own API yet, or are we just calling
others'?" and "What happens to my product if this external service has an outage or raises
prices?"

---

## Deploy and hosting

**What it is.** "Deploy" is publishing your code so real people can reach it. "Hosting" is the
computer-in-the-cloud that runs it. The difference between "works on my machine" and "works
for users."

**Why it exists.** Your laptop isn't a public, always-on server. Hosting puts the app on the
internet; deploying updates it.

**Options & tradeoffs.**
- **Push-to-deploy platforms (e.g. Vercel)** — recommended default. You push to GitHub, it
  builds and goes live automatically, with previews and rollbacks. Tradeoff: platform pricing
  and some constraints on how the app runs.
- **Traditional servers / VPS** — full control, but you manage the machine, security, and
  scaling yourself. Heavy for a solo non-technical builder.

**Reversible?** Fairly two-way for a typical web app — you can move hosts with effort. It
feels scarier than it is.

**Before you approve, ask:** "When I want to publish a change, what do I actually do?" and "If
a deploy breaks the site, how do I roll back?"

---

## Domain and DNS

**What it is.** The **domain** is your address (yoursite.com). **DNS** is the internet's phone
book that translates that name into the server's actual location. Buying a domain and having a
working site are two steps, not one.

**Why it exists.** Humans use names; computers use numbers. DNS connects the two. After you
buy a domain you point its DNS at your host, and (usually automatic now) get HTTPS so the
padlock shows and data is encrypted.

**What's being decided.** Where you buy the domain, and pointing DNS at your host. Mostly
mechanical.

**Tradeoffs.** Few. The classic gotcha is *propagation* — DNS changes can take minutes to
hours to take effect everywhere, so "it's not working yet" is often just waiting, not a bug.

**Reversible?** Two-way door. You can repoint DNS or move domains.

**Before you approve, ask:** "Is HTTPS (the padlock) set up automatically, or do I need to do
something?" and "If the site doesn't load right after I change DNS, is that just propagation?"

---

## Frontend vs. backend

**What it is.** **Frontend** is everything the user sees and clicks (the interface, in the
browser). **Backend** is the part they don't (data, logic, security, talking to the database)
— the dining room vs. the kitchen.

**Why it matters to you.** Knowing which side Claude is touching tells you what a change
affects. A frontend tweak changes how something looks; a backend change can affect data and
security and deserves more care.

**What's being decided.** Less a single decision than a lens: in any given moment, which side
are we in? Some choices (like a framework that blends both, e.g. Next.js) shape this.

**Tradeoffs.** Frontend changes are usually low-risk and visible. Backend changes — especially
to data or auth — are where real care belongs (see reversibility of those cards).

**Reversible?** The split itself isn't a "decision" to reverse; it's a map. Individual changes
vary.

**Before you approve, ask:** "Is this change frontend (just how it looks) or backend (data,
logic, security)?" — because the second answer means slow down a little.

---

## Build vs. buy

**What it is.** For any capability (payments, email, search, analytics, auth), the choice
between building it yourself or using an existing service.

**Why it exists.** Your time is the scarcest resource. Rebuilding a solved, security-sensitive
problem (payments, auth, email deliverability) is rarely worth it.

**Tradeoffs.** **Buy:** fast, battle-tested, secure — but a dependency and a recurring cost.
**Build:** full control and no per-use fee — but your time, your bugs, and your security
burden. For a solo builder the default is **buy the commodity, build the thing that's actually
your product.**

**Reversible?** Varies — usually swapping a bought service is two-way; replacing something
you've built deeply is harder.

**Before you approve, ask:** "Is this the special thing that makes my product *mine*, or a
solved commodity?" (Build the first; buy the second.) and "What's the real cost of this
service at my expected scale?"
