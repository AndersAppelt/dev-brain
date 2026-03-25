---
name: dotnet-targeted-build
description: run or recommend the smallest relevant dotnet build or restore scope for a c# or .net repository and summarize the result concisely. use when the task needs compile feedback during green or refactor, when touched files should be verified without running the whole solution, or when a targeted project, test project, or solution slice should be built before or alongside test execution. prefer the narrowest project path that covers the change, preserve the exact command used, and report only actionable compiler/build output. do not use for running tests, full ci pipelines, or broad solution validation unless the user explicitly asks.
---

# Dotnet Targeted Build

Build the smallest scope that can answer the current compile question.

## Non-negotiable rules

- Prefer the narrowest build target that covers the changed code.
- Build a single project before a whole solution unless dependencies make that impossible.
- If the change only affects tests, prefer the test project.
- If the change affects shared code used by many projects, build the smallest project that consumes it and only escalate when necessary.
- Report the exact command used or recommended.
- Summarize only actionable errors and warnings.
- Do not run tests.

## Scope selection order

Choose the first scope that answers the question:

1. touched test project
2. touched production project
3. one dependent project that validates the integration point
4. solution file only when project-level targeting is insufficient

## Command guidance

- Prefer `dotnet build <project-or-solution>`.
- Use `--no-restore` when dependencies are already restored and that will save time.
- Use `-c Release` only when the user asked for that configuration or the repo workflow clearly requires it.
- Avoid broad restore/build combinations when the compile question can be answered more narrowly.

## Output contract

Produce the response in this shape:

### Build scope
State why this is the smallest relevant target.

### Command
Provide the exact build command.

### Result summary
Summarize only the compiler/build output that matters for the current step.

### Next action
Point back to the relevant implementation or test skill.

## Boundaries

- Do not run `dotnet test` here.
- Do not widen to the whole solution unless justified.
- Do not dump long raw logs when a concise summary will do.
