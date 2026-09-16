---
name: obsidian-note
description: Use when writing, planning, rewriting, structuring, or summarizing notes inside an Obsidian vault, especially when the user mentions Obsidian, vault, notes, project-scoped PDFs, backlinks, tags, Plan Mode, or Build Mode.
license: MIT
compatibility: opencode
metadata:
  audience: note-takers
  workflow: obsidian-note-writing
---

# Obsidian Note

## Purpose

Help plan, write, and structure concise notes for an Obsidian vault.

## Trigger

Use this skill when:

1. The user asks to create, improve, summarize, organize, or rewrite notes.
2. The workspace is an Obsidian vault, or the user explicitly mentions Obsidian, vault, notes, backlinks, tags, or PDFs.
3. The task benefits from Obsidian-style Markdown, links, tags, or note structure.

## Plan Mode Behavior

When Plan Mode is active:

- Do not create or edit notes.
- Explain normally what notes should be written.
- Describe the intended note structure, key ideas, links, tags, and source material.
- Mention any missing context needed before writing.
- Produce an implementation-ready plan only.

## Build Mode Behavior

When Build Mode is active:

- Produce the necessary notes.
- Use the planned structure unless new file context requires an adjustment.
- Read relevant local context first, especially PDFs and existing notes when available.
- Keep the writing concise and directly useful.

## Obsidian Title Rule

The filename is already the first visible title when opening a note in Obsidian.

- Do not add a first-level heading identical to the filename.
- Avoid notes like `MTTQ.md` whose first section is `# MTTQ`.
- If a visible heading is useful, make it more specific than the filename.
- Prefer starting directly with the summary or the first meaningful section.

## Obsidian Conventions

- Use internal links with `[[Note Name]]`.
- Use tags sparingly and consistently.
- Avoid over-linking common words.
- Use Markdown headings with a clear hierarchy.
- Preserve existing naming conventions when visible in the vault.
- Do not invent backlinks, tags, citations, page numbers, or source details.

## PDF And Source Handling

- Inspect relevant PDFs or source files in the vault before drafting when available.
- If source material is missing or ambiguous, state what context is missing.
- Summarize source material faithfully.

## Project Scope For PDFs

PDFs related to the current notes are usually stored inside the active project workspace.

- Treat the current project folder as the PDF boundary.
- For example, when working on `app5`, prefer PDFs inside `app5`, especially a folder such as `fichier pdf`.
- Do not read PDFs from sibling projects such as `app3` or `app4` while working on `app5`, unless the user explicitly asks for it.
- Markdown notes from other projects may be read when useful.
- If a concept is already explained in another project's `.md` notes, reference it instead of duplicating the explanation.
- If the active project is unclear and PDF loading is needed, stop the note-writing flow and ask the user which project is active before reading PDFs or producing notes.

## Output Style

- Be concise and go directly to the point.
- Start with the most useful information.
- Use short sections and bullet points when helpful.
- Highlight open questions or follow-ups when useful.
- Keep the note clean enough to be saved directly in Obsidian.

## When Not To Use

Do not use this skill when:

- The current folder is not an Obsidian vault and the user did not mention Obsidian or notes.
- The task is general coding, debugging, configuration, or shell work.
- The user asks for raw extraction only, without note-writing or organization.
