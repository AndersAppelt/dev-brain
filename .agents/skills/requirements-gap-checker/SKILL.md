---
name: requirements-gap-checker
description: "review feature requirements for completeness, contradictions, and missing acceptance criteria before implementation starts. use when the user already has a draft requirement, a refined feature description, notes from discovery, a codebase review, or supporting files and wants to know what is still missing to make the requirement exhaustive. always evaluate happy path, edge cases, validation, permissions, data model changes, contracts, observability, rollout, testability, and open questions. identify missing decisions and ambiguities clearly instead of pretending the draft is ready."
---

# Requirements Gap Checker

Act as the final completeness pass before a requirement becomes a working feature spec or optional Jira-ready item.

## Core rules

- Treat every draft as incomplete until checked systematically.
- Use the requirement text, supporting files, links, uploads, PDFs, and codebase findings together when available.
- Be explicit about contradictions, vague language, hidden assumptions, and unverifiable statements.
- Prefer precise gaps over vague criticism.
- Tie each gap to a consequence: ambiguity, incorrect implementation risk, missing testability, rollout risk, or operational blind spot.

## PDF and blocked-artifact handling

If any input is a PDF, attempt to read it before concluding the requirement has gaps that the PDF might answer. Prefer native PDF extraction first, inspect visual pages when the text alone looks incomplete, and use OCR only as a last resort. If a needed PDF-reading step is blocked by permissions or unavailable capabilities, ask for the required permission explicitly and note which completeness checks are still blocked until the PDF can be read.

## Review dimensions

Always check for completeness across all of these:

- scope boundaries
- happy path behavior
- edge cases and invalid inputs
- validation and error handling
- permissions, roles, and visibility
- data model, persistence, and migration implications
- API, UI, event, and integration contract changes
- observability, auditing, and support signals
- backward compatibility, rollout, and feature flags
- acceptance criteria and testability
- explicit non-goals
- unresolved open questions
- whether the ticket prefix and optional Jira-output decision are known before final writing starts

## Output structure

Use this structure:

### Ready or not
State whether the requirement is ready for implementation, ready with noted assumptions, or not ready.

### Inputs reviewed
List the draft requirement sources that were reviewed.

### Gaps that must be resolved
List blocking omissions or contradictions.

### Gaps that should be resolved
List important but non-blocking improvements.

### Ambiguous statements
Quote or paraphrase statements that can be interpreted in more than one way.

### Missing acceptance criteria
List the behaviors that still are not objectively testable.

### Recommended clarifying questions
Ask the smallest set of questions needed to close the important gaps.

## Severity guidance

- **Must resolve** when multiple implementations could satisfy the text differently, or when safety, data, auth, contract, migration behavior, required ticket prefix, or explicit output choice is under-specified.
- **Should resolve** when the missing detail would not block initial implementation but would weaken quality, rollout, supportability, or testability.

## Boundaries

- Do not implement the feature.
- Do not silently invent answers to close gaps.
- Do not turn the output into the final polished spec unless explicitly asked.
