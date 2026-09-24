# Evaluation cases

Judge generated PR notes against the expected properties, not exact wording.

## 1. UI event-routing bug

Facts:

- A row contains a switch.
- Row clicks currently toggle the switch because of label behavior.
- For `needs_auth` rows, a row click should start OAuth instead.
- Direct switch clicks must still toggle enabled state.
- Non-auth rows must be unchanged.
- Browser tests cover both click targets.
- Before and after screenshots are available.

Expected:

- opens with old and new behavior
- uses before/after evidence
- uses a small event-routing diagram
- explicitly preserves direct-switch and non-auth behavior
- verification names both click paths
- does not summarize every changed file

## 2. Tiny null guard

Facts:

- A missing optional value can make one formatter throw.
- The fix returns an empty label when the value is absent.
- A unit test was added.
- No useful visual delta exists.
- Control flow is obvious.

Expected:

- concise behavior delta
- no forced screenshot section
- no diagram
- exact implementation fact
- unit test listed

## 3. Backend latency improvement

Facts:

- Batching reduces network calls from 20 to 4 per operation.
- p95 falls from 140 ms to 61 ms.
- Measurements use the same 50k-operation workload and hardware.
- Failure semantics are unchanged.
- Integration tests pass.

Expected:

- measurable before/after table
- measurement conditions stated
- batching boundary explained
- unchanged failure semantics called out
- no fake visual UX language

## 4. Behavior-preserving refactor

Facts:

- Three duplicated retry-policy builders become one helper.
- Retry count, backoff, and status-code list remain identical.
- Existing tests pass unchanged.

Expected:

- immediately states no intended behavior change
- no manufactured UX before/after
- explains structural duplication and new boundary
- lists preserved retry contract
- uses unchanged tests as equivalence evidence

## 5. Insufficient evidence

Facts:

- The author says "this should improve performance."
- No benchmark was run.
- The diff changes allocation strategy.
- Unit tests pass.

Expected:

- no invented performance numbers
- no factual claim that performance improved
- describes the implementation change and current verification
- benchmark claim is omitted or marked pending

## 6. Oversized PR

Facts:

- The PR changes authentication, billing, and navigation.
- 54 files changed.
- Behavior changes are loosely related.
- The author asks for one concise description.

Expected:

- groups notes by reviewer-relevant subsystem if possible
- surfaces shared invariants once
- does not hide breadth behind a generic summary
- may explicitly flag that the PR is broad to review
- avoids a giant all-system diagram

## Scoring

Score each output from 0-2 on:

1. behavior delta clarity
2. evidence quality
3. diagram judgment
4. implementation selectivity
5. preserved behavior / invariants
6. verification specificity
7. factual restraint
8. conciseness

Maximum: **16**.

Do not accept a skill change because one example looks prettier. It should improve or preserve behavior across the full case set.
