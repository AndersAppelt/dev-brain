---
name: feature-spec-writer
description: "turn clarified requirements into an agent-oriented feature specification and, optionally, a backlog-ready jira requirements draft. use when the user has provided a requirement, answered clarifying questions, completed discovery, or supplied supporting files and wants concrete deliverables that agents can implement from and humans can optionally schedule in jira. always produce the agent-oriented feature specification, ask whether a jira description is wanted if that is not already known, and ask for a ticket prefix such as `ABC-123` if it is not already known. save the agent-oriented specification in a repo-root docs folder using a filename that starts with the ticket prefix and continues with a generated slug. do not invent missing decisions; instead mark unresolved items clearly and keep all outputs aligned."
---

# Feature Spec Writer

Produce an agent-oriented feature specification from the clarified inputs and optionally produce a Jira-style requirements draft.

## Core rules

- Always produce the agent-oriented feature specification.
- Ask whether the user wants a Jira description unless that decision is already known.
- Ask for the ticket prefix, for example `ABC-123`, unless it is already known.
- Keep all outputs consistent with the clarified inputs.
- Prefer precise, testable language over aspirational language.
- Write unresolved assumptions and open questions explicitly instead of filling them in silently.
- Carry forward the full exhaustive checklist by default.
- Make acceptance criteria objective enough that another agent could derive implementation and tests from them.

## Input handling

Treat all of these as valid inputs when present:

- the clarified conversation
- notes from discovery
- codebase review findings
- gap-check findings
- repository-relative file paths
- pasted links or URLs
- uploaded files
- PDFs supplied by path, link, or upload

If multiple sources disagree, call that out explicitly in the outputs.

## PDF and blocked-artifact handling

When any supporting input is a PDF, attempt to read it before writing the outputs. Prefer native PDF extraction first, inspect visual pages when diagrams, tables, or screenshots may carry requirements, and use OCR only as a last resort. If a needed PDF-reading step is blocked by permissions or unavailable capabilities, do not continue as though the PDF had been reviewed. Instead, tell the user what was attempted, what failed, what permission is needed, and whether final writing is blocked or only partially blocked.

## Mandatory decisions before writing

Before final writing starts, ensure both of these are known:

1. whether a Jira description is wanted
2. the ticket prefix to use in the agent-spec filename

If either is unknown, ask before continuing.

## Output 1: agent-oriented feature specification

### File location rule

Write the agent-oriented spec into a repo-root folder named `docs`.

- If `docs` does not exist, create it.
- The filename must start with the ticket prefix, then a generated slug based on the feature title.
- Use the pattern: `docs/<ticket-prefix>-<generated-slug>.md`
- Example: `docs/ABC-123-user-can-archive-projects.md`

Generate the slug yourself from a concise feature title.

If the environment does not allow file creation, present the exact file path that should be created and the full file contents.

### File content structure

Use this structure inside the agent spec:

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

## Output 2: optional Jira requirements draft

Only produce this output if the user wants it.

Use this exact header structure:

# Jira draft

## Background
## Description
## Business requirements
## Technical Requirements
## Acceptance Criteria
## Open Questions

## Writing guidance for the Jira draft

- Keep the Jira draft concise and planning-friendly.
- Reuse the same facts as the agent spec, reformatted for backlog use.
- Keep the acceptance criteria aligned with the agent spec.
- Do not add sections beyond the required header structure.

## Writing guidance overall

- Reuse the same facts in all outputs, just reformatted for the audience.
- If the requirement is not truly complete, keep writing but flag the unresolved parts clearly.
- Prefer agent-usable specificity over polished prose.
- Generate the filename slug automatically; never ask the user to propose the slug.

## Boundaries

- Do not write implementation code.
- Do not omit important caveats just to make the spec sound finished.
- Do not produce the Jira output unless the user wants it.
- Do not proceed without the ticket prefix.
