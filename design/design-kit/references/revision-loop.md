# Revision loop — fixing the Kit from screenshots

Read this when generated screens come back.

This is the most valuable part of the design layer and the cheapest part for the person you are
working with. They looked at something and reacted. That reaction contains more information than any
answer they could have given to a question, and it cost them nothing to produce.

Your job is to translate it into values.

## The one rule: it is usually the Kit, not the screen

A complaint arrives attached to a screen, so the reflex is to fix that screen. Resist it. If the
spacing feels wrong on the dashboard, it is wrong everywhere and the scale is the problem. Patch the
screen and the same complaint returns on the next one, plus the screens have now drifted apart —
which is the exact failure the Kit exists to prevent.

Fix the value in the Kit, then re-emit the prompts the change touches. Say which ones changed.

The exception is real but narrow: if one screen has a problem no other screen could have, it is a
screen problem. Usually that means too much is on it — and too much on one screen is generally a
scope signal for CORE rather than a layout puzzle.

## Look before you read

Look at the screenshot and form your own judgement before you take their words as the diagnosis.
People are reliable about *that something is wrong* and unreliable about *what*. "Looks cheap" is a
true report of a real perception and almost never a correct diagnosis.

If what you see disagrees with what they said, say so: "you said it feels cramped, but the spacing
matches the Kit — what I see is four things competing at the same weight, so nothing has room. I'd
fix the hierarchy, not the spacing." That is thinking they get for free.

## Translate the reaction into a value

Common reactions and what they usually actually are:

- **"Too airy" / "слишком воздушно"** — the spacing scale is one step too large, or line-height is
  too loose. Cut the scale, do not cut content.
- **"Cramped"** — check density first. If density was decided as high on purpose, cramped may be
  correct and the real problem is that this screen carries too much, which goes back to CORE.
- **"Too many cards"** — the elevation rule is wrong. Flat surfaces separated by single-pixel
  dividers instead of elevated cards. One value, enormous visual effect, and the most common Kit
  error in generated UI.
- **"Looks cheap"** — almost never colour. It is usually one of three things: the type scale has no
  contrast (everything landed between 14 and 16), too many weights are in play, or borders are pure
  grey at full opacity. Check them in that order.
- **"Looks like every other AI app"** — go to the AI tell list. In practice it is the accent colour
  and the radius, and occasionally gradients that arrived without being asked for.
- **"I can't tell where to look"** — too many elements at the same visual weight. The fix is almost
  always removing emphasis from everything else, not adding more to the thing that should dominate.
- **"Too corporate" / "too serious"** — contrast and radius, plus the copy tone in the prompts. Do
  not reach for illustration; it is rarely the actual gap.
- **"Doesn't fit on a phone"** — density was derived for the wrong context. That is a Kit-level
  derivation error: go back to CORE, re-read who this is for and in what conditions, and expect
  several values to move.
- **"Fine, but boring"** — the direction was the safe one. This is the one case where the fix is a
  different direction rather than different values; offer one of the rejected directions rather than
  nudging the current one.

## Change the smallest number of values

Every value you move is a chance to break something that was working. Find the one or two values
that explain the complaint and move only those. Then say what you changed and what you expect it to
do — that lets them check your reasoning by looking at the next screenshot rather than by reading
your argument.

If a complaint requires more than three values to move, it is not a values problem. It is either the
direction or the density, and both are worth saying out loud rather than absorbing quietly.

## What not to do

- **Do not add a component to solve a layout problem.** A new component is a Kit change with reach
  into every screen. Solve it with what the inventory already has, or say explicitly that the
  inventory is missing something and why.
- **Do not ask what they want instead.** They came back with a reaction because reacting is cheap.
  Turning it into a specification request hands the expensive work back to them and dismantles the
  point of this loop. Decide, change, re-emit, and let them react again.
- **Do not restyle in the prompt while leaving the Kit stale.** The moment the prompts describe
  something the Kit does not, the system has stopped being the source of truth and every later
  screen will drift.
- **Do not defend v0.** It was built to be wrong in a few places. Finding one is the loop working,
  not a mistake to explain.

## Then re-emit

Update the Kit, name what moved and why in one line each, and re-emit the prompts affected. Add the
change to the Kit's decided-and-rejected section, briefly, so the same value does not get argued
twice.

If several rounds keep circling the same area, stop turning the crank and say what you think is
actually going on — most often that density or direction was derived from a CORE that has since
changed underneath it.
