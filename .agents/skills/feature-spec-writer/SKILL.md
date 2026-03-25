---
name: feature-spec-writer
description: "turn clarified requirements into two synchronized outputs: an exhaustive agent-oriented feature specification and a backlog-ready jira requirements draft. use when the user has provided a requirement, answered clarifying questions, or completed discovery and wants a concrete deliverable that agents can implement from and humans can schedule in jira. include all relevant behavior, constraints, edge cases, acceptance criteria, operational concerns, and explicit open questions. do not invent missing decisions; instead mark unresolved items clearly and keep both outputs aligned."
---

# Feature Spec Writer

Produce two aligned requirement artifacts from the clarified inputs:

1. an agent-oriented feature specification intended for implementation agents
2. a backlog-ready Jira-style requirements draft intended for planning and tracking

## Core rules

- Keep the two outputs consistent.
- Prefer precise, testable language over aspirational language.
- Write unresolved assumptions and open questions explicitly instead of filling them in silently.
- Carry forward the full exhaustive checklist by default.
- Make acceptance criteria objective enough that another agent could derive implementation and tests from them.

## Output 1: agent-oriented feature specification

Use this structure:

# Feature specification

## Summary
A short summary of the feature and intended user value.

## Goals
Concrete goals this feature must achieve.

## Non-goals
What this feature intentionally does not cover.

## Actors and permissions
Relevant user roles, visibility rules, and authorization constraints.

## Current-state context
Only the context needed from the existing system.

## Desired behavior
Describe the behavior in a structured way, including triggers, workflow, state changes, side effects, and user-visible results.

## Edge cases and failure handling
Describe invalid inputs, conflict cases, retries, empty states, and user-visible errors.

## Data and contract impact
Describe model changes, persistence concerns, migrations, API or event changes, UI contract impact, and backward compatibility expectations.

## Observability and operations
Describe logging, metrics, audit trails, support signals, rollout or feature flags, and operational considerations.

## Acceptance criteria
Use a numbered list of precise, testable behaviors.

## Open questions
List any unresolved decisions that still need answers.

## Output 2: backlog-ready Jira requirements draft

Use this structure:

# Jira draft

## Title
One concise title.

## Problem / context
One short paragraph.

## User story or requirement statement
Use a clear story or requirement format appropriate to the feature.

## Scope
Bullet the included scope.

## Out of scope
Bullet the excluded scope.

## Acceptance criteria
Reuse the same acceptance criteria in backlog-friendly form.

## Dependencies / impacted areas
List systems, modules, services, or teams affected.

## Risks / rollout notes
List rollout, migration, compatibility, operational, or support concerns.

## Open questions
List unresolved decisions.

## Writing guidance

- Reuse the same facts in both outputs, just reformatted for the audience.
- If the requirement is not truly complete, keep writing but flag the unresolved parts clearly.
- Prefer agent-usable specificity over polished prose.
- Keep Jira language concise and prioritization-friendly.

## Boundaries

- Do not write implementation code.
- Do not omit important caveats just to make the spec sound finished.
- Do not produce only one output unless the user asked for only one.
