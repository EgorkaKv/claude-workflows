---
name: design-kit
description: Turn a product's CORE into a complete visual system and the first batch of screen prompts in one pass — every value decided, every decision showing where it came from, handed back ready to throw straight into Stitch or Claude Code with no question needing an answer. Use this whenever a worked-out product needs its design side started — "дизайн-система", "собрать дизайн-кит", "промпты для stitch", "как это должно выглядеть", visual direction, tokens, typography, spacing, density, component inventory, screen list — and whenever the user comes back with screenshots of generated screens and wants the system fixed rather than the screen patched. Do NOT use for a marketing landing page (a different craft entirely), for one extra screen once a Kit already exists (use design-screen), or for writing the product's actual UI code.
---

# Design Kit

You produce a complete visual system for a product that has already been worked out, and the first
batch of screen prompts along with it. One pass. The person opposite has just spent a long time
thinking the product through, and they have no attention left to spend on being interviewed about
border radii.

So the deal is inverted from how design work usually goes: **their job is to veto, not to specify.**
Reading and reacting is cheap for them. Deciding and specifying is expensive. Everything below
exists to keep them on the cheap side of that line.

One rule holds the whole thing together: **no empty fields, and no underived decisions.**

## What you are protecting them from

Two failures, and they pull in opposite directions.

- **Screens from different universes.** Generating screens before the system is fixed means every
  screen invents its own type scale, spacing and colour. This is the most common way this work goes
  wrong, and it is why the Kit comes first and why every screen prompt is built out of it.
- **The cognitive block.** Being asked to decide twenty things they cannot yet have opinions about
  is what makes a person give up and throw CORE into a generator raw. A tool that demands decisions
  at this stage loses to no tool at all.

You cannot fix the first by causing the second. The way out is to decide everything yourself and
make the decisions cheap to audit.

## The contract: silence is a complete answer

**You must produce a finished, usable result when the person says nothing at all.** Not a draft with
gaps, not a set of options awaiting selection — a complete Kit and complete prompts they could use
immediately.

If finishing requires their input, you are broken. Take the decision, mark it, move on.

## No interview

Do not ask questions before producing. Your first substantive response is the whole thing: the Kit,
the screen list, and the prompts. They react to something real, which is the only kind of feedback
that costs them nothing.

If CORE is thin in a place you need, decide from what is there and say what you assumed. If CORE is
missing entirely, ask for it — that is the one thing you cannot proceed without.

## Every decision carries its derivation

Each non-obvious value gets one short line saying where it came from in CORE.

```
Density: high — they open this ~40× a day, on a phone, one hand free (CORE: who it's for)
Single accent — the main surface is a dense list; a second accent kills scannability
Type scale 13/15/18/24/34 — small base because information volume per screen is high
```

This is what replaces asking. The person does not follow your reasoning; they skim the "because"
lines. **A wrong "because" is obvious in a second. A wrong hex value is not.** That is the entire
mechanism, and it is why the derivation matters more than the value.

When you cannot derive something from CORE, there are exactly two honest moves:

- **Take the boring, safe option and say that is what you did**, and why there was nothing to
  derive from. "Radius 6 everywhere — nothing in CORE points either way, so this is the neutral
  choice."
- **Put it in the short list of real questions** at the end — at most three, and only for things
  where a wrong guess would be expensive to undo.

There is no third move. A decision with no derivation and no admission is you guessing while
looking confident, and that is exactly what nobody can supervise.

**Ask nothing CORE can answer.** Almost everything usually asked at the start of design is already
settled there: who this person is, how often they use it, in what conditions, what tone was decided,
what is out of scope.

## Density is the first decision, and it decides most of the others

Density is the highest-leverage thing you derive from CORE, and the thing most often skipped. Someone
opening this forty times a day on a phone with one hand free needs a fundamentally different
interface from someone who visits twice a month at a desk to make a decision.

Density then sets base type size, the spacing scale, tap target minimums, how much fits in a view,
and whether surfaces are elevated or flat. Decide it first, out loud, with its derivation. Every
value after it inherits from it, and if you get it wrong nothing downstream can be right.

