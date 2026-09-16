---
name: corrector
description: Correct spelling and grammar mistakes in the user prompt before answering / Corrige les fautes d'orthographe et de grammaire du prompt utilisateur avant de répondre
license: MIT
compatibility: opencode
metadata:
  audience: maintainers
  workflow: prompt-postprocess
---

## Purpose / Objectif

EN: Improve the user's prompt for spelling and grammar while preserving meaning, then answer the request.
FR: Améliorer l'orthographe et la grammaire du prompt utilisateur sans en changer le sens, puis répondre à la demande.

## Behavior / Comportement

1. EN: Rewrite the user's prompt with corrections only.
   FR: Réécrire le prompt utilisateur en corrigeant uniquement les fautes.

2. EN: Display the corrected prompt in a boxed block.
   FR: Afficher le prompt corrigé dans un bloc encadré.

3. EN: Answer the original request normally.
   FR: Répondre normalement à la demande d'origine.

## Output Format / Format de sortie

Use this structure exactly / Utiliser exactement cette structure :

[Corrected Prompt / Prompt corrigé]
<corrected prompt>

[Answer / Réponse]
<final answer>

## Rules / Règles

- EN: Preserve intent and meaning.
  FR: Préserver l'intention et le sens.
- EN: Keep the same language as the user prompt.
  FR: Conserver la même langue que le prompt utilisateur.
- EN: Do not alter code snippets, commands, file paths, URLs, IDs, or proper nouns unless there is an obvious typo.
  FR: Ne pas modifier les extraits de code, commandes, chemins de fichiers, URL, identifiants ou noms propres, sauf faute évidente.
- EN: Do not invent missing information.
  FR: Ne pas inventer d'informations manquantes.
- EN: If no correction is needed, repeat the prompt unchanged in the corrected block.
  FR: Si aucune correction n'est nécessaire, répéter le prompt tel quel dans le bloc corrigé.

## When to Use / Quand l'utiliser

EN: Use this skill when spelling or grammar mistakes reduce clarity.
FR: Utiliser ce skill quand des fautes d'orthographe ou de grammaire nuisent à la clarté.

## When Not to Use / Quand ne pas l'utiliser

- EN: The prompt is already clear and correct.
  FR: Le prompt est déjà clair et correct.
- EN: The user asks for verbatim quoting.
  FR: L'utilisateur demande une citation verbatim.
- EN: The prompt is mostly code/commands and correction may break intent.
  FR: Le prompt contient surtout du code/des commandes et la correction pourrait casser l'intention.
