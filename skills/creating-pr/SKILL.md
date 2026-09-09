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

The body says why the change exists, and what problem it solves. Nothing else.

Say it in as few words as the why needs. Do not describe the diff. Do not list the files.

Work the why out from the code, the commits, the branch name and the ticket.

Write what the change does when the why stays unclear. Keep it as short. Tell the user that you
could not work the why out.

## The steps

1. Read the diff against the base branch. The why must match the real code.
2. Push the branch.
3. Show the body. Wait for the user to approve it.
4. Open the PR. Use `gh pr create` for a GitHub remote. Use `glab mr create` for a GitLab remote.
