# PR Notes principles

## A PR description is a review interface

A diff tells the reviewer exactly what changed in code. It does not reliably explain:

- why the change exists
- what behavior changed
- which branch is important
- what must remain unchanged
- what evidence supports correctness

PR Notes fills that gap.

## Compression, not narration

The objective is not completeness. It is useful compression.

Prefer the smallest set of facts that lets a reviewer build the correct mental model.

A strong note often contains less text than a weak one because screenshots, metrics, a tiny flow diagram, and precise invariants carry more information than prose.

## Evidence hierarchy

Prefer, when applicable:

1. observable before/after evidence
2. tests exercising the changed path
3. a small control-flow diagram
4. correctness-critical implementation details
5. logs or metrics for operational behavior

Do not add evidence merely to make the PR look substantial.

## Diagrams explain decisions

A diagram earns its place when it makes branching or sequencing clearer than prose.

Good candidates:

- one click can take two paths
- auth changes based on state
- controller selection changes behavior
- request retries or falls back
- data moves through a non-obvious sequence

Bad candidates:

- one-line guards
- flat file changes
- obvious renames
- diagrams that repeat the same bullets

## Invariants are review targets

A useful PR note names behavior that should not move.

Examples:

- switch clicks still toggle
- keyboard activation remains intact
- cache eviction semantics are unchanged
- timeout ownership stays with the caller
- API response shape is unchanged

This converts hidden regression risk into an explicit review target.

## Factual restraint

Do not upgrade a hypothesis into a result.

If performance was not measured, do not claim it improved.

If a test was not run, do not check the box.

If a screenshot does not exist, do not describe one as evidence.

A concise incomplete truth is better than a polished fabricated PR.
