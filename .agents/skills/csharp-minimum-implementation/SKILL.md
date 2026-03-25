---
name: csharp-minimum-implementation
description: write the minimum production code needed to make one approved c# or .net red test stop failing. use when the user has reviewed a single failing test and wants the green step of tdd, asks for the smallest fix that satisfies the current test, or wants the next implementation increment without extra behavior. keep the change narrow, avoid opportunistic refactors, preserve existing behavior, use dotnet-targeted-build for compile feedback when helpful, and route test reruns through dotnet-test or dotnet-test-mtp. do not use for writing new tests, broad redesigns, cleanup passes, or multi-feature implementations.
---

# Csharp Minimum Implementation

Make the approved red test pass with the smallest defensible change.

## Non-negotiable rules

- Assume exactly one red test has already been selected and reviewed.
- Change only what is necessary to satisfy that test.
- Do not add unrelated behavior, edge cases, optimizations, or cleanup unless the test strictly requires them.
- Do not refactor while implementing green.
- Prefer the smallest edit surface: the narrowest method, class, or mapping that satisfies the test.
- Use `dotnet-targeted-build` for compile-only feedback when needed.
- Use `dotnet-test` or `dotnet-test-mtp` for verification.

## Decide whether to proceed

Before writing code, verify that the red test is a valid target for green:

- If the red test is too broad, ambiguous, or clearly testing the wrong behavior, say so and ask to adjust the test instead of writing speculative implementation.
- Otherwise, proceed with the smallest change that makes that test pass.

## Implementation rules

- Prefer extending existing behavior over introducing a new abstraction.
- Prefer a direct conditional, branch, or mapping update over a new pattern or framework.
- If the missing contract is public API, add only the member required by the test.
- If the test requires a collaborator seam, add the smallest seam that preserves current design intent.
- Keep touched files to a minimum.
- Leave comments only when the code would otherwise be misleading.

## Output contract

Produce the response in this shape:

### Approved behavior
Restate the single behavior being implemented.

### Minimum code change
Provide only the production code change needed for green.

### Verification
State the narrowest build scope to check through `dotnet-targeted-build` if needed, then the narrowest test scope to rerun through `dotnet-test` or `dotnet-test-mtp`.

### Stop
Stop and wait for review. Do not refactor yet.

## Boundaries

- Do not write another test.
- Do not combine green with refactor.
- Do not improve surrounding design unless the current test cannot pass without it.
- Do not widen test execution scope by default.
