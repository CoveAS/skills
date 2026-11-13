---
name: working-with-agents
description: "Use only when invoked. Runs the working skill, but sends each question for the user to a decider sub-agent first. The decider takes the choices it can, and gives the user each remaining question with the code and facts needed to answer it in one pass."
---
# Working with agents

Follow the `working` skill. Change one thing: each time `working` tells you to ask the user, ask a decider sub-agent first.

This covers every question, every real choice and every confirm.

## Keep a record

Keep a list of each answer the user gave in this session. Write one line for each: the choice, the pick, the reason.

## Brief the decider

Start a new sub-agent with the Agent tool for each question. The sub-agent knows nothing about the session. Put everything it needs in the brief:

1. the decider rules below, word for word,
2. the requirement from align,
3. the question and the options,
4. the code each option touches, with enough lines around it to show its shape,
5. the facts from research, quoted,
6. the record of the user's answers.

Show the content. Do not refer to it. The decider cannot see what you saw.

## Act on the answer

- **DECIDED.** Take the choice. Tell the user in one line what you took and why. Go on.
- **NEED CONTEXT.** Find the missing facts, and brief a new decider. If you cannot find the facts, the user gets the question.
- **REJECTED.** Split or sharpen the question, and brief a new decider.
- **ASK USER.** Give the user the question that the decider wrote. Wait for the answer, and add it to the record.

## The decider rules

You are the decider. An agent brings you a choice. You may read files to check a fact. Do not change anything.

Start your answer with one label: `REJECTED`, `NEED CONTEXT`, `DECIDED` or `ASK USER`.

**REJECTED.** The brief holds more than one question, or a vague question. Say how to split or sharpen it.

**NEED CONTEXT.** The brief lacks a fact you need. Name the fact. Do not guess. The agent is deep in the code. Your job is to keep the bigger picture.

**DECIDED.** One option follows from the code, the conventions, the facts or a clear standard. Look past the options given. Ask how the design would look if it was written from scratch today, and pick the most correct choice. Name the choice and give the reason in one sentence.

Decide a choice of taste too, but only when the record of the user's answers shows a clear pattern for it. Name the earlier answer you follow.

**ASK USER.** Use this when:

- the choice needs taste and the record shows no clear pattern,
- the choice is hard to undo or reaches other people, such as a delete, a push or a message,
- you are not sure the choice is obvious.

Then write the question for the user in the shape below.

## The question shape

The user must answer from this message alone, with a number.

1. Put the question first, in one line.
2. List the options with numbers. Each option shows the result the user will see. Mark your pick with ★ on the left, and indent the others with `&nbsp;` so the numbers stay in a column.
3. Under the list, write **I recommend #n** and the reason in one clause.
4. Show the code the choice is about, with enough lines around it to show its shape. Give the file and the line.
5. End with the facts you rely on, quoted. The user reads them only to doubt the ★.

Example:

> **Should a removed user keep their open tasks?**
>
> ★ 1. **Unassign.** The tasks show "No owner" in the list.
> &nbsp;&nbsp;&nbsp;2. **Keep.** The tasks still show "Kari (removed)".
>
> **I recommend #1.** Open work needs a live owner.
>
> `src/Users.php:40`
> ```php
> public function remove(User $user): void
> {
>     $user->deleted_at = now();
>     $user->save();
>     // nothing clears tasks.owner_id here
> }
> ```
>
> What I saw: 14 open tasks have a removed owner now.
