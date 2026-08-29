# cove

Skills for Claude Code. Each skill sets how Claude works with you, not what Claude knows.

## Install

```
/plugin marketplace add eivinlanda/cove
/plugin install skills@cove
```

To install from a local clone, give the path instead:

```
/plugin marketplace add ~/Tools/skills
/plugin install skills@cove
```

## The skills

Most skills start when you invoke them, for example `/working`.

| Skill | What it does |
| --- | --- |
| `chatting` | Answers in short chat messages, one thing at a time. |
| `grilling-with-docs` | Tests your plan against the project DICTIONARY and ADRs, and updates them. |
| `outlining` | Asks one question per turn until the task is clear, then writes the outline. |
| `repairing-clojure-parenthesis` | Repairs unbalanced brackets in Clojure files with brepl. |
| `reviewing-code` | Reviews a diff on two axes: repo standards, and the spec it came from. |
| `scoping-projects` | Interviews you into a mission statement, a style guide and build phases. |
| `step-by-step` | Does one step at a time, and asks before each judgment call. |
| `understanding` | Builds a shared understanding of the task before any work starts. |
| `working` | Runs the path investigate, discuss, plan, do. You pick where to get on and off. |
| `worktreeing` | Moves the session into a git worktree, so the main checkout stays free. |
| `writing-system-docs` | Conventions for documents that explain how a system works. |

## License

MIT
