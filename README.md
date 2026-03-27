# dev-brain

This repository contains local Codex skills under `.agents/skills` for two primary domains:

- requirements discovery and specification
- C#/.NET test-driven development and verification

## Skills In Scope

Only the following local skills are considered part of this repo workflow catalog:

- `requirements-discovery-loop`
- `codebase-requirements-reviewer`
- `requirements-gap-checker`
- `feature-spec-writer`
- `csharp-tdd-loop`
- `csharp-red-test-author`
- `csharp-minimum-implementation`
- `csharp-test-refactor`
- `dotnet-test`
- `dotnet-test-mtp`
- `dotnet-targeted-build`

## Supported Workflows

### 1) End-to-End Requirements Workflow

Use this when starting from a rough idea or partial requirement and you need implementation-ready outputs.

1. Start with `requirements-discovery-loop` to structure the conversation and identify missing decisions.
2. Use `codebase-requirements-reviewer` to inspect current behavior and constraints in the existing codebase.
3. Run `requirements-gap-checker` to surface blocking gaps, ambiguities, and missing acceptance criteria.
4. Finish with `feature-spec-writer` to produce an agent-oriented feature specification and a backlog-ready Jira requirements draft.

Typical outcome: exhaustive, testable requirements with explicit open questions.

### 2) Codebase-Informed Requirement Review Workflow

Use this when a draft requirement already exists and you want to validate completeness before implementation.

1. Run `codebase-requirements-reviewer` to extract facts and constraints from the code.
2. Run `requirements-gap-checker` to classify must-resolve vs should-resolve gaps.
3. Optionally run `feature-spec-writer` once unresolved decisions are clarified.

Typical outcome: a validated requirement with concrete clarifying questions and measurable acceptance criteria.

### 3) Single-Slice C#/.NET TDD Workflow (Red -> Green -> Refactor)

Use this when implementing a feature or bug fix through strict, incremental TDD.

1. Orchestrate with `csharp-tdd-loop` (one behavior slice at a time).
2. Red step: `csharp-red-test-author` writes exactly one meaningful failing test.
3. Run targeted tests with `dotnet-test` for VSTest-style repositories or `dotnet-test-mtp` for native Microsoft Testing Platform (.NET 10) repositories.
4. Green step: `csharp-minimum-implementation` applies the smallest production change to pass the approved red test.
5. Use `dotnet-targeted-build` for narrow compile feedback where needed.
6. Rerun the narrowest relevant test scope via `dotnet-test` or `dotnet-test-mtp`.
7. Optional refactor step: `csharp-test-refactor` performs focused readability/maintainability cleanup after green.

Typical outcome: behavior implemented safely with clear review stops between phases.

### 4) Targeted Verification Workflow

Use this when you only need fast feedback on build/test status for a narrow code change.

1. Use `dotnet-targeted-build` for compile-only validation with the smallest relevant project scope.
2. Use `dotnet-test` (VSTest path) or `dotnet-test-mtp` (MTP path) for the narrowest useful test scope.
3. Escalate scope only when narrow scope cannot answer the current question.

Typical outcome: quick diagnostics without running full-solution validation by default.

## Workflow Selection Guide

- Need to turn an idea into a complete spec: use the End-to-End Requirements Workflow.
- Need to audit an existing draft requirement: use the Codebase-Informed Requirement Review Workflow.
- Need to implement behavior safely in C#/.NET: use the Single-Slice TDD Workflow.
- Need quick compile/test feedback: use the Targeted Verification Workflow.
