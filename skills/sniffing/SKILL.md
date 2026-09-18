---
name: sniffing
description: "Names the worst code smells in code the user points at, as a short keyword list. Use when the user asks for a smell test, asks what smells in a file, a folder, a domain, a branch, a pull request or the current changes, or invokes /sniffing."
---
Read the target the user points at. If nothing targeted then assume the current changes. If no current changes then ask the user for a target.
If the target is a diff, read only the new code. Ignore the smells the old code already had.

Use `git diff` for changes that are not committed. Use `git diff <base>...<branch>` for a branch. Use `gh pr diff <number>` for a pull request.

Write a numbered list of the smells. Give at least 3 items and at most 7. Put the worst first.

Write each item as keywords only. Keep it to a few words. Add the path and the line number after the keywords.

Write nothing else. No preamble, no explanation, no fix.
