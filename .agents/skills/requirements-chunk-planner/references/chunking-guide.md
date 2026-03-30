# Chunking Guide

Use this checklist to judge whether a proposed chunk is actually deployable.

## Deployable chunk checklist

A strong chunk usually answers yes to most of these:
- Can it be merged and deployed without waiting for all later chunks?
- Does it have a clear boundary and purpose?
- Can the team validate it independently?
- Is rollback or containment obvious?
- Does it reduce uncertainty for later work?
- Does it avoid hidden dependency on unfinished UI, API, or data flows?

## Prefer these patterns

### Vertical slice
A thin end-to-end increment through the affected layers.

### Internal-first rollout
Ship a chunk for internal users, admins, or flagged traffic first.

### Compatibility bridge
Introduce the adapter, translation layer, or fallback path that makes later chunks safer.

### Read-before-write
For risky integrations, start with safe retrieval or observability before mutation.

## Use enabling chunks carefully

Sometimes the first chunk must create infrastructure, a migration path, or a feature flag. That is acceptable only when the chunk is still safe to deploy and its value is clear. Explain why it needs to exist before later slices.

## Anti-patterns

### Layer split without value
Database, backend, and frontend as separate chunks is usually a work breakdown, not a deployable plan.

### Giant first chunk
If the first chunk changes many surfaces at once, it is probably too large.

### Hidden dependency
If chunk 2 cannot work unless chunk 4 is also present, the sequence is misleading.

### Fake deployability
A chunk that compiles but cannot be validated or safely rolled back is not meaningfully deployable.

## Default tie-breakers

When multiple chunking strategies seem reasonable, prefer the one that:
1. reduces risk earliest
2. proves the main user outcome earlier
3. minimizes migration and compatibility complexity
4. keeps review scope small
