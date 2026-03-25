---
name: csharp-tdd-loop
description: orchestrate test-driven development for c# and .net one red-green-refactor slice at a time. use when the user wants to implement from a requirement, specification, acceptance criterion, or bug report with tdd; asks for the next tdd step; asks to continue after reviewing a red test or green implementation; or wants constraints like one failing test, minimal implementation, review stops, and optional refactor inferred automatically. always route test execution through dotnet-test or dotnet-test-mtp and build checks through dotnet-targeted-build. do not use for broad multi-feature coding, large design work, or bundling multiple loops into one turn.
---

# Csharp TDD Loop

Drive the conversation as a strict single-slice TDD loop. Infer the constraints automatically so the user does not need to restate them.

## Core rules

- Do exactly one red-green-refactor slice at a time.
- Never produce more than one new failing test in a single loop.
- Never produce production code during the red step.
- Never continue from red to green until the user has reviewed and approved the red step.
- Never refactor unless the user explicitly asks, or explicitly approves a refactor after green.
- Always prefer the smallest observable behavior that advances the requirement.
- Always delegate test execution to `dotnet-test` or `dotnet-test-mtp`.
- Always delegate compile-only feedback to `dotnet-targeted-build`.
- Stop after each red or green step and wait for the user.

## Decide the current phase

1. **Start or continue from a requirement/spec/bug**
   - Enter **red**.
   - Ask no extra planning questions unless the requirement is too vague to identify any observable behavior.
   - Select the smallest next behavior slice and hand off to `csharp-red-test-author`.

2. **User approved the red step or asks for the implementation**
   - Enter **green**.
   - Hand off to `csharp-minimum-implementation`.

3. **User asks to refactor, clean up, rename, or improve readability after green**
   - Enter **refactor**.
   - Hand off to `csharp-test-refactor`.

4. **User asks for multiple behaviors at once**
   - Narrow to the single smallest next slice.
   - State that the skill is intentionally doing one loop only.

## Red step contract

When entering red:

- Translate the requirement or bug report into one observable behavior.
- Produce exactly one failing test and only the minimum helper code needed for readability.
- Explain briefly why this test should fail today.
- Invoke `dotnet-test` or `dotnet-test-mtp` for the narrowest possible test run.
- End the turn with a clear review stop.

Use this response shape:

### Selected slice
One sentence naming the single behavior under test.

### Red test
Provide only the new or changed test code and any tiny test helper needed for readability.

### Run
State the targeted test command or targeted test scope to execute through the appropriate dotnet test skill.

### Why it should fail
One or two sentences tied to the missing behavior or bug.

### Review stop
Ask the user to approve or request changes. Do not proceed to implementation.

## Green step contract

When entering green:

- Assume the red test has already been reviewed.
- Write the minimum production change required to make that exact test pass.
- Do not fold in opportunistic refactors, cleanup, or extra behavior.
- Use `dotnet-targeted-build` when compile feedback is needed.
- Use `dotnet-test` or `dotnet-test-mtp` to rerun the narrowest possible scope.
- End the turn with a clear review stop.

Use this response shape:

### Goal
Restate the single approved failing behavior.

### Minimum implementation
Provide only the smallest production code change required.

### Verify
State the targeted build scope if needed, then the targeted test scope to run.

### Review stop
Ask the user to approve or request changes. Do not refactor yet.

## Refactor step contract

When entering refactor:

- Preserve behavior.
- Prefer small readability improvements: helper extraction, naming cleanup, fixture simplification, duplication removal, and local structure cleanup.
- Avoid large design changes unless the user explicitly asks for them.
- Rerun the narrowest build/test verification through the dedicated build/test skills.
- Stop for review again.

Use this response shape:

### Refactor goal
One sentence.

### Refactor
Provide the focused refactor only.

### Verify
State the narrowest build/test verification scope.

### Review stop
Ask whether to continue with the next behavior slice.

## Requirement slicing rules

When starting from a requirement or specification:

- Prefer one externally visible behavior over one internal implementation detail.
- Prefer the smallest step that could fail for a meaningful reason.
- If the requirement is large, pick the first slice that creates a stable foothold for later loops.
- If the API contract itself is missing, a compile-time failing test is acceptable only when the missing type/member is the exact behavior promised by the requirement.

## Boundaries

- Do not write a backlog, full implementation plan, or multiple test list unless the user asks.
- Do not run broad solution tests by default.
- Do not change production code during red.
- Do not refactor during green.
- Do not silently skip test execution: route it through the appropriate dotnet test skill.
