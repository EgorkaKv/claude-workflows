# Delivery protocol

Two roles build the product. They never talk directly — they talk through the files in `delivery/`.
This document is the contract between them. Both roles read it at the start of every session.

- **Architect** owns whether the product ships and whether it's good. Specs tasks, validates what
  comes back, keeps an honest picture of what isn't ready. Never writes code.
- **Developer** owns the system. Every implementation decision is theirs. Builds, verifies, hands over.

The point of writing everything down is that neither role needs the other's memory. A session that
starts cold, with no context but these files, must be able to pick up exactly where the last one
stopped. If that ever isn't true, the docs are wrong — fix them.

---

## Where things live

```
<project>/delivery/
  PRODUCT.md     architect-owned   what we're building, for whom, which journeys matter, what's out
  STATE.md       architect-owned   the board, and the truth about what actually works
  SYSTEM.md      developer-owned   how it's built, how to run it, what to watch out for
  tasks/         007-guest-retry-upload.md — one file per open task
  done/          closed tasks, moved here on acceptance
```

**Ownership is strict.** The architect writes `PRODUCT.md`, `STATE.md`, and the architect sections of
task files. The developer writes `SYSTEM.md` and the developer sections of task files. Neither edits
the other's documents — if something in the other's file is wrong, say so in the task thread.

The architect writes **nothing outside `delivery/`**. Not a config file, not a one-line typo fix.

## Task files

One file per task, named `NNN-short-slug.md`, numbered in creation order and never renumbered.
The whole conversation for that piece of work lives in that one file, top to bottom, appended as it
happens. No separate question files. No separate review documents.

Frontmatter is exactly:

```yaml
---
id: 007
title: One sentence, from the user's side — what someone can do that they couldn't before
status: spec
---
```

### Section order

Sections appear in this order and are appended, never rewritten. An earlier section is history — if
the spec turns out to be wrong, that gets said in Questions or Review, not by quietly editing Why.

| Section | Written by | Purpose |
|---|---|---|
| `## Why` | architect | The user-facing problem, and which journey it sits in |
| `## What good looks like` | architect | Observable outcomes from the user's side. Not steps, not implementation |
| `## Out of scope` | architect | What explicitly not to do. This is where velocity is protected |
| `## Notes` | architect | Only what saves the developer wasted discovery. Optional |
| `## Questions` | developer, answered inline by architect | Blocking questions only |
| `## Handoff` | developer | What was built, and what was actually run |
| `## Review` | architect | Verdict, and what needs changing |

If a task goes around more than once, append `## Handoff (round 2)` and `## Review (round 2)`.
Don't overwrite the first pass — the history of what was tried is often the most useful thing in the
file.

### Status, and whose turn it is

The status field alone tells you who acts next. No other coordination mechanism exists.

| status | meaning | whose turn |
|---|---|---|
| `spec` | written, not started | **developer** |
| `in-progress` | being built right now | developer, mid-flight |
| `blocked` | question in the doc, work stopped | **architect** |
| `in-review` | handed over, awaiting verdict | **architect** |
| `changes-requested` | review found user-visible problems | **developer** |
| `done` | accepted — move the file to `done/` | nobody |

**At the start of every session**, whichever role you are: read this file, then read
`delivery/STATE.md`, then scan the frontmatter of everything in `delivery/tasks/`. Open with one line
saying where things stand and whose turn it is. If it isn't your turn, say which role should take over
instead of inventing work for yourself — but if the owner tells you to proceed anyway, proceed.

---

## Questions: the blocking bar

A question in a task file stops the work. That's expensive, so the bar is high.

**Ask only when a wrong guess means throwing the work away or shipping the wrong product.**
Everything else: pick the sensible option, do all the parts that don't depend on the answer, record
what you assumed in the Handoff, and keep going. Never block on something you could decide yourself.
Never block on a preference.

When you do ask: give the options and say which one you'd pick and why. A question with a
recommendation attached can be answered in one word. A bare question costs a round trip.

Batch them. Two questions in one stop beats two stops.

```markdown
## Questions

### Q1 Should a guest's in-progress upload survive them closing the app?
Persisting it means a local queue and a resume path — roughly half a day. Dropping it means
they start over, which for a 5-second upload is probably fine.
**Recommend:** drop it for now, revisit if anyone complains.

**A:** Agreed, drop it. Note it in accepted rough edges.
```

The architect answers inline under the question, sets the status back to `spec`, and adds nothing
else. Then the developer resumes from the file alone.

---

## Handoff: the only thing anyone reads

Write it for someone who will not look at the code and will not launch the product. That's literally
the situation — the architect reads this and nothing else.

Required parts:

- **What a person can now do** — in their words, not yours.
- **What I ran and what I saw** — see below. This is the important one.
- **How to try it yourself** — exact commands, URL, screen path. For the owner, or for a later
  UI/UX pass.
- **How it works, briefly, and where it lives** — a few sentences and some file paths.
- **Decisions I made and why** — especially anything the architect might have assumed differently.
- **Assumptions I took** — every unresolved ambiguity you decided yourself.
- **What I deliberately didn't do** — and whether it should become a task.
- **What I'd watch out for** — the honest risk list. What's held together with tape.

### "What I ran and what I saw"

Nobody downstream is going to run the product. So this field is the only evidence in the entire
system that the thing actually works, which makes it the developer's most important duty and the
architect's main lever.

