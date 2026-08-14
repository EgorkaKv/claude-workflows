# Delivery protocol

Two roles build the product and never talk directly — they talk through the files in `delivery/`.
This document is the mechanics: where things live, what the statuses mean, what each document has to
contain. Judgment lives in the roles themselves.

A session that starts cold, with no context but these files, has to pick up exactly where the last
one stopped. When that isn't true, the docs are wrong — fix them.

## Where things live

```
<project>/delivery/
  PRODUCT.md     architect   what we're building, for whom, which journeys matter, what's out
  STATE.md       architect   the board, and the truth about what actually works
  SYSTEM.md      developer   how it's built, how to run it, what to watch out for
  tasks/         016-shortlist-pagination.md — one file per open task
  done/          closed tasks, moved here on acceptance
```

Ownership is strict: each role writes its own documents and its own sections of task files, and never
edits the other's. If something in the other's file is wrong, say so in the task thread.

The architect writes nothing outside `delivery/`.

## Task files

`NNN-short-slug.md`, numbered in creation order, never renumbered. The whole conversation for that
piece of work lives in that one file, appended top to bottom. No separate question files, no separate
review documents.

```yaml
---
id: 016
title: One sentence from the user's side — what someone can do that they couldn't before
status: spec
---
```

| Section | Written by | Purpose |
|---|---|---|
| `## Why` | architect | the user-facing problem, and which journey it sits in |
| `## What good looks like` | architect | observable outcomes from the user's side — not steps |
| `## Out of scope` | architect | what explicitly not to do |
| `## Notes` | architect | optional — only what saves the developer wasted discovery |
| `## Questions` | developer, answered inline by the architect | blocking questions only |
| `## Handoff` | developer | what was built, and what was actually run |
| `## Review` | architect | verdict, and what needs changing |

Sections are appended, never rewritten — an earlier one is history. If the spec turns out to be
wrong, that gets said in Questions or Review, not by quietly editing `Why`. A second round appends
`## Handoff (round 2)` and `## Review (round 2)`.

## Status — the only coordination mechanism

| status | meaning | whose turn |
|---|---|---|
| `spec` | written, or a question just got answered | **developer** |
| `blocked` | question in the doc, work stopped | **architect** |
| `in-review` | handed over, awaiting verdict | **architect** |
| `changes-requested` | review found user-visible problems | **developer** |
| `done` | accepted — file moves to `done/` | nobody |

Whoever changes the situation changes the status, in the same turn: developer → `blocked` when
asking, `in-review` when handing over. Architect → `spec` when answering a question,
`changes-requested` or `done` when reviewing.

At the start of a session, whichever role you are: scan the frontmatter in `delivery/tasks/` and say
in one line where things stand and whose turn it is. If it isn't yours, say which role should take
over rather than inventing work — unless the owner tells you to proceed anyway.

## Questions

A question stops the work, so ask only when a wrong guess means throwing the work away or shipping
the wrong product. Give the options and say which one you'd pick — a question with a recommendation
attached can be answered in one word.

```markdown
### Q1 Should a guest's in-progress upload survive them closing the app?
Persisting it means a local queue and a resume path — roughly half a day. Dropping it means they
start over, which for a 5-second upload is probably fine.
**Recommend:** drop it for now, revisit if anyone complains.

**A:** Agreed, drop it. Note it in accepted rough edges.
```

The architect answers inline, sets the status back to `spec`, and adds nothing else.

## Handoff

Written for someone who will not read the code and will not launch the product — that is literally
who reads it. Use whatever headings fit the work; what matters is that the architect can answer:

- What can a person do now that they couldn't before?
- **What did you run, and what did you see?** — required, always, under that heading.
- How would the owner try it themselves?
- How does it work, roughly, and where does it live?
- What did you decide, assume, or deliberately not do — and what would you watch out for?

### What I ran and what I saw

The only evidence in the entire system that the thing works.

```markdown
- `npm run build` — clean. `npm test` — 34 passed, 0 failed.
- Uploaded a 2 MB file in the browser, killed the network mid-upload, got the retry banner, hit
  Retry — upload completed, the file appeared in the list, position preserved.
- Retried three times in a row — no duplicate rows.
- **Did not check:** files over the 10 MB limit, or a slow-but-not-dead connection.
```

