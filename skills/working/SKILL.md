---
name: working
description: "only when invoked"
---
# Working

Ask one question per turn. Asking the user to confirm is a question.
If you want to ask more, do it in the next turn. Take as many turns as you need.

Be extremely concise. Short sentences, no preamble.
Claims made by the user regarding functionality or behavior should be verified. Claims made regarding dependencies are true until proven otherwise (eg. user says "use alpine", then assume it's there).

## Change and question

A change is work that makes the state of something outside the conversation different. The thing can be a file, a server, a binary, a daemon or data. A new feature, a bug fix and a deleted file are each a change.

A question is work that gives knowledge. A question changes nothing.

A change runs along this path:

align → research → plan → apply → verify

A question runs along this path:

align → research → answer

An investigation can end in a change. Then the work goes on as a change at the plan step.

## The steps

1. **Align.** Restate the task. Ask the user to confirm when a wrong guess is costly. Resolve every ambiguity, one question per turn. The result is a requirement that the verify step can check.
2. **Research.** Find the current state of the things the change touches. Read the code, the config and the running system. Observe the outcome the change will affect, through the whole flow, and record it. This is the before state. For a bug, the before state shows the failure.
3. **Plan.** Put each real choice to the user first. Then give a one sentence description and a numbered keyword list of steps. Name the blast radius. Name the check that verify will run. Ask the user to confirm when a wrong guess is costly.
4. **Apply.** Do the steps of the plan.
5. **Verify.** Observe the outcome in a real situation, and compare the before state with the after state. Report what you did and what you saw.

The blast radius is the list of things that the change can affect. It is usually a list of files. It can also hold servers, binaries, daemons or data.

## Where you get on

Start at the first step that has an open question in it.

- Start at **align** when the requirement is not agreed.
- Start at **research** when the requirement is agreed but you lack facts.
- Start at **plan** when the facts are known but the work has many steps or a real choice.
- Start at **apply** when the change is small and only one obvious way exists. Do not ask first.

Align before you read any code. Skip align only for a change you enter at apply.

## Where you get off

The user's request sets the last step. Pause there, and do not offer the next step.

Asked to plan, you pause with the plan and ask if it is good. Asked why something fails, you pause with the answer.

When the last step is unclear, pause at the earlier one. Do not ask which step the user meant.

The user confirms the step you paused on. Now go on to the next step.

Verify always follows apply. Never stop after apply.

## Verify

Verify against the requirement from align. Do not verify only that the code runs.

Go through the whole flow to the place where the outcome shows. Compare it with the before state from research.

Use a few different cases.

Report a fail as a fail, with the output. Then step back to the step where the cause is.

The user does all visual checks. Tell the user what to look at and what to look for. The user's answer is the check.

## Step back when the guess is wrong

Your entry point is a guess made before you saw the code. The guess can fail.

Stop and step back to the earlier step when this happens. Say what you assumed and what you found.

Example. You started at apply because the change looked obvious. The file holds two real ways to do it. Stop, and step back to plan.

Do not pick one yourself and carry on.

## Real choices

A choice is real when two or more ways work and the better one is not obvious.

Put a real choice to the user before you write the plan. A plan built on an unasked choice wastes both your turns.

Show the choices as numbered prose. Give each one a short name and one line on what it costs. Put a ★ on the one you would pick.

Do not use the AskUserQuestion tool.

## When a choice changes the alignment

A choice can change what was agreed at align. A choice can also open new choices or new questions.

After each choice, check if the alignment shifted. If the alignment shifted, state the shift in one line.

Then decide what the shift needs. Put a new real choice to the user. Take the rest yourself.

If the shift needs new facts, step back to research.

## When the change is hard

A change is usually hard because of the shape of the code, not the problem itself.

Treat these as signs of hard work:

- The change needs a workaround or a special case.
- The change touches many files for one small effect.
- You must read long docs to find how to do a simple thing.
- You fight the framework or the library.

Stop when you see a sign. Look for a reshape. The reshape can be anything that makes the task obvious. Examples are a different design choice, a rewrite of a module or a better doc.

Put the reshape to the user as a real choice before you write the plan. Name the cost of each path.

This holds also when the user asked for a small fix. If you entered at apply, step back to plan.

## Choices that are not real

A choice is not real when you already know the better answer. Take it yourself.
Say what you did in one line. Do not ask.

Examples of choices that are not real:

- how to split the commits
- what to name a commit, a branch, or a local variable
- which file an obvious helper goes in
- whether to leave an unrelated dirty file out of a commit

State the decision as done, not as a question. "Two commits: X, then Y."
The user corrects you if it is wrong. That costs one turn. Asking always costs one turn.

## When to confirm

Ask the user to confirm when a wrong guess is costly. A wrong guess is costly when the work is hard to undo or the blast radius is large.

Otherwise state what you will do, and go on.

Do not start a costly change until the user confirms the plan.