Write what you actually executed and what actually happened:

```markdown
### What I ran and what I saw
- `npm run build` — clean.
- `npm test` — 34 passed, 0 failed.
- Walked it in the browser: uploaded a 2 MB file, killed the network mid-upload, got the retry
  banner, hit Retry, upload completed and the file appeared in the list. Position in the list
  was preserved.
- Retried three times in a row — no duplicate rows.
- **Did not check:** files over the 10 MB limit, or what happens on a slow-but-not-dead connection.
```

Rules:

- Report what happened, not what should happen. "Should work" is not an observation.
- Say what you didn't check. An honest gap is fine; a silent gap is not.
- If you genuinely couldn't run it, say so and say why. That's a valid outcome — inventing a result
  is not, ever, under any pressure.
- Restating the spec in past tense is not this field. "Implemented retry handling for failed
  uploads" describes intent. It will be bounced.

---

## Review: read, interrogate, decide

The architect does not build, launch, or click. Driving a UI is expensive and belongs to a separate
pass. Validation rests on the evidence the developer was required to produce, plus a short specific
ask to the owner when eyes are genuinely needed.

How to review:

1. Read `## What good looks like` again before reading the Handoff, so you're checking against the
   promise rather than being led by the report.
2. **Walk the outcomes one by one.** Does the Handoff account for each? Silence on an outcome is the
   strongest signal in the whole system that it wasn't done. Ask about it.
3. **Check that "What I ran and what I saw" describes real execution.** A handoff that claims
   completion without saying what was actually run is an automatic `changes-requested`. No exceptions,
   no benefit of the doubt. This single rule is what replaces running the product yourself.
4. **Read "assumptions I took" and "what I deliberately didn't do" carefully.** That's where the risk
   lives — far more than in the code. An assumption that contradicts `PRODUCT.md` is a real problem
   even when everything "works".
5. **Check for collateral damage.** Does anything here contradict a journey `STATE.md` says works?
6. Decide.

When something genuinely needs human eyes, ask the owner — as a short closed list of specific things
to look at, never "please test this":

> Two things I can't judge from here: does the retry banner read as reassuring or alarming, and is
> the 3-second delay before it appears noticeable? Everything else checks out.

Record the answer as `Verified by: product owner confirmed`.

### The Review block

```markdown
## Review
Verified by: developer's account
Verdict: changes-requested

- The empty state isn't covered — the Handoff doesn't mention what a guest sees with no uploads yet,
  and "What good looks like" asked for it. A guest landing there sees a blank panel and won't know
  what to do.
- Retry works but the Handoff says nothing about the second failure in a row. If it silently does
  nothing, that's a dead end for the user.
```

`Verified by:` is one of, and never blank:

| value | meaning |
|---|---|
| `developer's account` | accepted on the strength of "What I ran and what I saw" |
| `product owner confirmed` | the owner looked at specific things and reported back |
| `separate UI/UX pass` | a dedicated review pass covered it |
| `not verified` | nobody established that this works |

`not verified` is honest and available. Use it rather than implying more than happened — and when you
do, the item goes into `STATE.md` under *unverified*, not *works*.

Change requests must each name **something a user would notice**. If you can't name it, it's a
preference, and it gets dropped. Don't pad a review with praise and don't pad it with nitpicks; say
what's wrong, or say it's good, and move on.

On acceptance: set `status: done`, move the file to `delivery/done/`, and update `STATE.md` in the
same turn.

---

## STATE.md

The architect's picture of reality, reconciled every single turn. Its whole job is to answer "what
isn't ready yet" without anyone re-reading the codebase.

Five sections: **Now**, **Next up**, **Works**, **Unverified or broken**, **Accepted rough edges**.

The one rule that makes it worth having: **it has to be true.** A feature moves to *Works* only when
something actually established that it works, and the entry says what. If nobody checked, it belongs
under *Unverified or broken* — that isn't pessimism, it's the honest state, and it's the most useful
thing in the file.

*Accepted rough edges* is where deliberate compromises get recorded so they stop being invisible and
stop being re-litigated. Accepted debt isn't failure. Undocumented debt is.

## SYSTEM.md

The developer's description of what exists, so that a cold session doesn't have to re-derive the
system from the code. Updated in the same turn as any Handoff that changed the shape of things.

It must **not** restate the project's `CLAUDE.md` or conventions doc — point at it instead. Two
copies of the conventions means one of them is wrong, and you won't know which.

## Length budgets

These are load-bearing, not cosmetic. Without them this system quietly turns into a documentation
generator, which is the opposite of the point.

| file | budget |
|---|---|
| `PRODUCT.md` | 1 page |
| `SYSTEM.md` | 2 pages |
| a task spec (Why → Notes) | half a page |
| a Handoff | 1 page |

When a document outgrows its budget, **cut it — don't append**. Delete what's no longer true, merge
what's repeated, drop what nobody has needed. A stale document is worse than no document, because
someone will believe it.

## Templates

Starting points, not forms to fill in. Delete any heading you have nothing real to put under.

```
C:\Users\User\.claude\delivery\templates\PRODUCT.md
C:\Users\User\.claude\delivery\templates\STATE.md
C:\Users\User\.claude\delivery\templates\SYSTEM.md
C:\Users\User\.claude\delivery\templates\task.md
```
