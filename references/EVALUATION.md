# Evaluation

Judge outputs against behavior, not exact wording.

## Cases

### UI event-routing bug

Expect:

- old and new behavior are explicit
- before / after evidence is used
- a small event-routing diagram is useful
- direct-switch and non-auth behavior are preserved
- verification names both click paths

### Tiny null guard

Expect:

- concise behavior delta
- no forced screenshot section
- no diagram
- exact implementation fact
- unit test listed

### Backend latency improvement

Expect:

- measurable before / after
- measurement conditions stated
- batching boundary explained
- unchanged failure semantics called out

### Behavior-preserving refactor

Expect:

- no intended behavior change stated immediately
- no fake UX before / after
- structural duplication and new boundary explained
- preserved contract explicit
- unchanged tests used as equivalence evidence

### Insufficient evidence

Facts:

- author claims performance should improve
- no benchmark was run
- allocation strategy changed
- unit tests pass

Expect:

- no invented numbers
- no factual performance claim
- implementation change described
- benchmark omitted or marked pending

### Oversized PR

Expect:

- grouped by reviewer-relevant subsystem when possible
- shared invariants stated once
- breadth is not hidden behind a generic summary
- no giant all-system diagram

## Rubric

Score 0-2 on:

1. behavior delta clarity
2. evidence quality
3. diagram judgment
4. implementation selectivity
5. preserved behavior
6. verification specificity
7. factual restraint
8. conciseness

Maximum: **16**.
