---
name: dotnet-test-mtp
description: run, scope, and diagnose targeted dotnet test workflows for c# and .net 10 repositories using native microsoft.testing.platform mode. use when the repo is configured for microsoft.testing.platform, when dotnet test needs mtp-native options like --project, --solution, or --test-modules, or when the task calls for faster native mtp execution and diagnosis. prefer the smallest possible scope, preserve the exact command, summarize only relevant failures, and keep mtp-native behavior distinct from older vstest-style assumptions. do not use for pre-.net 10 repositories or standard vstest-oriented dotnet test flows; use dotnet-test instead.
---

# Dotnet Test MTP

Run the narrowest useful native MTP `dotnet test` command.

## Detect whether this skill applies

Use this skill when the repository is clearly on the native Microsoft Testing Platform path in .NET 10.

Typical signals include runner selection for `Microsoft.Testing.Platform` and existing commands or docs that use MTP-native `dotnet test` options.

## Non-negotiable rules

- Prefer the smallest possible scope.
- Use MTP-native option patterns.
- Preserve the exact command used.
- Summarize only the failures relevant to the current task.
- Escalate to broader scope only when the narrow scope cannot answer the question.

## Scope selection order

Choose the first scope that fits:

1. `--project <PROJECT_PATH>` for a single test project
2. `--test-modules <EXPRESSION>` when targeting built test modules directly is the smallest useful scope
3. `--solution <SOLUTION_PATH>` only when project/module scope is insufficient

Remember that `--project`, `--solution`, and `--test-modules` are mutually exclusive.

## Command patterns

Use patterns like these when helpful:

- `dotnet test --project path/to/TestProject.csproj`
- `dotnet test --project path/to/TestProject.csproj --no-build`
- `dotnet test --solution path/to/App.sln`
- `dotnet test --test-modules "**/*Tests.dll" --root-directory .`
- `dotnet test --project path/to/TestProject.csproj --results-directory artifacts/test-results`
- `dotnet test --project path/to/TestProject.csproj --diagnostic-output-directory artifacts/test-diag`

Do not fall back to VSTest-era positional project/solution arguments when the repository is already using native MTP mode.

## Output contract

Produce the response in this shape:

### Test scope
State why this is the smallest useful MTP-native scope.

### Command
Provide the exact `dotnet test` command.

### Result summary
Summarize the relevant pass/fail outcome and the most important failure details only.

### Diagnostic next step
Recommend the next narrow action, such as adjusting the red test, proceeding to green, or increasing MTP diagnostics.

## Boundaries

- Do not use VSTest-only option guidance here.
- Do not widen to the whole solution by default.
- Do not mix build-only guidance into the result when `dotnet-targeted-build` would be clearer.