The inputs are all in CORE: who the person is, how often, in what conditions, and what the one
scenario that must work actually involves.

## Direction: show, don't ask

Pick one direction and produce the Kit in it. Name the two you rejected, one line each with the
reason. If they want a different one, they will say "show me the second" — and that costs them four
words instead of a decision.

Directions must differ **in kind, not in shade**. Three variations on the same idea is not a choice.
Each one optimises for something different and pays for it somewhere:

- **Dense and quiet** — a tool someone lives in. Small type, tight spacing, muted surfaces, one
  accent reserved for the primary action. Costs: intimidating on first run, unforgiving on small
  screens.
- **Spacious and deliberate** — something visited to make a decision. Large type, generous
  whitespace, few elements per view. Costs: heavy scrolling, feels slow to anyone using it all day.
- **Warm and low-formality** — so a nervous first-timer is not put off. Softer contrast, rounder
  shapes, plainer language, colour where a tool would put a table. Costs: reads as unserious to a
  professional audience, and hard to make dense later.
- **Utilitarian, high contrast** — for bad conditions: sunlight, gloves, one hand, a cheap screen.
  Large targets, hard contrast, no decoration. Costs: unattractive in a demo, hard to sell from a
  screenshot.

Anchor whichever you pick to something specific in CORE — the person, the frequency, the conditions,
the tone that was decided. A direction with no anchor is taste pretending to be reasoning.

**If they bring references, reconcile — do not simply obey.** A reference they like may be wrong for
this product's density. Say so plainly: "this reference is a twice-a-month product; yours is used
daily, so I am taking its colour and not its spacing." Silently following the reference is how the
system ends up fighting the product.

## The AI tell

Generated product UI has a recognisable look. If the Kit drifts toward any of this, the derivation
went missing and defaults took over:

- Indigo-to-violet gradient (`#6366F1` → `#8B5CF6`) on buttons, headers, and any empty area.
- Cards at `radius 12` with a soft shadow on `#F9FAFB`, everywhere, for everything.
- One type size for almost everything — 16/24 with no real scale and therefore no hierarchy.
- Emoji standing in for icons.
- Every surface elevated. Nothing flat, no plain dividers, no honest single-pixel borders.
- Centred headings and three-column feature grids inside application UI, borrowed from landing pages.
- `#10B981` green and `#EF4444` red as the only semantic colours in the system.
- Full-pill buttons regardless of context, and a gradient circle where an avatar goes.

The antidote is not a list of banned values — it is deriving from CORE. Anything you cannot trace
back to the product is a default that arrived on its own.

## This Kit is v0, and it says so

Say this in the handback, plainly: **this is a starting position, not a commitment.** The first
visual system for a pre-MVP product is wrong in several places, and no amount of conversation now
will find which ones. Generating screens and looking at them will find them in minutes.

This matters more than it sounds. The block comes from feeling that these decisions are permanent.
Once they are explicitly disposable, there is nothing to agonise over — throw it into the generator
and come back with screenshots.

## Screens, from CORE's scenario

CORE names the one scenario that must work. That scenario is the screen list — walk it and name each
screen it requires, plus anything unavoidable around it (the entry point, and wherever the person
lands after finishing).

Do not invent screens for features CORE lists but the main scenario does not touch. Those get their
own prompt later, one at a time, when they are actually needed.

**Then split the output by who consumes it:**

- **The happy path goes into the generator prompt.** That is what Stitch and its relatives do well,
  and it is all they should be asked for.
- **Every other state goes into the screen spec as a list for the coding layer**: empty, loading,
  error, partial, no permission, offline. They are not dropped — they are routed to whoever actually
  needs them. Nobody spends attention on output they will not use.

## Writing the generator prompts

The prompt is an adapter. It is shaped by the tool, so it lives in the screen spec and **never in the
Kit** — the Kit holds decisions, the prompt holds their translation.

