# Hugo with a hand-rolled theme, optimised for long-term resilience

The blog uses **Hugo** (single-binary Go SSG) with a theme **built from scratch** — a handful of templates and ~100 lines of CSS — rather than Astro/Next or a vendored Hugo theme. The author's priority order is **long-term resilience first, ease of publishing second**; design flexibility is explicitly deprioritised. Hugo's no-`node_modules` profile means a build today still works in years with no maintenance; an in-repo theme has no upstream that can rot.

## Considered options

- **Astro.** Better DX for a React-fluent author, beautiful reading-first theme ecosystem (`astro-paper`, `astro-nano`). Rejected because `node_modules` dependency rot is a real failure mode for a project the author will touch sparingly — a working build today may not build cleanly in three years without proactive maintenance.
- **Vendored Hugo theme.** Copy a minimal theme (`hugo-bearblog`, `hugo-theme-paper`) into the repo. Rejected because the reading-first design surface is small enough (~100 lines of CSS, ~5 templates) that the savings are modest, and a hand-written theme means future-you can read every line and remember why it's there.
- **Hugo theme as submodule or Hugo module.** Rejected outright — upstream changes can break the build silently, which is the exact failure mode resilience priorities are meant to prevent.

## Consequence

The repo is fully self-contained. There is intentionally no theme dependency to track, update, or audit. Design changes happen by editing CSS and templates in this repo, not by upgrading a third-party package.
