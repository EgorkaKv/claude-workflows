# Monetization — price as a product decision

Read this when the conversation turns to price, business model, or who pays.

It exists because these questions get answered with a label — "credit-based", "freemium", "seats" —
when what they deserve is an argument. A monetization model is not a financial choice bolted on
after the product is designed. It decides who shows up, how often they use the thing, which
features are worth building, and what the product does to itself over time. Getting it wrong
quietly poisons the feature set.

## Start from behaviour, not from revenue

The useful question is never "how do we make money from this". It is **"what does this pricing make
people do?"**

Every model rewards a behaviour and punishes another. Before comparing revenue, work out which
behaviour the product actually needs in order to work. If the product only becomes valuable through
frequent, exploratory, low-stakes use — a writing tool, a search tool, anything where the habit is
the value — then any model that makes people hesitate before each use is fighting the product. If
the value is concentrated in rare, high-stakes moments, the opposite holds, and charging for the
habit will feel like extortion.

Decide that first. Then pick the model that pays for the behaviour you want.

## What each model quietly assumes

- **Subscription** assumes the product is used often enough that people stop noticing they pay for
  it. Below roughly monthly use, every renewal becomes a fresh purchase decision and churn is
  structural rather than fixable. Subscription also caps the upside from heavy users and lets light
  users subsidise them — usually a good trade early, because predictability is worth more than
  extraction when you are still learning what the product is.
- **Credits and usage-based pricing** assume value scales with volume *and* that people can predict
  their own volume. The hidden cost is rationing: every action becomes a small purchase decision,
  which suppresses exactly the exploratory use that builds habit. For anything AI-shaped this is
  severe — users stop experimenting, never discover the good use cases, and conclude the product is
  fine but unnecessary. Credits earn their place when usage is genuinely spiky and genuinely
  expensive to serve.
- **Per-transaction or commission** assumes there is a discrete valuable event you can sit on top
  of, and that you cannot be routed around once people know each other. Alignment is excellent —
  you get paid when they succeed — but you only get paid when they succeed, which means you are
  underwriting their conversion problem as well as your own.
- **One-time purchase** assumes near-zero cost to serve and no expectation of ongoing improvement.
  Rare now, and worth naming honestly when someone proposes it: the objection is not revenue, it is
  that you have promised nothing and can therefore be abandoned without cost.
- **Seats** assume a team, and immediately create an incentive to under-provision seats and share
  logins. If the product's value grows with how many people in the org use it, seats price against
  your own adoption.
- **Free with ads** assumes enormous scale and that attention is the product. Almost always
  incompatible with a narrow, high-intensity pain, because a narrow audience cannot produce enough
  attention to matter.

## When the payer is not the user

Three roles, often three people: whoever feels the pain, whoever signs, and whoever can veto.

Serve only the user and the product gets loved and not bought. Serve only the buyer and it gets
bought and not used — which surfaces a year later as churn nobody can explain, because the usage
data was never good and nobody was looking. When these roles diverge, the Core needs to name all
three, and the feature set needs at least one thing that exists purely for the buyer: reporting,
control, auditability, or a way to look good internally for having chosen it.

## Pain intensity is the ceiling

People pay to stop bleeding. They do not pay to be mildly delighted, however elegant the solution.

The practical test: **what do they do about this problem today, and what does that cost them** in
money, hours, or risk? Your price lives below that number, not below some abstract sense of value.
And if the honest answer is "nothing, they live with it", then the competitor is inertia, the
willingness to pay is near zero regardless of how good the product is, and the conversation needs
to go back to whether the pain is real — not to which pricing model to use.

## The free tier is a product decision

A free tier works when the free user creates value for the paying ones — network effects, content,
a referral surface — or when the pain grows with use, so the free tier is a working demonstration
of a problem the person is about to have.

It fails, expensively, when the free tier fully solves the pain. Then you have built two products,
and the good one has no customers. The question to ask is not "how much do we give away" but
**"what does the free user run into that makes the paid version obvious?"** If there is no honest
answer, there should be no free tier — a trial is a different and usually better instrument.

## Worked example: "let's drop the subscription and go credit-based"

This is what engaging with the question looks like, as opposed to filing it.

**What changes.** Revenue becomes unpredictable in both directions. Scope appears that did not
exist before: metering, a balance the user can see and trust, a top-up flow, a decision about
whether credits expire, and support conversations about all of it. The pricing page turns into a
calculator, which raises the bar to first purchase — people who cannot estimate their usage
postpone the decision, and postponed decisions are lost ones.

**Who you win.** Heavy irregular users who felt overcharged by a flat fee. People who cannot get a
recurring line item approved but can expense a one-off top-up. Anyone whose usage is genuinely
seasonal.

**Who you lose.** Light regular users who liked not thinking about it. Buyers whose finance function
prefers a predictable subscription and treats variable spend as a problem. And, most importantly,
the exploratory user — the one who would have discovered the use case that made them a customer for
three years, but who stopped poking at it once each poke had a price.

**What would have to be true.** That usage varies enough between users for a flat price to feel
unfair to a meaningful share of them. And that value per action is legible enough that someone can
tell whether a credit was well spent — because if they cannot, every charge feels arbitrary and the
product feels expensive at any price.

**Second order.** People optimise for spending fewer credits. If the product's value comes from
being used freely, you have just priced against your own retention, and the metric that degrades is
the one you will not notice for months.

**A position worth stating.** For products whose value is a habit, a subscription with generous
limits beats credits, and the honest problem being solved by "credits" is usually a packaging
problem — a flat price that is wrong for a segment, which a second tier fixes more cheaply than a
new model does. Credits earn their place when usage is genuinely spiky *and* genuinely expensive to
serve, and where the person can see what each unit bought them.

## Questions worth actually asking

- How often does the person come back? The answer decides subscription versus anything else more
  than any other fact.
- What does it cost you to serve one more use? If that number is meaningful, usage-based is a real
  candidate rather than a preference.
- What do they spend on this problem today, and to whom?
- Who signs, and what do they need in order to defend the choice internally?
- What behaviour does this price discourage — and can the product survive that behaviour being
  discouraged?
- What is the cheapest way to find out you are wrong about the price? Almost always a conversation
  or a checkout page, not a launch.

Whatever comes out of it: the model, the reason, and the alternatives you rejected all go into LOG.
Pricing gets re-litigated more often than anything else in a product, and the argument is what
stops it being re-litigated from scratch every time.
