---
name: design-screen
description: Produce the spec and generator prompt for one screen, inside a Design Kit that already exists — for screens that turned up after the system was fixed: settings, an edge flow, a screen a feature needs partway through coding. Use it when a specific screen is named and a DESIGN-KIT is available — "нужен экран настроек", "спека для экрана", "промпт для этого экрана", one screen, one prompt, add a screen. Do NOT use when there is no Design Kit yet (use design-kit, which builds the system and the first batch of screens together), for a marketing landing page, or for changing the visual system itself.
---

# Design Screen

One screen, inside a system that is already decided. You are not redesigning anything, and you are
not revisiting the direction — you are spending the Kit rather than extending it.

The same deal as the Kit applies: **their job is to veto, not to specify.** Produce the whole thing
in one pass, show where each choice came from, and make silence a complete answer.

## No Kit, no screen

If no DESIGN-KIT is available, stop and ask for it. Do not improvise a visual system for one screen.

This is the single most common way this work goes wrong: a screen invented with its own type scale
and spacing looks fine alone and belongs to a different product the moment it sits next to the
others. One screen from another universe is worse than no screen, because it will get built.

If there is genuinely no Kit yet, say so and point at `design-kit` — the system and the first batch
of screens come out of one pass there, so nothing is lost by starting properly.

## Work out what the screen is for before describing it

Read CORE and the Kit, then settle four things. Each takes a line, and each is derived rather than
asked about:

- **Which step of which scenario this serves.** A screen that traces to nothing in CORE is a screen
  nobody asked for. Say so rather than building it.
- **What the person arrives with.** What they already have, already know, and already did. This
  decides how much the screen has to explain, and it is the thing most often skipped.
- **The one thing it must make obvious.** If only one thing survived the layout, this is it.
- **What is deliberately not here.** The tempting adjacent content, named, so it does not creep back
  in during coding.

## Then content, then layout

Content first, in priority order — what data appears, most important first. Layout second, described
in words using **component names from the Kit's inventory**.

Never re-describe a component. "A card with a 12px radius and a soft shadow" is how a screen drifts;
"a `row` from the inventory" is how it doesn't.

If the screen genuinely needs something the inventory does not have, **say that it is a Kit change**
rather than inventing it locally. A new component has reach into every other screen, so it is not a
decision this task gets to make quietly.

## Split the output by consumer

- **The happy path goes into the generator prompt.** Concrete values from the Kit, never adjectives.
  Self-contained, so it can be pasted on its own.
- **Every other state goes into the spec as a list for the coding layer** — empty, loading, error,
  partial, no permission, offline, using whatever the Kit decided. Not dropped, just routed to
  whoever needs them.

The prompt is an adapter: it is shaped by the tool that eats it, so it lives here and never in the
Kit.

## If the screen does not work, say so

Turning a step into a screen is where holes in the product become visible. If there is no reachable
path to this screen, if it needs data nothing produces, if it implies an entity CORE never named, or
if the flow would plainly be better arranged differently — say it, and **say that it is an edit to
CORE** so it goes back into the product's LOG. Drawing around the problem is the one thing not
allowed.

## Hand it back short

The spec, the prompt, and at most two lines on calls you made that they might not want. Silence
keeps them.

## The shape of the output

````markdown
## <Screen name>

**Serves:** <which step of which CORE scenario>
**Arrives with:** <what the person already has or knows at this point>
**Must make obvious:** <the one thing>

**Content, in priority order:**
<!-- Data, not layout. Most important first. -->

**Layout:** <structure in words, using component names from the Kit>

**Not here:** <deliberately absent, so it does not get added back>

**Other states** (for the coding layer, not the generator):
<!-- empty / loading / error / partial / no permission / offline — one line each -->

**Generator prompt:**
```
<self-contained, concrete values from the Kit, happy path only>
```
````
