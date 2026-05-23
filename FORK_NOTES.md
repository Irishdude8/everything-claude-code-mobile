# Fork notes — Pacio LLC

This is a fork of [ahmed3elshaer/everything-claude-code-mobile](https://github.com/ahmed3elshaer/everything-claude-code-mobile) created 2026-05-23 to fix a plugin manifest schema mismatch that blocks `/plugin install` in current Claude Code releases.

## What was changed vs upstream

1. **`.claude-plugin/plugin.json`** — removed three top-level fields:
   - `"skills": "./skills/"`
   - `"agents": "./agents/"`
   - `"commands": "./commands/"`

   Claude Code auto-discovers `skills/`, `agents/`, `commands/` folders at the plugin root — declaring them as explicit path strings fails manifest validation with `agents: Invalid input`. Removing the fields lets the install succeed.

2. **`.claude-plugin/marketplace.json`** — pointed the plugin's `source.repo` at this fork (`Irishdude8/everything-claude-code-mobile`) so a marketplace registration on this repo serves the fixed manifest.

## Why this fork exists at all (instead of just side-loading)

We side-loaded the skills + commands + agents + rules directly into `C:\ClaudeShared\` since the plugin manager kept reading the broken upstream manifest even after we updated marketplace pointers locally. The side-load is what's actually in use.

This fork is kept as:
- A working reference for what the manifest *should* look like
- A target for future `/plugin marketplace add Irishdude8/everything-claude-code-mobile` if the install workflow improves
- Documentation of the schema mismatch encountered 2026-05-23

## Upstream contribution

A clean PR or issue against `ahmed3elshaer/everything-claude-code-mobile` would let the upstream marketplace install correctly for everyone. Not yet filed.

## Sync policy

This fork is unlikely to track upstream rebases automatically. If upstream lands the same fix, the fork can be deleted. If upstream adds new skills/commands, manually re-side-load from upstream rather than rebasing this fork.