- Report what happened, not what should happen. "Should work" is not an observation.
- Say what you didn't check. An honest gap is fine; a silent gap is not.
- Couldn't run it at all? Say so and say why — that's a valid outcome. An invented result never is.
- Restating the spec in past tense is not this field, and it gets bounced.

## Review

Read `## What good looks like` again before reading the Handoff, so you're checking against the
promise rather than being led by the report. Then:

1. **Walk the outcomes one by one.** Silence on an outcome is the strongest signal in this system
   that it didn't get done. Ask about it.
2. **Check that "What I ran and what I saw" reports real execution.** A handoff that claims
   completion without saying what was run is an automatic `changes-requested` — no benefit of the
   doubt. This rule is what replaces running the product yourself.
3. **Corroborate the load-bearing claims yourself.** Reading the source to confirm a factual claim —
   "nothing needed to change here", "the endpoint already existed" — or making a cheap read-only
   check of your own (a URL, a response header, the built bundle) is the strongest verification
   available to you, and it costs minutes. This is not code review: you're confirming the account is
   true, not forming opinions about how it's written.
4. **Read the assumptions and the "didn't do" list properly.** That's where the risk lives, far more
   than in the code. An assumption that contradicts `PRODUCT.md` is a real problem even when
   everything works.
5. **Check for collateral damage.** Does anything here contradict something `STATE.md` says works?

When something genuinely needs human eyes, ask the owner for a short closed list of specific things,
never "please test this":

> Two things I can't judge from here: does the retry banner read as reassuring or alarming, and is
> the 3-second delay before it appears noticeable? Everything else checks out.

Close the review with these two lines:

```markdown
Verified by: developer's browser run, corroborated against `PhotoCarousel.tsx`
Verdict: done
```

`Verified by:` names who established it and how — the developer's account, your own reading of the
code, your own live check, the owner looking at it, or any combination of those. It is never blank,
and **"nobody established this"** is a legitimate value that gets written plainly rather than dressed
up. Whatever you put here is what goes into `STATE.md`, so it has to survive being read literally.

`Verdict:` is `done` or `changes-requested`, and it matches the status you set.

Every change request names something a user would notice. If you can't name it, it's a preference —
drop it.

On acceptance: `status: done`, move the file to `delivery/done/`, update `STATE.md` in the same turn.

## STATE.md

The architect's picture of reality, rewritten every turn. Its whole job is to answer "what isn't
ready yet" without anyone re-reading the codebase. Five sections: **Now**, **Next up**, **Works**,
**Unverified or broken**, **Accepted rough edges**.

Two rules keep it worth having:

- **It has to be true.** Something moves to *Works* only when something established that it works,
  and the entry says what. If nobody checked, it belongs under *Unverified or broken* — a long
  unverified section is honest, not embarrassing.
- **It's a state, not a diary.** *Now* is what's in flight, usually one or two things. It is not a
  record of what happened this round: an accepted task leaves *Now* entirely and becomes one line
  under *Works*. Everything else about finished work lives in its file in `done/`.

One line per entry, everywhere in the file. When an entry needs a paragraph, the paragraph belongs in
the task file.

## SYSTEM.md

The developer's description of what exists, so a cold session doesn't have to re-derive the system
from the code. Updated in the same turn as any handoff that changed the shape of things.

- **It describes the present, not the history.** No "previously X, now Y", no task numbers tagged
  onto lines. That's a changelog, and the next session will read it as the system.
- **It points at the project's `CLAUDE.md` or conventions doc, never restates it.** Two copies of the
  conventions means one of them is wrong and nobody knows which.

## Keeping documents short

`PRODUCT.md`, `STATE.md`, and `SYSTEM.md` grow every turn unless someone actively cuts them, and all
three are read at the start of every session. So before adding anything to one of them: reread it,
delete what stopped being true, then add. A stale document is worse than no document, because
someone will believe it.

Task files are the opposite — each records one piece of work and is written once, so length follows
the work. A spec longer than the implementation means too much was written; a handoff that's long
because a lot actually happened is fine.

## Templates

Starting points in `C:\Users\User\.claude\delivery\templates\` — `PRODUCT.md`, `STATE.md`,
`SYSTEM.md`, `task.md`. Delete any heading you have nothing real to put under.
