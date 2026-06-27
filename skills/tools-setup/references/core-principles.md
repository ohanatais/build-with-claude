# Core Principles

Loaded for every tools-setup session. The mindset and the cross-cutting gotchas that apply no
matter which tool is being set up.

## Teach the goal, not the click-path

Tool UIs change all the time. An instruction like "click the green button top-right" rots the
moment the vendor redesigns. So always frame a step by its **goal**: "you're looking for where
this project's secret keys live — usually under a Settings or API section." That survives a
redesign, and it teaches the user to navigate any tool, not just memorize one screen. When in
doubt about the current layout, ask the user what they see and guide from there rather than
asserting a screen you can't see.

## One step at a time, confirmed

A non-technical builder drowns in a 20-step wall. Give one step, let them do it, confirm it
worked, then the next. This is slower per message and dramatically faster overall, because it
catches a wrong turn at step 3 instead of at step 20. It also keeps the user feeling in
control rather than swept along.

## Most settings are defaults — say which ones aren't

Decision fatigue comes from treating every field as a meaningful choice. Most aren't. Tell the
user plainly: "leave these at default; the only setting that matters here is X, and here's what
it does." Reserve their attention for the few settings that actually affect their product.

## Secrets safety is the highest-stakes habit

Every tool hands you keys — API keys, database passwords, tokens. The rule, every single time:

- **Secrets go into environment variables, never into the code, and never committed to
  GitHub.** A key pasted into code and pushed is a key leaked to anyone who finds the repo.
- **There are usually two scopes** for the same secret: your own machine (a local `.env` file
  that is *not* committed) and the live site (set in the host's dashboard, e.g. Vercel's
  environment variables). The same key often must be set in both places — forgetting the live
  one is a top cause of "works locally, breaks in production."
- **Publishable/public keys vs. secret keys** — some tools (like Stripe) give both. The
  publishable one is safe in frontend code; the secret one must stay server-side in an env
  var. Never mix them up.

Flag secret-handling every time a key appears. It's the one habit where a mistake is genuinely
costly.

## Test mode vs. live mode (anything with money)

Payment tools run in two worlds: a **test/sandbox mode** with fake cards and no real money,
and a **live mode** with real charges. Build and verify everything in test mode first. Going
live is a deliberate switch that swaps the keys (test keys → live keys) — and it's a frequent
gotcha to leave test keys in production (no real charges happen) or accidentally ship live keys
while developing (real charges happen). Always know which mode the user is in.

## "Works locally, breaks live" — the usual suspects

When something runs on the user's machine but fails on the deployed site, it's almost always
one of:
- An **environment variable set locally but not on the host.**
- A value that points at the local setup (a localhost URL, a test key) that needs the
  production value.
- A **build step** that differs between machine and host.

This pattern is common and fixable; it's not a sign anything is deeply wrong.

## Propagation and patience

Some changes aren't instant. DNS changes (domains) can take minutes to hours to take effect
everywhere; a new deploy takes a bit to go live. "It's not working yet" is often "it's not
done propagating yet." Before debugging, confirm whether you're just waiting.

## Verify, don't assume

End every tool's setup with a concrete success signal: "you'll know the database is connected
when you can see your tables in the dashboard," "you'll know email works when this test message
arrives." Setup that's never verified tends to fail silently and surface later at the worst
time.

## Only set up what the product needs now

A default kit exists, but it's not a checklist to complete. A free content site needs no
payments; a tool without user accounts needs no email yet. Set up the tool when there's a real
need for it, not preemptively. Every extra tool is another account, another bill, another thing
that can break. Fit the kit to the product.
