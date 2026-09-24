# PR Notes principles

## The PR description is a review interface

A diff is precise about code and poor at communicating intent. A reviewer still has to work out why the change exists, which path it changes, and what must not move.

PR Notes supplies that context and nothing else. It is not a release note, a changelog, a commit summary, or an architecture document.

## Compression, not narration

Prefer the smallest set of facts that gives the reviewer a correct mental model. One matched before/after pair, one small diagram, and two invariants often carry more than four paragraphs.

Test every line: does this reduce the reviewer's uncertainty about this change? If not, delete it.

## Evidence hierarchy

Prefer, in order:

1. before/after visual or measured evidence from the actual change
2. tests that exercise the changed path
3. a small control-flow diagram
4. correctness-critical implementation detail
5. logs or metrics for operational behavior

Do not add evidence to make the PR look substantial.

## Observed vs inferred

Keep what you saw separate from what you concluded.

- Observed: a command you ran, a test output, a file you read, an image you captured.
- Inferred: a conclusion drawn from reading the code.

Inference is allowed and often necessary. Unlabelled inference presented as fact is not.

## When evidence is missing or weak

| Situation | Do |
|---|---|
| Not measured | say "not measured" and describe the change; no delta table |
| Measured under different conditions | report both runs with their conditions, or omit the comparison |
| Screenshots predate the change | omit them, or state that they are stale |
| Tests fail | say which ones fail and why the change still stands; never present a failing suite as verification |
| CI has not run | write "CI not run" |
| Coverage is partial | say which paths are covered and which are not |
| Old state cannot be reproduced | describe the old behavior in text; never fabricate a before image |

A concise incomplete truth beats a polished fabricated PR.

## Hard cases

### Security-sensitive changes

Any change to authentication, authorization, sessions, tokens, secrets, uploads, or trust boundaries must state:

- which trust boundary moved
- what is newly possible for an actor who could not do it before
- what is explicitly not covered

Never describe a security change in vague UX terms such as "improves sign-in reliability". Name the check that was added, moved, or removed.

### Schema and data migrations

State the forward direction, the rollback direction, what happens to existing rows, and whether the migration is safe to run before or after the code deploy. Note any lock, backfill, or downtime implication. "Adds a column" is not enough.

### Large multi-subsystem PRs

Give the reviewer a reading order instead of more prose:

- what to review first, and why
- which parts are mechanical (renames, generated output, formatting) and can be skimmed
- which parts carry the real decision
- shared invariants stated once, not repeated per file
- what is deliberately out of scope

At most one diagram per subsystem. Never one diagram spanning unrelated subsystems.

### Behavior-preserving refactors

State that no behavior change is intended, in the first sentence. Then give the structural problem, the new boundary, the preserved contract, and the evidence for equivalence. Do not fabricate a before/after UX story.

### Generated code

Do not narrate generated files. State the generator, what changed in its input, and the command that regenerates the output. Point the reviewer at the hand-written source that produced it.

### Dependency bumps

State the version change, the reason, whether it is a security fix, and what could shift in behavior. If the lockfile is the only substantive change, say so.
