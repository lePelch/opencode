---
name: plan-mode-guard
description: Prevent false implementation starts while Plan Mode is active / Empêche les faux démarrages d'implémentation quand le mode Plan est actif
license: MIT
compatibility: opencode
metadata:
  audience: maintainers
  workflow: execution-gate
---

## Purpose / Objectif

EN: Enforce a strict separation between planning and implementation so the assistant never claims to start coding while in read-only Plan Mode.
FR: Forcer une separation stricte entre planification et implementation pour que l'assistant ne pretend jamais commencer le code en mode Plan (lecture seule).

## Trigger / Declenchement

Activate this skill when both conditions are true:

1. The conversation indicates planning mode (keywords like `plan`, `build the plan`, `commence l'implementation` after a plan).
2. A read-only guardrail is present (for example `Plan Mode - System Reminder`, `READ-ONLY`, `STRICTLY FORBIDDEN`, `you MUST NOT make any edits`).

## Priority / Priorite (MANDATORY)

If a system message indicates Plan Mode / READ-ONLY, these rules are absolute and override all other instructions, including user requests to implement immediately.

## Core Rule / Regle principale

EN: In Plan Mode, never say or imply that implementation has started.
FR: En mode Plan, ne jamais dire ni laisser entendre que l'implementation a commence.

## Hard Gate / Blocage strict

When Plan Mode is active:

- DO NOT claim or imply implementation starts now.
- DO NOT announce file operations (`je vais modifier`, `je restructure`, etc.).
- DO NOT run write-capable actions or suggest they are being executed.
- Respond with a BLOCKED status and an execution-ready plan only.

## Deterministic Response Contract

If user asks to implement while Plan Mode is active, output MUST contain:

1. `Mode actuel: Plan (lecture seule)`
2. One line explaining that edits are blocked.
3. Numbered implementation steps ready to run later.
4. Validation commands.
5. Exact unblock command:
   `Quitter le mode Plan puis demander: "Execute maintenant".`

No implementation-start phrasing is allowed outside this contract.

## Forbidden Phrases (strict)

- "Je lance l'implementation maintenant"
- "Je cree et j'applique le patch"
- "Je vais modifier les fichiers"
- "Ensuite je valide avec un build"

## Required Behavior / Comportement obligatoire

1. **Acknowledge constraint clearly**
   - EN: State in one sentence that Plan Mode is read-only and prevents edits.
   - FR: Dire en une phrase que le mode Plan est en lecture seule et bloque toute modification.

2. **Continue with useful non-edit work**
   - Inspect files, gather context, and produce an execution-ready plan.
   - Include concrete file paths, ordered steps, and validation commands.

3. **Use explicit handoff language**
   - EN: "Implementation-ready plan prepared. I will execute once Plan Mode is disabled."
   - FR: "Plan pret pour implementation. J'executerai des la sortie du mode Plan."

4. **If user asks to implement immediately while still read-only**
   - Do not refuse vaguely.
   - Provide: (a) what is blocked, (b) what is already prepared, (c) exact next action to unblock.

## Output Template / Modele de sortie

Use this structure when blocked by Plan Mode:

```text
Mode actuel: Plan (lecture seule)
Je ne peux pas modifier les fichiers tant que ce mode est actif.

Plan d'implementation pret:
1) ...
2) ...
3) ...

Validation prevue:
- ...
- ...

Action requise pour executer:
- Quitter le mode Plan puis demander: "Execute maintenant".
```

## Decision Policy / Politique de decision

- Prefer action over questions when possible.
- Ask at most one targeted question only if a real functional ambiguity remains.
- Never ask for permission to continue planning work.

## Pre-send Self-check (required)

Before sending a response in Plan Mode, verify:

- No sentence claims or implies execution has started.
- No tool or action writes files or changes system state.
- The response includes all mandatory contract items.
- The user can copy the next trigger command directly.

## When Not to Use / Quand ne pas l'utiliser

- When no read-only constraint is active.
- When the user explicitly asks for planning only and not implementation.
