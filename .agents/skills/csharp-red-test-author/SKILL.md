---
name: csharp-red-test-author
description: write exactly one meaningful failing test for a c# or .net codebase based on a requirement, acceptance criterion, bug report, or existing code analysis. use when the task is to start the red step of tdd, prove that a feature does not yet exist, reproduce a bug with a test, or choose the smallest next failing behavior. keep tests concise, readable, and specialized; create helpers only when they reduce setup noise; never fake failure with unconditional assertions; never change production code; and hand off execution to dotnet-test or dotnet-test-mtp. do not use for implementing the fix, broad refactors, or writing multiple new tests at once.
---

# Csharp Red Test Author

Write one failing test that fails for the right reason.

## Non-negotiable rules

- Write exactly one new failing test.
- Keep the test small enough to describe a single behavior.
- Make the failure meaningful: the failure must point to the missing behavior or the present bug.
- Never force failure with `Assert.True(false)`, `Assert.Fail()`, throwing manually, or any equivalent fake failure.
- Never change production code.
- Create helpers only when they improve readability and hide mechanical setup rather than test intent.

## Choose the right failing mechanism

Prefer these failure modes in order:

1. **Specific assertion failure** when the API exists but behavior is wrong.
2. **Exception expectation mismatch** when the behavior should reject or accept something differently.
3. **Compile-time failure** only when the required public contract itself is missing and the requirement makes that contract explicit.

A compile-time red test is acceptable when the absence of a type, method, property, or overload is the clearest proof that the feature does not yet exist. Do not use compile-time failure as a shortcut when a runtime behavior test is possible.

## Analyze before writing

Before producing the test:

1. Inspect the relevant production code and nearby tests.
2. Mirror the local test framework, naming style, fixture style, and assertion library.
3. Find the smallest observable behavior slice that advances the requirement.
4. Reuse existing builders, factories, or fixture helpers when they keep the test readable.
5. Avoid asserting through multiple layers when a closer assertion exists.

## Test writing rules

- Prefer explicit arrange-act-assert structure unless the local style uses another clear pattern.
- Name the test so the failure reads like a concrete requirement.
- Keep assertions specific. Avoid broad "not null" or "is true" assertions when an exact value, message, type, or state can be checked.
- Keep setup local unless extracting a helper materially improves readability.
- If a helper is needed, keep it tiny and domain-named.
- Avoid adding multiple scenarios, parameter matrices, or theory rows in the red step unless the single next behavior is inherently data-driven.

## Output contract

Produce the response in this shape:

### Chosen behavior
One sentence describing the exact missing behavior or bug manifestation.

### Failing test
Provide only the new or changed test code and any tiny helper needed for readability.

### Why this fails meaningfully
Explain the exact reason this test should fail today.

### Targeted execution
State the narrowest test scope that should be run through `dotnet-test` or `dotnet-test-mtp`.

### Stop
Stop and wait for review. Do not propose a fix unless the user asks to proceed to green.

## Boundaries

- Do not write multiple tests as options.
- Do not add production code.
- Do not rewrite unrelated tests.
- Do not hide intent behind generic test helpers or over-abstracted builders.
- Do not broaden the scope just because the requirement document is broad.
