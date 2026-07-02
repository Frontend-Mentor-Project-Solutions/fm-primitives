# Frontend Mentor Primitives

Shared CSS/JS building blocks reused across Frontend Mentor challenge repos
in this org. The goal is to write a pattern once — a reset, a layout
primitive, a form control, a web component — and pull it into any
challenge that needs it, instead of copy-pasting between projects.

No npm registry, no publishing pipeline. Everything is consumed straight
from a tagged GitHub release, either via jsDelivr (CSS) or a git-based
dependency (JS, once that's needed).

---

## What's in here

```
packages/
  reset/
    reset.css                  Base UA-default reset (box-sizing, margins,
                                 text-size-adjust, list roles, img defaults,
                                 form control font inheritance, :target
                                 scroll-margin)
    checkbox-reset.css          (planned) custom checkbox/radio indicator,
                                 --checkbox-* custom property hooks
    checkbox-reset--switch.css  (planned) role="switch" track/thumb modifier
    checkbox-reset--toggle.css  (planned) pressed-button modifier
    radio-reset.css             (planned) companion to checkbox-reset
    button-reset.css            (planned) unstyled button base

  layouts/
    breakout-grid.css           Content column with popout/breakout/
                                 full-width tiers, via named grid lines
    (planned) cluster.css, sidebar.css, cover.css, switcher.css —
    additional Every-Layout-style layout primitives, added as challenges
    call for them

  css-utilities/                (planned) small single-file CSS patterns:
    content-card.css, tag-badge.css, avatar.css, styled-select.css,
    empty-state.css, line-item-table.css, score-display.css,
    game-grid.css, validated-field.css

  components/                   (planned) Shadow DOM web components:
    app-dialog/, nav-drawer/, cart-drawer/, app-tabs/,
    combobox-search/, drag-list/, image-lightbox/,
    toast-notification/, countdown-timer/, progress-ring/,
    vote-counter/, live-preview-pane/, stepper-progress/,
    copy-button/, toggle-button-group/
```

Only `resets/base-reset.css` and `layouts/breakout-grid.css` exist today.
Everything else is added incrementally, the first time a challenge
actually needs it — nothing is built speculatively ahead of use.

---

## Versioning

This repo uses git tags as version numbers (semver: `MAJOR.MINOR.PATCH`).
No `package.json`, no registry account.

- **PATCH** (`v1.0.1`) — bug fix, no change to import paths or behavior
- **MINOR** (`v1.1.0`) — new file/pattern added, nothing existing breaks
- **MAJOR** (`v2.0.0`) — renamed/removed file or folder, or a behavior
  change that would break an existing `@import`

Always pin consuming projects to a specific tag, never to `main` — `main`
can change shape at any time, but a tag is permanent once pushed.

To cut a release:

```bash
git add .
git commit -m "Describe the change"
git tag vX.Y.Z
git push origin main --tags
```

---

## Using this in a project

Replace `vX.Y.Z` below with the actual tag you want to pin to, and check
the repo's tags page for the latest:
`https://github.com/Frontend-Mentor-Project-Solutions/fm-primitives/tags`

### Plain HTML/CSS (no build step)

Import directly from jsDelivr in your main stylesheet, or link it in
`<head>`:

```css
@import url("https://cdn.jsdelivr.net/gh/Frontend-Mentor-Project-Solutions/fm-primitives@vX.Y.Z/packages/reset/reset.css");
@import url("https://cdn.jsdelivr.net/gh/Frontend-Mentor-Project-Solutions/fm-primitives@vX.Y.Z/packages/layouts/breakout-grid.css");
```

or

```html
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/gh/Frontend-Mentor-Project-Solutions/fm-primitives@vX.Y.Z/packages/reset/reset.css"
/>
```

### Framework projects (Vite, Astro, Vue, Angular, SvelteKit, etc.)

Two options, pick whichever suits the build tool:

**A. `@import` in your global stylesheet** — simplest, works anywhere a
network `@import` is acceptable at build time:

```css
/* src/styles/global.css */
@import url("https://cdn.jsdelivr.net/gh/Frontend-Mentor-Project-Solutions/fm-primitives@vX.Y.Z/packages/reset/reset.css");
@import url("https://cdn.jsdelivr.net/gh/Frontend-Mentor-Project-Solutions/fm-primitives@vX.Y.Z/packages/layouts/breakout-grid.css");
```

**B. Download a local copy at project setup** — better if your bundler
doesn't inline network `@import`s the way you want, or you want the file
version-controlled inside the challenge repo itself:

```bash
curl -o src/styles/reset.css \
  https://cdn.jsdelivr.net/gh/Frontend-Mentor-Project-Solutions/fm-primitives@vX.Y.Z/packages/reset/reset.css

curl -o src/styles/breakout-grid.css \
  https://cdn.jsdelivr.net/gh/Frontend-Mentor-Project-Solutions/fm-primitives@vX.Y.Z/packages/layouts/breakout-grid.css
```

Then import the local copy as normal:

```css
@import "./reset.css";
@import "./breakout-grid.css";
```

Re-run the `curl` command with a new tag whenever you deliberately want
to pick up an update — local copies won't change on their own, which is
usually what you want mid-project.

### Web components (once `components/` exists)

Import the module directly wherever custom elements are registered:

```js
import "https://cdn.jsdelivr.net/gh/Frontend-Mentor-Project-Solutions/fm-primitives@vX.Y.Z/packages/components/app-dialog/app-dialog.js";
```

```html
<app-dialog>...</app-dialog>
```

---

## Roadmap

- [ ] `checkbox-reset.css` + `--switch` / `--toggle` modifiers
- [ ] `radio-reset.css`, `button-reset.css`
- [ ] First layout primitive beyond breakout-grid (likely `cluster` or
      `cover`, whichever a challenge needs first)
- [ ] First web component — likely `<app-dialog>` or `<nav-drawer>`,
      based on how many challenges in the pipeline need a modal/overlay
- [ ] Consider GitHub Packages / real npm publishing once a component
      has actual JS dependencies worth version-locking beyond a single
      file import
