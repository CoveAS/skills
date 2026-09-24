---
name: dumping-session
description: "Writes a short session dump that captures the essence of a session: what it did, the files read and edited, the problems found, solved and still open, the decisions, the dead ends and the next step. Use when the user asks what happened in the session, asks for a session summary, a recap or a handover, or invokes /dumping-session."
---
Capture the essence of the session. Do not write its full history.

Most sessions have only some of the parts below. Include a part only when the session has it and a reader needs it. Leave out the other parts, with no heading and no "None".

In each part, keep only the items that matter. Leave out small steps, routine reads and anything the next session does not need.

Write the dump in this order. Keep every part short.

1. The session. One sentence about what the session did. Always include this part.
2. The state. The branch, and whether any changes are not committed.
3. The files read. A numbered list in priority order, the most important first. Give the path, the line numbers and an extremely short reason.
4. The files edited. A numbered list. Give the path and an extremely short line about the change.
5. The problems found. A numbered list. One short line each.
6. The problems solved. A numbered list. One short line each. Name the fix.
7. The open problems. A numbered list of the problems that are not solved. One short line each.
8. The decisions. A numbered list. Give the choice and a short reason.
9. The dead ends. A numbered list of what the session tried that did not work, and why.
10. The commands. The commands that test or reproduce a problem. Leave out routine commands.
11. The next step. One line about what to do first.

Use only what happened in this session. Do not guess.

Put the whole dump in one markdown code block. The user copies it out.

Write nothing else. No preamble, no summary, no plan.
