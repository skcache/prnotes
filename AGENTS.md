# AGENTS.md

## Purpose

This repository contains one Agent Skill: **PR Notes**.

Its job is to turn a code change into a concise, evidence-backed pull request description optimized for review speed and correctness.

## Before changing the skill

Read:

1. `SKILL.md`
2. `references/principles.md`
3. every file in `examples/`
4. `evals/cases.md`

## Non-negotiable behavior

Preserve these properties:

- **Behavior delta first.** Explain what changed in observable terms before implementation details.
- **Evidence over prose.** Prefer screenshots, metrics, tests, and exact states.
- **Conditional diagrams.** Add a diagram only when it reduces review effort.
- **Selective implementation notes.** Include correctness-critical mechanisms, not a file dump.
- **Preserved behavior matters.** State nearby paths that must not regress.
- **Verification maps to behavior.** Generic "tested locally" is insufficient.
- **No invention.** Never fabricate tests, screenshots, metrics, or implementation facts.
- **Conciseness is part of correctness.** Delete anything that does not help review.

## Refinement protocol

When improving the skill:

1. Identify a concrete failure mode.
2. Change the smallest instruction set that fixes it.
3. Keep the skill general across frontend, backend, systems, and refactor PRs.
4. Add or update an evaluation case for any new behavioral rule.
5. Avoid turning the skill into a rigid template engine.
6. Re-read all eval cases after the change.

A generated PR note should let a competent reviewer understand the intent and changed path in roughly 30 seconds before opening the diff.
