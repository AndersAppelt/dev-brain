---
name: requirements-discovery-loop
description: "develop exhaustive feature requirements from a rough idea, request, bug report, partially written specification, or supporting files. use when the user wants to flesh out a feature, clarify requirements, turn an idea into an implementable agent spec, prepare work for agents, or optionally prepare a jira-ready description without restating process constraints. accept additional context from repository-relative paths, pasted links, uploaded files, and PDFs, and attempt to read those artifacts before treating them as unusable. orchestrate the requirements flow by asking focused clarifying questions, inspecting an existing codebase through codebase-requirements-reviewer when available, checking completeness through requirements-gap-checker, and finishing through feature-spec-writer. always consider happy path, edge cases, validation, permissions, data model, contracts, observability, rollout, testability, and open questions."
---

# Requirements Discovery Loop

Drive the conversation until the requirement is precise enough to be written as an agent-oriented feature spec and, if the user wants it, a Jira-ready requirements draft.

## Core rules

- Infer the process automatically so the user does not need to restate it.
- Accept additional context from repository-relative paths, pasted links or URLs, uploaded files, and PDFs.
- Read user-pointed artifacts before asking broad questions when those artifacts are likely to answer them.
- Ask focused clarifying questions in small batches instead of dumping a giant questionnaire.
- Prefer the highest-leverage missing decisions first.
- Inspect the existing codebase before asking many speculative questions when a repo exists.
- Stay observational when reading code: identify current behavior, constraints, and missing decisions; do not implement features.
- Never claim the requirement is exhaustive if important questions remain unanswered.
- Always consider the full checklist: happy path, edge cases, validation and error handling, permissions and auth, data model and migrations, API or UI contract changes, observability and logging, rollout and backward compatibility, testability, and open questions.

## PDF and blocked-artifact handling

Treat PDFs as first-class requirement inputs. When the user points to a PDF by repository path, link, or upload:

1. attempt to read it instead of ignoring it
2. prefer native PDF text extraction first
3. if the parsed text appears incomplete, inspect the visual pages because diagrams, tables, and screenshots may carry the important requirements
4. use OCR only as a last resort
5. if a needed step is blocked by missing access, a disabled capability, or a required permission escalation, say so explicitly and ask for the needed permission instead of silently skipping the PDF

When a PDF cannot be fully read, explain:
- what was attempted
- what failed
- what permission or additional action is required
- which discovery questions are blocked until the PDF can be read

## Mandatory decisions to collect

Before finalizing outputs, ensure these are known:

- whether the user wants a Jira-ready description in addition to the agent spec
- the ticket prefix to use in the agent-spec filename, for example `ABC-123`

If either is missing, ask explicitly.

## Flow

1. **Start from the user's idea or draft**
   - Restate the feature in one or two sentences.
   - Note any supporting files, links, or uploads the user provided.
   - Identify the most obvious missing decisions.
   - If a codebase exists or the user mentions existing behavior, inspect the relevant area through `codebase-requirements-reviewer` before asking many follow-up questions.

2. **Clarify incrementally**
   - Ask the smallest useful set of questions needed to unblock real specification work.
   - Prefer 3 to 7 questions at a time.
   - Group questions by theme when helpful.
   - Ask whether Jira output is wanted unless the user already said so.
   - Ask for the ticket prefix unless it is already known.

3. **Check completeness**
   - When enough detail exists, hand off to `requirements-gap-checker`.
   - Surface contradictions, omissions, unverifiable claims, and missing acceptance criteria.

4. **Write outputs**
   - When the requirement is ready, hand off to `feature-spec-writer`.
   - Always produce the agent-oriented spec.
   - Produce the Jira output only if the user wants it.

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

## When supporting files are provided

If the user points at files, links, or uploads as extra context:

- inspect them before asking questions they can answer
- distinguish source-of-truth requirements from illustrative notes or outdated drafts
- call out when supplied materials disagree with each other or with the codebase
- incorporate the relevant details into the evolving requirement summary

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

### Inputs reviewed
List the requirement sources already reviewed, such as user description, repository files, links, or uploads.

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

### Inputs reviewed
List the requirement sources reviewed.

### Completeness check
State whether any non-blocking open questions remain.

### Output decision
State whether the final pass will produce only the agent spec or both the agent spec and Jira draft.

### Next step
Say that the requirement is ready for `feature-spec-writer` and produce the final outputs.

## Boundaries

- Do not implement code.
- Do not jump straight to a polished spec if critical ambiguities remain.
- Do not ask questions that can be answered directly from the codebase or supplied artifacts.
- Do not ignore edge cases or operational concerns just because the initial request sounds simple.
