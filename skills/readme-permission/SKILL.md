---
name: readme-permission
description: Ask for explicit user permission before creating or modifying any README.md file, regardless of the tool used.
compatibility: opencode
---

# README Permission

## Scope

These instructions are also loaded as global instructions. Apply them in every
project without requiring the skill to be invoked. Follow the active agent's
restrictions; permission never authorizes writing in Plan mode.

## Before Writing

- Before creating or modifying any file named `README.md`, explain the target
  path and the intended changes, then ask the user for explicit permission.
- Use the question tool when available and wait for an explicit answer.
  Silence, a general implementation request, or switching to Build is not
  permission to write to a README.
- Approval applies only to the described files and changes. Ask again before
  expanding that scope.
- Apply this rule regardless of the tool or mechanism: patches, write or edit
  tools, shell commands, scripts, generators, formatters, and delegated work.
  Do not bypass it by deleting, replacing, or renaming the README.
- If permission is refused or still pending, leave the README untouched.
  Continue independent authorized work when possible.
- Reading a README or proposing changes in the conversation does not require
  permission under this rule.
