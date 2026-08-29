---
name: specifying
description: Reach a written agreement with the user before any code is written. Fills in a fixed list of items — the why, the story, scope, exclusions, one testable acceptance criterion, assumptions and risks — inferring what it can and asking one question at a time for the rest. Use when a request is not yet fully specified, when the user says "I want X", hands over a user story, ticket or bug report, or invokes /specifying by name.
---

# Specifying

Fill in the ten items below, write them out as the agreement, and stop there. Implementation is a
separate conversation, held after they accept.

## Restate first

Before you look at any code, write item 1 and item 2 in the chat. Only those two.

Then ask one question: is this the right direction? Wait for the answer.

A wrong direction makes every later step waste. The code cannot tell you the direction, only the user
can. If they correct you, restate again and ask again.

Start on the other items after they accept the direction. Item 1 appears twice: here, and again in the
finished agreement.

## The items

1. **The task, restated** — in their terms, one paragraph.
2. **The why** — the problem behind the request.
3. **The story** — a user story, or a one-line behavior statement where a story doesn't fit (bugs,
   refactors, spikes). More than one if more than one is pertinent.
4. **Current behavior** — what the system does today, seen with your own eyes.
5. **Where it lives** — the code this touches, what already overlaps, what it conflicts with, who owns it.
6. **Scope** — what will be built.
7. **Out of scope** — what this will explicitly *not* do: the edges, roles, platforms and cases someone
   might otherwise assume are included. Anything cut but still valuable is listed here as "later".
8. **Acceptance criterion** — one testable sentence in observable terms. Add two or three concrete cases
   (input → expected result) if the sentence leaves edge behavior implicit.
9. **Assumptions** — anything you inferred and they haven't confirmed.
10. **Risks** — data changes or migration, permissions, performance, rollback, who else is affected.
    Say "none" once you have checked each.

## The story form

As a *[role]*, I want *[need]*, so that *[benefit]*. The benefit is not the need said again.
Name the need, never the screen, the button or the field.
Split the story when an "or" or an "and" joins two causes or two benefits.

## How to fill them

For each item, in this order of preference:

- **Have it.** They gave it to you. Check it rather than rebuild it — a supplied user story still hides a
  why, and still has unstated exclusions.
- **Infer it.** From the request, the codebase, the running system, existing tickets or docs. Items 4 and
  5 are always found by looking. Prefer looking wherever looking can answer. Look only after the user
  accepts the direction.
- **Ask.** For what looking cannot resolve: intent, priorities, business rules, who it's for, what "done"
  means to them.

Never invent an item to avoid asking. Anything you inferred rather than confirmed belongs in item 9.

Work in whatever order the request allows. Fill what you can from what you were given, look at the system
to fill more, ask for the remainder. When something you learn invalidates an item you already filled,
refill it and say so.

## How to ask

- **One question per turn.** Never two. Take as many turns as it needs.
- Write questions so they are easy to understand and easy to answer.
- **Prefer a correction to a composition.** State your assumption and ask them to correct it. "I'm
  assuming this is logged-in users only — right?" beats "who is this for?"
- Offer concrete options when the answer is a choice.
- Never batch questions into a list to save time. It doesn't.

## Before writing the agreement

Say it out loud, and stop for an answer, if:

- **It doesn't need building.** An existing feature, a setting or a config change already solves the why.
  Propose that and offer to close the request.
- **It's already mostly built.** Reframe from "build" to "expose" or "finish".
- **It conflicts** — with the architecture, an existing behavior, another commitment, or the timeline.
  Name the tradeoff and attach the smallest viable alternative.

You are the only one who has seen the code. Silence here reads as agreement.

## The agreement

Write all ten items in the chat as one block they can copy, where they can react to it line by line.

Then ask the question that is usually missing: **how will you know this worked?** Their answer is often a
better specification than the original request was.

Wait for words that say yes.

## Re-entry

If they invoke this again, or change the request substantially mid-flight, start over with the new
request. Carry forward what is still true; refill anything the change touched.

## When to skip this entirely

The request is small, well understood, and you already know where the code lives. This is proportional to
uncertainty, not to politeness.
