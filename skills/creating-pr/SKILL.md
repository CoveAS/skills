---
name: creating-pr
description: Write the title and body of a pull request, then open it with gh or glab. Use when the user asks for a pull request or a merge request. Use also when work on a branch is done, to ask the user whether to make one.
---

# Creating a PR

The team reads the code. The text says what the code cannot.

## When to start

Start when the user asks for a pull request or a merge request.

Ask when work on a branch is done. Never assume a PR should be made.

## The title

Take the prefix that the branch name or the commits share. Keep it exactly as it is.

Write the subject after the prefix, with a capital first letter.

```
OPP-2065: Split the session store from the cache
backopp: Retry the payment webhook
```

Write no prefix when the branch and the commits share none. Start with the capital letter.

The title needs no approval. Change it only when the user asks.

## The body

The body says what the change does, and why the code base needs it. The why is the problem the
change solves in the code. It is not the story of how the work started.

Say it in as few words as the change needs. Do not list the files.

Work the why out from the code, the commits, the branch name and the ticket. Tell the user when
you could not work the why out.

## The steps

1. Read the diff against the base branch. The why must match the real code.
2. Push the branch.
3. Show the body. Wait for the user to approve it.
4. Open the PR. Use `gh pr create` for a GitHub remote. Use `glab mr create` for a GitLab remote.
5. If the session works in a worktree, ask the user if the session should leave it. A yes means `ExitWorktree` with `remove`. Set `discard_changes: true` only when the remote has every commit and no file is uncommitted. Otherwise stop and tell the user.

## Claude's signature

Claude signs only with two dashes followed by the model name and effort level, and brain emoji if 🧠 thinking is on, nothing else.
Example:
```
-- Opus 5.5 medium 🧠
```