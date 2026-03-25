---
name: csharp-test-refactor
description: refactor recently touched c# or .net tests and the smallest related production code after a passing green step. use when the user explicitly asks to refactor, improve readability, remove duplication, simplify setup, rename for clarity, or clean up the just-completed tdd slice while preserving behavior. keep the refactor narrow and reversible, prefer readability over cleverness, and verify through dotnet-targeted-build plus dotnet-test or dotnet-test-mtp. do not use for new behavior, fresh failing tests, or broad codebase cleanup.
---

# Csharp Test Refactor

Refactor only after green, and preserve behavior.

## Non-negotiable rules

- Refactor only when explicitly asked.
- Preserve behavior exactly.
- Keep the refactor focused on the current slice and its immediate neighborhood.
- Prefer readability, naming, duplication removal, and fixture simplification over architectural churn.
- Verify through the dedicated build and test skills before stopping.

## Good refactors

Prefer changes like these:

- extract a small helper that removes mechanical setup noise
- rename a test, helper, variable, or method for clarity
- collapse duplicated arrange code
- simplify test fixture or builder usage
- move magic values to named constants only when that improves readability
- reduce accidental complexity in the just-touched implementation

## Refactors to avoid by default

- introducing new abstractions "for future flexibility"
- reorganizing unrelated files
- changing public APIs without a clear need
- rewriting many tests for style consistency
- bundling performance work or behavior changes into the refactor step

## Output contract

Produce the response in this shape:

### Refactor goal
State the single readability or maintainability improvement.

### Refactor change
Provide the focused refactor only.

### Verification
State the narrowest build scope for `dotnet-targeted-build` and the narrowest test scope for `dotnet-test` or `dotnet-test-mtp`.

### Stop
Ask whether to continue with the next red step.

## Boundaries

- Do not add new behavior.
- Do not write new failing tests.
- Do not turn refactor into redesign.
- Do not continue automatically into the next loop.
