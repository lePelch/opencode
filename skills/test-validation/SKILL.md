---
name: test-validation
description: Plan tests explicitly in Plan mode and request user approval before writing unplanned tests in Build mode. Use for development, bug fixes, refactoring, and test changes.
compatibility: opencode
---

# Test Validation

## Scope

These instructions are also loaded as global instructions, so Plan and Build
receive them without needing to invoke the skill. Apply them to development
tasks and test changes, regardless of the selected model. Do not add testing
ceremony to unrelated tasks such as ordinary conversation or note writing.
Follow the active agent's restrictions; these instructions never authorize
editing in Plan mode or switching agents automatically.

## Plan Mode

- Inspect the existing test conventions before proposing tests.
- Include a clearly identified "Tests prévus" section (or the equivalent in
  the user's language) in the plan presented in the conversation.
- For each proposed test or small group of related tests, state:
  - Whether it will be created or an existing test will be modified.
  - Its type: unit, integration, end-to-end, or another relevant type.
  - The scenario, inputs or conditions, and expected observable result.
  - The target file or suite when known; mark uncertain locations as tentative.
- Mention meaningful error cases and boundaries when relevant, without adding
  speculative tests or imposing arbitrary coverage targets.
- Identify any new test dependency, framework, fixture, or infrastructure.
- If no test changes are warranted, say so briefly and explain why. Distinguish
  running existing checks from creating or modifying tests.
- Resolve unclear behavioral expectations with the user rather than guessing.
- Present the test choices as part of the plan for user approval. Do not create
  tests, edit project files, or write a plan file merely to satisfy this skill.

## Build Mode

- Use the most recent user-approved plan and any subsequent explicit approvals
  as the agreed test scope. Approval of the plan covers its listed tests; do
  not ask again for each planned test.
- A switch to Build alone does not approve an unapproved test proposal. An
  explicit request to implement the presented plan does approve its tests.
- Implement the approved test scenarios using the project's conventions.
- Before writing an unplanned test, explain its scenario, expected result,
  benefit, and any relevant tradeoff, then ask for approval using the question
  tool when available. Offer concise choices such as add, adjust, or skip.
- This approval requirement also covers new scenarios or behavioral assertions
  added to existing tests, material changes to an approved expected result,
  and unplanned test dependencies or infrastructure. Do not bypass it by
  changing an existing test instead of creating a new file.
- Minor implementation details within an approved scenario, such as naming,
  file placement, or equivalent fixtures, do not require another approval.
- Wait for an explicit answer before implementing the unapproved portion.
  Silence is not approval. Continue independent, already approved work when
  possible; if the choice blocks progress, explain what is blocked.
- If no approved test plan exists, propose the intended tests and obtain
  approval before writing them. A direct user request specifying a test's
  scenario and expected behavior already authorizes that test.
- Running existing tests, linters, and checks does not require approval under
  this skill; continue to respect tool permissions and other safety rules.
- Never weaken, delete, or skip an existing test merely to make the suite pass.
  Ask before materially changing its intended behavior if not already approved.

## Reporting And Handoff

- Keep questions concrete, brief, and in the user's language. Group related
  proposals when practical, but allow the user to approve them selectively.
- Preserve the approved scenarios, pending proposals, and user decisions in
  handoffs or summaries so that a model or agent change does not lose scope.
- Other agents doing test-writing work must respect the same approval boundary;
  read-only agents do not need to request approval just to suggest tests.
- In the final summary, distinguish tests created or modified, checks actually
  run and their results, and any tests declined, deferred, or awaiting approval.
  Never claim a check ran or passed without evidence.
