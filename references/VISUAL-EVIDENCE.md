# Visual evidence

Before/after screenshots are the strongest evidence a visual change can carry, and the easiest to fake. This file defines how to capture them honestly.

## When captures are required

Capture a before/after pair when the change affects anything a user can look at:

- layout, spacing, color, typography, component states
- interaction: click, hover, focus, keyboard, drag
- navigation, routing, URL changes
- loading, empty, error, and disabled states
- auth and sign-in flows
- anything you would otherwise describe with the word "now shows"

**Rendered output counts.** The question is never "is this a docs change" — it is "can the change be seen". Capture it when the change alters:

- a README, changelog, or any Markdown as it renders
- a docs site, MDX page, or static site
- Markdown mechanics: fences, tables, task lists, diagrams, code blocks
- CSS, themes, typography, spacing tokens
- a generated page, dashboard, or report

A change whose source file is `.md` is still a visual change if someone looks at the result.

Do not capture for backend-only, refactor-only, dependency, generated-code, or internal infrastructure changes. A screenshot of a passing terminal is not visual evidence of a backend change.

## Capture sequence

Order matters. The BEFORE image only exists before the code changes.

1. Reproduce the old behavior — base branch, `git stash` on the current change, previous build, deployed version, or a second checkout.
2. Capture BEFORE.
3. Apply the change.
4. Reproduce the identical scenario: same route, same inputs, same data, same account.
5. Capture AFTER.

If this skill is loaded after the change is already in place, recover the old state instead of skipping it: stash the change, check out the base commit, or run the previous build. If none of that is possible, say the BEFORE image is unavailable. Do not draw one, do not describe one as if it existed, and do not reuse an unrelated screenshot.

## Capturing rendered output

Same rule, different mechanism: the renderer is the app.

1. Render the base revision and the branch revision from the same source region.
2. Use the real product wherever you can — the deployed docs site, the running app, GitHub's own rendering.
3. Only if the real renderer genuinely cannot be driven — a site behind auth, a build you cannot run — fall back to a renderer that closely reproduces it: the product's markdown flavour plus its own stylesheet.
4. Hold viewport width, theme, and the cropped region identical between the pair. Same origin, same width, same theme; only the content changes.

Before concluding that a renderer failed, check for **cross-origin iframes**. GitHub draws Mermaid inside a `viewscreen.githubusercontent.com` frame, so querying the main document finds no diagram and looks like a broken renderer when the diagram is fine. Query every frame, not just the top document.

State a limitation only once you have confirmed it. A limitation you assumed is a false claim in the note.

## Framing

Hold everything constant between the pair except the change:

- same viewport size and device scale
- same zoom, same theme, same font settings
- same scroll position and surrounding content
- same app state and same synthetic data

Then crop tightly around the region that changed. A 40px state change does not need a 1440px screenshot, and the reviewer should not have to hunt for the difference.

For small changes, an annotated crop is more useful than a full page. Keep annotation minimal: one arrow or box, not a labelled diagram.

## Storage

Write captures to a hidden, gitignored directory in the working repository:

```text
.pr-notes/
  screenshots/
    before-<short-name>.png
    after-<short-name>.png
```

Use one short kebab-case name per scenario, and add pairs rather than overwriting: `before-empty-state.png` / `after-empty-state.png`.

Ensure the ignore entry exists unless the user explicitly wants the images committed:

```gitignore
/.pr-notes/
```

Add the exact root entry. Do not use a bare `.pr-notes` or a broad pattern that could hide unrelated files.

Never leave captures staged in the diff.

## Putting images in the PR

The local directory stays hidden and untracked. When the note needs hosted URLs, upload or attach the selected images through the normal PR workflow, then reference the result:

```md
### Before / after

| Before | After |
|---|---|
| ![before](<uploaded-url>) | ![after](<uploaded-url>) |
```

If there is no upload path, say where the local files are and let the author attach them. Do not invent a URL.

## Images replace prose

When a capture shows the change, the capture is the explanation. Delete the sentence that describes it. A note that narrates its own evidence takes longer to read than the change deserves.

## Reporting

State what the pair shows in one line, and name what it does not cover:

> Before/after captured at 1440×900, light theme, same seeded account. The timeout state is not covered.

A pair of screenshots proves the visual delta on the captured path only. It does not prove the interaction behind it, and it is not a substitute for tests.
