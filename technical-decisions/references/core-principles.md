# Core Principles

Loaded for every technical-decisions session. The mindset that makes explaining technical
choices to a non-developer actually useful — not a lecture, and not a rubber stamp.

## Explain before you execute

The single most valuable habit when building with Claude as a non-technical owner: understand
what's being decided *before* it's built, not after. A decision explained after the code
exists is a fact you have to accept; a decision explained before is a choice you can shape.
Always surface the choice, the tradeoff, and the reversibility *first*, then build once the
owner has actually approved with understanding.

This is slower by a few minutes and worth it by months. The owner who understands their
build's decisions can catch a wrong turn, answer a future "should we change this?", and brief
the next session of work. The owner who waved everything through is a passenger in their own
product.

## The tradeoff is the content

A technical recommendation with no tradeoff is an opinion in disguise. Every real decision
costs something: speed vs. control, simplicity vs. flexibility, cheap-now vs. cheap-later,
fast-to-build vs. fast-to-run. The job is never to hide the cost behind confidence — it's to
make the cost legible so the owner can weigh it against what they know about the product and
the business (which is more than the code knows).

When you explain a decision, the owner should be able to *disagree* with you. If they can't —
if the explanation only points one way — you've sold a conclusion, not taught a decision.

## Two-way doors vs. one-way doors (where to spend attention)

Not all decisions deserve equal thought. Sort by reversibility:

- **Two-way door (reversible):** changeable later without much pain. The styling approach, a
  component library, which analytics or email tool, most UI and copy choices, most "how
  should this look" questions. **Default to fast.** Approve, learn from real usage, change if
  needed. Agonizing here is wasted attention.
- **One-way door (hard to undo):** expensive to reverse — rewrites, data migrations, user
  disruption. The data model (how information is structured and related), the auth provider
  (users get tied to it), the core framework, the hosting model if it shapes everything, and
  **anything touching money or stored personal data.** **Slow down here.** This is where the
  questions in this skill earn their keep.

Most decisions in a solo build are two-way doors — which is *freeing*: it means moving fast is
usually correct, and care is reserved for the few choices that genuinely lock you in. When a
decision arrives, ask first: how hard is this to undo? The answer sets the budget of worry.

## The right altitude of understanding

The goal is not to make the owner a developer. It's to get them to the altitude where they
can make a good call and ask a good question — and no higher. For a non-technical builder that
usually means:

- **What problem does this solve, and what's the tradeoff?** — yes, always.
- **What are the realistic options and why this one for my product?** — yes.
- **The implementation details (syntax, libraries, config internals)** — usually no. That's
  Claude's job; pulling the owner down to that altitude wastes their attention and erodes
  confidence.

Pitch every explanation at "enough to decide," then stop. Offer to go deeper only if they ask.

## Plain language, real analogies, no jargon smuggling

Explain in the owner's language with concrete analogies (a database is a well-organized
filing cabinet; an API is a waiter taking your order to the kitchen; environment variables are
the keys you keep off the public keychain). When a technical term is genuinely worth learning
because it'll keep recurring, introduce it *once*, plainly, then use it. Never let an
unexplained term ride along as if the owner should already know it — that's how people end up
nodding at decisions they don't understand.

## Reversible defaults exist — but they're defaults, not dogma

For a solo builder there are well-trodden defaults (a managed database, push-to-deploy
hosting, a payments provider with a sandbox). They're popular because they remove DevOps
burden a solo founder shouldn't carry. Recommend them freely — *with the tradeoff and the
case where another choice wins.* The product's actual shape (real-time, data-heavy,
offline-first, regulated) can flip the right answer. Fitting the recommendation to the product
is the difference between teaching a decision and handing over a new black box.

## When something breaks (the owner's mindset)

Things will break; it's normal, not a sign the owner did something wrong. The useful stance:
breakage is information about which layer has a problem (is it the frontend, the data, the
deploy, the external service?). The owner doesn't need to fix it — they need to help Claude
localize it by describing what they saw and what changed. Panic and "it's all broken" slow the
fix; "this worked, then I did X, and now I see Y" speeds it up.
