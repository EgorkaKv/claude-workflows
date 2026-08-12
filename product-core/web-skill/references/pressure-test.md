# Pressure test — attack the Core before reality does

Run this when the Core looks finished, and whenever the person asks you to attack it. It is required
before you call anything done.

It exists because the characteristic failure of this layer is not a missing section. It is a
beautiful, internally consistent document describing a product nobody wants — and a document like
that is harder to notice than an incomplete one, because everything in it agrees with everything
else.

Take the position honestly. You are trying to find the thing that kills this, not to be contrarian
and not to produce a balanced risk register. One real hole found is worth more than ten hedged
concerns, and a pressure test that concludes "some risks to monitor" was not a pressure test.

## Find the load-bearing assumption

Go through CORE claim by claim and ask: **if this were false, what would still stand?**

Most claims fail small — a wrong guess about a feature costs a sprint. Usually one or two claims,
if false, make the entire thing pointless. Those are the load-bearing ones, and they are almost
never about the feature set. They are assumptions about behaviour:

- that people know they have this problem
- that they care enough to change what they currently do
- that they will bother, on a Tuesday, when nothing is forcing them to
- that the person who feels the pain can authorise a fix
- that the problem stays a problem once they have looked at it twice

Name them out loud, in the conversation. A Core with two unnamed load-bearing assumptions is not
finished, however complete it looks.

## Then ask what would falsify each one cheaply

For every load-bearing assumption: what is the cheapest thing that would tell you it is wrong? Ten
conversations, a landing page, doing the job by hand for one person for a week, watching someone
attempt it in their current tools.

If the only answer you can find is "build it and see", that is itself the finding — and it belongs
in LOG's open questions as the most important thing not yet known, not buried as a caveat.

## Look for the product that gets adopted, not the one already in use

Cores are almost always written from the point of view of a happy existing user, because that is the
pleasant version to imagine. Attack the two states nobody wrote down:

- **Day 0.** Why does anyone start? What makes the first five minutes worth it before any data, any
  habit, any configuration exists? An empty product is the state most products actually die in, and
  it rarely appears anywhere in the Core.
- **The second visit.** What brings them back before the habit exists? "It's useful" is not a
  mechanism. Something has to either remind them, hold something of theirs, or have left the job
  unfinished in a way they want to resolve.

## Interrogate every feature

For each thing in "what we're building", ask why it is really there. Three bad reasons, all common:

- **It is obvious.** Everyone in the category has it, so nobody asked whether this product needs it.
- **It is satisfying to build.** The most dangerous category, because it survives every review by
  looking like progress.
- **It was in the original idea** and nobody has re-examined it since the idea changed underneath it.

Then the direct test: **what happens if you ship without it?** If the answer is "not much", it is
not v1, and moving it to the not-building list is the single cheapest improvement available.

## Check that the segment is a segment

- If you cannot name one specific person, it is not a segment.
- If two people who both fit the description would want opposite things from the product, it is not
  a segment — it is two, and the Core is quietly serving neither.
- If it is defined by the tool people use rather than the problem they have, it is a channel wearing
  a segment's clothes. Useful for finding them, useless for deciding what to build.

## Check the "not building" list for honesty

If it contains only things nobody wanted anyway, it is decoration and it will not protect anything.
A real out-of-scope list hurts slightly to read — there should be at least one item on it that the
person still feels the pull of. If there isn't, the scope has not actually been cut yet.

## Check the switching cost

What does this person do today? Whatever it is — a spreadsheet, a WhatsApp group, three tabs, or
nothing at all — it works well enough that they are still doing it.

Being better is usually not enough. It has to be better **on the dimension they actually feel**, by
a margin large enough to pay for the cost of change: learning it, moving their data, admitting the
old way was bad, and getting whoever else was involved to go along with it. Cores routinely compare
against a competitor and skip this, which is why they overestimate adoption.

## Check whether it survives without the founder

Does the Core describe a product, or a service this person will personally operate? Both are
legitimate, and they lead to entirely different builds. Confusing them is common and expensive: it
produces a Core that reads like software and a reality where every customer needs an hour of manual
work nobody costed.

## Find the pivot that is already visible

Adversarial work should not only subtract. If the load-bearing assumption is the weak point, ask
what the same material would build if that assumption turned out to be false. Frequently the
strongest version of the idea is sitting in the Observations section, in a competitor's mistake or
an odd behaviour that got noticed and then filed.

Offer it as an alternative, not as a replacement. It is their call.

## How to report what you found

Lead with the single thing most likely to kill this, stated in one or two sentences with no
softening. Then at most two or three others, ordered by how much they matter, not by how confident
you are.

Say what you could not attack — a claim you have no way to evaluate is a real limit on the test and
pretending otherwise makes the whole exercise decorative.

Then say plainly whether you would proceed as written, proceed with something cut or changed, or go
back and check something first. The findings, and the assumptions you named, go into LOG's open
questions — that is what makes the next session start from what is genuinely unknown rather than
from what is comfortable.
