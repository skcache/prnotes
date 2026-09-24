# PR Notes

**PR descriptions that explain the change before the reviewer opens the diff.**

PR Notes is an Agent Skill for writing concise, review-ready pull request descriptions.

It focuses on five things:

| | |
|---|---|
| **Change** | what was wrong and what happens now |
| **Before / after** | visual or measurable evidence |
| **Flow** | a small diagram when the changed path is non-obvious |
| **Implementation** | only the details that matter for correctness |
| **Verification** | checks mapped to the changed behavior and likely regressions |

```mermaid
flowchart LR
    A[Behavior delta] --> B[Before / after]
    B --> C{Flow unclear?}
    C -- yes --> D[Small diagram]
    C -- no --> E[Implementation]
    D --> E
    E --> F[Verification]
```

## Example

```md
## What changed

Clicking an MCP server row that required sign-in disabled the server.
Row clicks now start sign-in while the switch still controls enabled state.

### Before / after

| Before | After |
|---|---|
| Row click turns the server off | Row click opens sign-in and keeps it enabled |

### Flow

```mermaid
flowchart LR
    A[Row click] --> B{Needs auth?}
    B -- yes --> C[Start OAuth]
    B -- no --> D[Normal toggle]
```

### Implementation

- Auth-required rows remain enabled while disconnected.
- Direct switch clicks keep the existing toggle behavior.
- Non-auth rows are unchanged.

### Verification

- [x] Auth-required row click starts sign-in.
- [x] Direct switch click still toggles enabled state.
- [x] Non-auth rows behave as before.
```

## Use

Clone the repository and give your agent access to `SKILL.md`.

```bash
git clone https://github.com/skcache/prnotes.git
```

For clients that support the Agent Skills format, place this folder in the client's skills directory and invoke **PR Notes** when writing or rewriting a pull request description.

The skill is intentionally adaptive. Tiny fixes do not get decorative diagrams. Refactors do not get fake before/after sections. Performance changes use measured deltas. Missing evidence stays missing.

## Structure

```text
prnotes/
├── SKILL.md
├── AGENTS.md
├── README.md
├── LICENSE
├── examples/
├── evals/
├── references/
└── templates/
```

## Inspiration

Inspired by a public PR-writing example shared by [Luke Parker](https://x.com/LukeParkerDev), especially the combination of concise behavior description, before/after evidence, and a compact control-flow diagram.

PR Notes generalizes that presentation pattern into a reusable Agent Skill.

## License

MIT
