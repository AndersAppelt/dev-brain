---
name: dotnet-test
description: run, scope, and diagnose targeted dotnet test workflows for c# and .net repositories that use the traditional vstest option model. use when tests need to be run, listed, filtered, logged, or debugged in repos that are not using native microsoft.testing.platform mode in .net 10. prefer the smallest possible scope such as a single project, test class, or test method; preserve the exact command; summarize only relevant failures; and support filters, trx/loggers, coverage collection, runsettings, blame, and diagnostics when useful. do not use when the repo is clearly configured for native mtp mode on .net 10; use dotnet-test-mtp instead.
---

# Dotnet Test

Run the narrowest useful `dotnet test` command for VSTest-style repositories.

## Detect whether this skill applies

Use this skill when the repository is on the traditional `dotnet test` / VSTest path.

Switch to `dotnet-test-mtp` instead when the repo is clearly using native Microsoft Testing Platform mode in .NET 10, for example when test runner selection indicates `Microsoft.Testing.Platform`.

## Non-negotiable rules

- Prefer the smallest possible test scope.
- Run one project before a whole solution unless the question is explicitly broad.
- Prefer a method or class filter over a whole project when a single failing test is known.
- Preserve the exact command used.
- Summarize only the failures relevant to the current task.
- Escalate to broader scope only when the narrow scope cannot answer the question.

## Scope selection order

Choose the first scope that fits:

1. single test method via `--filter`
2. single test class via `--filter`
3. single test project
4. solution

## Command patterns

Use patterns like these when helpful:

- `dotnet test path/to/TestProject.csproj --filter "FullyQualifiedName~Namespace.Class.Method"`
- `dotnet test path/to/TestProject.csproj --filter "FullyQualifiedName~Namespace.Class"`
- `dotnet test path/to/TestProject.csproj --logger trx`
- `dotnet test path/to/TestProject.csproj --collect:"XPlat Code Coverage"`
- `dotnet test path/to/TestProject.csproj -s path/to/.runsettings`
- `dotnet test path/to/TestProject.csproj --blame`
- `dotnet test path/to/TestProject.csproj -d test.log`

Prefer `--no-build` when the project has already been built and the goal is only to rerun tests quickly.

## Output contract

Produce the response in this shape:

### Test scope
State why this is the smallest useful scope.

### Command
Provide the exact `dotnet test` command.

### Result summary
Summarize the relevant pass/fail outcome and the most important failure details only.

### Diagnostic next step
Recommend the next narrow action, such as adjusting the red test, proceeding to green, or using blame/diag/logging.

## Boundaries

- Do not use MTP-native option patterns here.
- Do not widen to the whole solution by default.
- Do not mix build-only guidance into the result when `dotnet-targeted-build` would be clearer.
