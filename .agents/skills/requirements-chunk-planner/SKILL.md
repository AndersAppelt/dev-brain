---
name: requirements-chunk-planner
description: break an approved feature requirement or agent-facing feature spec into smaller, individually deployable implementation chunks. use when discovery is complete and the next step is planning incremental delivery, defining vertical slices, sequencing work, identifying dependencies, or turning one large feature into safe deployable increments. prefer this skill after requirements-discovery-loop, requirements-gap-checker, or feature-spec-writer have produced a stable requirement. do not use this skill to invent requirements from scratch or to write implementation code.
---

# Requirements Chunk Planner

Break an approved requirement into the smallest reasonable sequence of deployable slices.

## Inputs to accept

Accept any combination of these inputs:
- a concise feature description from the user
- an agent-facing spec already written in `docs/`
- repository-relative paths to supporting files
- pasted links or URLs to supporting docs
- uploaded files
- PDFs supplied by path, link, or upload
- a Jira draft, if the user already has one

Treat pointed files, linked docs, and uploaded files as first-class inputs. Read them before chunking when they appear relevant.

If the requirement is still vague, contradictory, or missing important decisions, do not force a breakdown. State what is unresolved and send the user back to the discovery flow.

## PDF and blocked-artifact handling

Treat PDFs as first-class source material for chunking. Attempt to read them before deciding whether the requirement is ready to slice. Prefer native PDF extraction first, inspect visual pages when diagrams or tables may affect chunking boundaries, and use OCR only as a last resort. If a needed PDF-reading step is blocked by permissions or unavailable capabilities, ask for the required permission explicitly and explain whether chunking is blocked until the PDF can be reviewed.

## Workflow

1. Confirm the source material.
   - Prefer an approved agent-facing spec when one exists.
   - If the user provides multiple supporting sources, reconcile them and call out conflicts.
2. Check chunking readiness.
   - Confirm the requirement is specific enough to slice.
   - Reject premature breakdowns when business rules, boundaries, or acceptance criteria are still unstable.
3. Identify the thinnest end-to-end slices.
   - Prefer vertical slices that can be deployed safely.
   - Avoid layering-only chunks such as “database first, API later, UI later” unless the user explicitly wants that plan.
4. Produce a deployable sequence.
   - Each chunk must deliver a meaningful increment.
   - Each chunk must have a clear boundary, rollout story, and validation story.
5. Highlight risk and coupling.
   - Surface prerequisites, migrations, feature flags, compatibility concerns, and rollback considerations.
6. End with a recommendation for the first chunk.

## Rules for good chunking

Always optimize for deployability, reversibility, and reviewability.

### Do
- Prefer thin vertical slices over technical-layer splits.
- Keep chunks independently understandable.
- Make dependencies explicit.
- Note which chunk creates enabling infrastructure and why that chunk is still deployable.
- Include rollout notes when a feature flag, dark launch, migration, or compatibility bridge is needed.
- Preserve user value in every chunk where possible.
- Keep chunk names short and specific.

### Do not
- Do not produce a vague checklist of implementation tasks.
- Do not create chunks that only make sense when all remaining chunks are complete, unless the user explicitly accepts that tradeoff.
- Do not hide risky coupling.
- Do not write code.
- Do not silently invent missing business rules.

## Output

Produce a concise markdown breakdown using this structure.

# Chunk plan: [feature name]

## Summary
- Total chunks: [N]
- Recommended first chunk: [name]
- Major risks: [short list]

## Proposed sequence

### Chunk 1: [short name]
**Goal**: [what becomes possible after this chunk]
**Why this is separately deployable**: [deployment boundary]
**Scope**:
- [item]
- [item]
**Out of scope**:
- [item]
- [item]
**Dependencies / prerequisites**:
- [item]
**Validation**:
- [how to confirm it works safely]
**Rollout / compatibility notes**:
- [flag, migration, fallback, or none]
**Risks / unknowns**:
- [item]

Repeat for each chunk.

## Cross-cutting concerns
- Data and migrations
- Backward compatibility
- Operational visibility
- Testing strategy
- Release / rollback considerations

## Recommendation
- Start with: [chunk name]
- Because: [brief reasoning]

## When to send the user back to discovery

Do not finish a chunk plan when any of these are true:
- the core user outcome is still unclear
- there is no stable acceptance boundary
- critical files or linked references conflict
- the requirement contains unresolved product decisions that materially affect slicing

In those cases, list the missing decisions and tell the user to return to the requirements discovery flow first.

## Examples of strong chunking

### Good
- “Introduce read-only retrieval behind a feature flag”
- “Support creation for one happy-path case with explicit validation boundaries”
- “Add internal-only visibility before external rollout”

### Weak
- “Make database changes”
- “Implement backend”
- “Implement frontend”
- “Finish remaining work”

## Reference

See `references/chunking-guide.md` for the chunk quality checklist and anti-patterns.
