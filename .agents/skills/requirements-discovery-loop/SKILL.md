---
name: requirements-discovery-loop
description: develop exhaustive feature requirements from a rough idea, request, bug report, or partially written specification. use when the user wants to flesh out a feature, clarify requirements, turn an idea into an implementable spec, prepare work for agents, or produce backlog-ready jira requirements without restating process constraints. orchestrate the requirements flow by asking focused clarifying questions, inspecting an existing codebase through codebase-requirements-reviewer when available, checking completeness through requirements-gap-checker, and finishing through feature-spec-writer. always consider happy path, edge cases, validation, permissions, data model, contracts, observability, rollout, testability, and open questions.
---

# Requirements Discovery Loop

Drive the conversation until the requirement is precise enough to be written as both an agent-oriented feature spec and a backlog-ready requirements draft.

## Core rules

- Infer the process automatically so the user does not need to restate it.
- Ask focused clarifying questions in small batches instead of dumping a giant questionnaire.
- Prefer the highest-leverage missing decisions first.
- Inspect the existing codebase before asking many speculative questions when a repo exists.
- Stay observational when reading code: identify current behavior, constraints, and missing decisions; do not implement features.
- Never claim the requirement is exhaustive if important questions remain unanswered.
- Always consider the full checklist: happy path, edge cases, validation and error handling, permissions and auth, data model and migrations, API or UI contract changes, observability and logging, rollout and backward compatibility, testability, and open questions.

## Flow

1. **Start from the user's idea or draft**
   - Restate the feature in one or two sentences.
   - Identify the most obvious missing decisions.
   - If a codebase exists or the user mentions existing behavior, inspect the relevant area through `codebase-requirements-reviewer` before asking many follow-up questions.

2. **Clarify incrementally**
   - Ask the smallest useful set of questions needed to unblock real specification work.
   - Prefer 3 to 7 questions at a time.
   - Group questions by theme when helpful.

3. **Check completeness**
   - When enough detail exists, hand off to `requirements-gap-checker`.
   - Surface contradictions, omissions, unverifiable claims, and missing acceptance criteria.

4. **Write outputs**
   - When the requirement is ready, hand off to `feature-spec-writer`.
   - Produce both outputs in one pass unless the user asks for only one.

## What to ask about by default

Always consider whether the current requirement is missing any of these:

- user roles and permissions
- entry points and triggers
- happy path behavior
- edge cases and invalid input
- state transitions and persistence
- API, events, UI, or integration contracts
- migration or backward compatibility concerns
- logging, metrics, audit, or support visibility
- failure modes and user-visible errors
- acceptance criteria and testability
- rollout constraints or feature flags

Ask only the questions that matter most now.

## When a codebase exists

Before broad questioning, use `codebase-requirements-reviewer` to learn:

- where the current behavior lives
- which abstractions, data shapes, and integrations already exist
- what constraints or inconsistencies the code introduces
- what the requirement draft fails to mention

Then ask sharper questions informed by that review.

## Response shape while discovery is ongoing

Use this structure:

### Current understanding
A short summary of the feature as currently understood.

### Missing decisions
A short list of the most important unanswered or ambiguous points.

### Questions for you
Ask only the next small batch of clarifying questions.

### Next step
State whether the next move is more discovery, a codebase review, a gap check, or writing the final outputs.

## Response shape when ready to finalize

Use this structure:

### Current understanding
Short final summary.

### Completeness check
State whether any non-blocking open questions remain.

### Next step
Say that the requirement is ready for `feature-spec-writer` and produce both outputs.

## Boundaries

- Do not implement code.
- Do not jump straight to a polished spec if critical ambiguities remain.
- Do not ask questions that can be answered directly from the codebase.
- Do not ignore edge cases or operational concerns just because the initial request sounds simple.
