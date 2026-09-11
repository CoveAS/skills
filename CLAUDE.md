# cove skills

This repo is a Claude Code plugin. Each folder under `skills/` holds one skill, as a single `SKILL.md`.

## Naming

Name a skill for the act it performs, in the gerund form: `planning`, `specifying`, `worktreeing`.

Use the same name in three places. Use the folder name, the `name:` field in the frontmatter and the row in the README table.

Use lower case and hyphens. Do not use spaces or capitals.

Name the act, not the role. Write `storytelling-as-a-business-owner`. Do not write `confused-business-owner`.

Keep the name to one act. Split the skill when the name needs an "and".

## The file

Every skill is one `SKILL.md` with frontmatter and a body.

The frontmatter holds `name` and `description`. Nothing else.

The description says what the skill does, then when to use it. Claude reads the description to decide whether to load the skill, so name the triggers.

Write the body as instructions to Claude. Keep it short.

## The README

The README holds a table of every skill. Add a row when you add a skill. Remove the row when you remove a skill.

Keep the rows in alphabetical order.

## How to update the plugin

The plugin is installed from this repo. A push is not enough, the local copy must be pulled.

1. Commit the change.
2. Push to `main`.
3. Run `claude plugin update skills@cove`.
4. Restart Claude Code.

The plugin declares no version, so each commit counts as a new one. `claude plugin validate` warns about the missing version. That warning is expected.
