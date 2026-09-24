# PR Notes principles

## A PR description is a review interface

A diff is precise about code. It is often poor at communicating intent.

The reviewer still has to infer:

- why the change exists
- what behavior changed
- which branch matters
- what must remain unchanged
- what evidence supports correctness

PR Notes provides that missing context.

## Compression, not narration

The objective is useful compression.

Prefer the smallest set of facts that gives the reviewer the correct mental model.

Screenshots, metrics, a tiny flow diagram, and explicit invariants often carry more information than paragraphs of prose.

## Evidence hierarchy

Prefer, when applicable:

1. observable before / after evidence
2. tests exercising the changed path
3. a small control-flow diagram
4. correctness-critical implementation details
5. logs or metrics for operational behavior

Do not add evidence merely to make the PR look substantial.

## Diagrams explain decisions

A diagram earns its place when branching or sequencing is clearer visually than in prose.

Good candidates:

- one interaction can take two paths
- auth behavior depends on state
- controller selection changes behavior
- requests retry or fall back
- data moves through a non-obvious sequence

Bad candidates:

- one-line guards
- obvious renames
- flat file changes
- diagrams that repeat the bullets

## Invariants are review targets

Useful PR notes name behavior that should not move.

Examples:

- switch clicks still toggle
- keyboard activation remains intact
- cache eviction semantics are unchanged
- timeout ownership stays with the caller
- API response shape is unchanged

This turns hidden regression risk into an explicit review target.

## Factual restraint

Do not upgrade a hypothesis into a result.

If performance was not measured, do not claim it improved.

If a test was not run, do not check the box.

If a screenshot does not exist, do not describe one as evidence.

A concise incomplete truth is better than a polished fabricated PR.
