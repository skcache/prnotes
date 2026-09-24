# Evaluation

Judge outputs against behavior, not exact wording.

## Failure modes

These are the ways a PR note goes wrong. Each one is a scoring failure.

| Failure | Looks like |
|---|---|
| Template theater | every heading emitted, including an empty `### Flow` and a "Before / after: N/A" |
| Fabricated verification | `- [x]` on tests that were never run |
| Invented metrics | a delta table where only one column was measured |
| Screenshot fabrication | a before image that was never captured, or a stale one presented as current |
| Diagram sprawl | a diagram for a linear path, or one giant diagram spanning unrelated subsystems |
| File-list bullets | implementation lines that list touched files instead of review-relevant mechanisms |
| Narration | "This PR aims to…", commit-by-commit walkthrough, closing summary |
| Refactor UX fiction | an invented before/after user story for a behavior-preserving change |
| Security vagueness | an auth change described as "improves sign-in reliability" |
| Hidden failure | failing tests or unrun CI presented as green |
| Bloat | the note takes longer to read than the diff |
| Diff blindness | a note written from an issue title when the diff was never read |
| Meta-commentary | the note explaining its own structure, or a PR comment explaining how the note was written |
| Forensic report | documenting the investigation instead of the change |
| Prose over pixels | a paragraph describing a visual difference that a capture would settle in one look |

## Cases

| Case | Must | Must not |
|---|---|---|
| Tiny null guard | exact condition, the path that no longer reaches it, one test | evidence section, diagram, more than a few lines |
| Visual UI fix | captured before/after pair, cropped, consistent framing | prose standing in for a capture that was possible |
| Visual fix, old state unrecoverable | say BEFORE is unavailable, describe old behavior in text | a fabricated or unrelated before image |
| Auth / event routing | the decision point, preserved click and keyboard paths | a UX-flavored summary |
| State machine | the new transition and the states it can no longer reach | a restated state list |
| API behavior change | request/response delta, unchanged consumers, failure semantics | "endpoint updated" |
| Backend performance | measured delta with conditions | an unmeasured claim |
| Perf claim, no benchmark | what changed, "not measured", the reason it should help | numbers, a one-column table |
| Cache / concurrency | the invariant that makes it correct — ordering, keying, eviction, ownership | a description of the code shape |
| Refactor | preserved contract, new boundary, equivalence evidence | invented before/after UX |
| Migration | forward, rollback, existing rows, deploy ordering | "adds a column" |
| Large multi-subsystem | reading order, mechanical vs decision-bearing, out of scope | one generic summary, one all-system diagram |
| Incomplete coverage | covered and uncovered paths named | partial coverage presented as proof |
| Issue disagrees with diff | the disagreement stated explicitly | silently following either one |
| Security-sensitive | trust boundary, what is newly possible, what is not covered | vague reliability language |
| Dependency bump | version, reason, security relevance, behavior risk | a changelog restatement |
| Docs, text only | what a reader now learns | a diagram |
| README / rendered output | classified as visual; before/after captures of the rendered result; a one-line delta | a table about markdown mechanics, an essay about the fix, "docs-only so no screenshot" |
| Generated code | generator, changed input, regenerate command, hand-written source | line-by-line narration of generated files |
| Diff not accessible | say what could not be inspected, ask or stop | reconstructing the change from the issue title |
| Failing tests / CI not run | the failure named, CI status stated honestly | implying a green run |

## Regression case: rendered-output change

The case that catches "technically correct, visually exhausting".

Facts:

- a README example renders incorrectly on GitHub
- the fix changes README source only
- the visible result is dramatically different
- both revisions can be rendered

Expect:

- classified as **visually observable**, not "docs-only"
- before/after captures of the rendered region, same width and theme, cropped tight
- a one-to-two sentence behavior delta
- at most two implementation bullets
- at most three short verification bullets
- the whole body scannable in under 15 seconds
- no table about markdown mechanics
- no self-referential comment explaining how the note was written
- no "docs-only means no screenshot" reasoning anywhere

Penalize heavily when the output is correct but exhausting. A note that has to
explain itself has already failed.

## Rubric

Score 0-2 on:

1. behavior delta clarity
2. evidence quality and honesty (including visual evidence)
3. diagram judgment
4. implementation selectivity
5. preserved behavior
6. verification specificity
7. factual restraint
8. conciseness

Maximum: **16**. A fabricated fact caps the total at 8. A note a reviewer cannot scan in 15 seconds caps it at 10.