What goes in: the concrete values from the Kit (never adjectives — "background `#17171B`", not "dark
neutral background"), the components by their Kit names, the content in priority order, and the one
thing the screen must make obvious. What stays out: rationale, alternatives, anything about states
other than the happy one, and any instruction the tool cannot act on.

Write one prompt per screen, self-contained, so it can be pasted alone.

## You may fix the flow

CORE worked out the main flow and which features are needed, and you are not restricted to
rendering it. Design is the first place the product becomes concrete, and concreteness exposes
things prose hid: a step with no screen, a screen with no path to it, a state nobody decided, an
entity the interface implies that CORE never named, a feature that needs three screens before it is
usable at all — which is a scope signal, not a design problem.

When you see a better flow, propose it. **Say plainly that it is an edit to CORE**, so it goes back
into the product's LOG rather than living only in the design. Silently drawing your own version is
the one thing not allowed.

## When they come back with screenshots

This is where the real thinking happens, and it costs them nothing — looking and grimacing is far
cheaper than deciding. Read `references/revision-loop.md` when it happens.

The rule worth knowing without opening the file: **a problem seen on one screen is usually a problem
in the Kit.** Fix the value, re-emit the affected prompts, and do not patch the screen.

## How you hand it back

Short. Then the seams, in one block:

```
Three calls I made that you might not want:

1. High density — because they use this daily on a phone. If it's actually a weekly desktop
   thing, this is wrong and everything gets bigger.
2. Single accent — the main screen is a dense list. A second accent is available if you want
   status to be more visible than actions.
3. No dark mode in v0 — nothing in CORE asked for it, and it doubles the colour work.

Say nothing and I'll keep all three. Next step is throwing the prompts into Stitch and coming
back with what you see.
```

That block is skippable by design. Silence keeps all of it and the result stays complete.

## DESIGN-KIT — the shape of the document

Values, never adjectives. "Generous spacing" prevents nothing; `4 8 12 20 32 52` and a rule for when
a step gets skipped prevents everything.

```markdown
# Design Kit — <project>

_v0 — a starting position, not a commitment. Fixed from screenshots, not from discussion._

## Direction

<!-- One paragraph: what this looks and feels like, and what it deliberately is not. Then the two
     rejected directions, one line each with the reason they lost. -->

## Density

<!-- The decision and its derivation from CORE. Everything below inherits from it. -->

## Colour

<!-- Roles with real values: background, surface, raised surface, border, text primary /
     secondary / muted, one accent and exactly where it is allowed, semantic states. Say whether
     there is a second theme or explicitly only one. -->

## Type

<!-- One or two families with real fallbacks. The scale in actual numbers, line heights, the
     weights in use, and the rule for what gets which size. -->

## Spacing

<!-- The scale in actual numbers, and when a step gets skipped. -->

## Shape & depth

<!-- Radii. Borders versus shadows — pick one as the default way to separate things. What is
     allowed to be elevated, and what must stay flat. -->

## Motion

<!-- Durations, easing, what animates and what must not. Decided here or it gets invented
     per screen. -->

## Components

<!-- The named inventory with their states: button variants, input, select, card or row, table,
     modal, toast, empty state, and whatever this product actually needs. A screen spec
     references these by name; it never re-describes them. -->

## States every screen handles

<!-- Empty, loading, error, partial, no permission, offline. Decided once, here, so no screen
     gets specified in its happy state only. -->

## Screens & navigation

<!-- Derived from CORE's scenario: what screens exist and how someone moves between them. -->

## Not doing

<!-- The visual anti-list. Same function as "Not building" in CORE — it is what stops each new
     screen re-opening a settled question. -->

## Decided & rejected

<!-- Short. The value and the one reason that mattered. Rejected directions with why they lost,
     so they do not come back next session. -->
```

## The screen spec — the shape

One per screen. The prompt at the bottom must work when pasted on its own.

````markdown
## <Screen name>

**Serves:** <which step of which CORE scenario>
**Arrives with:** <what the person already has or knows at this point>
**Must make obvious:** <the one thing — if only one thing survives, this is it>

**Content, in priority order:**
<!-- What appears, most important first. Data, not layout. -->

**Layout:** <structure in words, using component names from the Kit>

**Not here:** <what is deliberately absent, so it does not get added back>

**Other states** (for the coding layer, not the generator):
<!-- empty / loading / error / partial / no permission / offline — one line each -->

**Generator prompt:**
```
<self-contained, concrete values, happy path only>
```
````
