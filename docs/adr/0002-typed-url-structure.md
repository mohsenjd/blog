# Typed URL structure: `/posts/{slug}/` and `/til/{slug}/`

Posts live at `/posts/{slug}/`. Future **TIL**s will live at `/til/{slug}/`. The `slug` is committed in front matter (not derived from filename), so renaming files cannot break URLs. **Date is deliberately absent from the URL** so that posts updated long after publication don't carry a stale-looking date in their canonical link.

## Considered options

- **Flat `/{slug}/`.** Used by Dan Luu, Josh Comeau, Tom MacWright. Shortest and most timeless. Rejected because it forces *all* content types into one shared slug namespace alongside `/about/`, `/feed.xml`, etc., and a future TIL at `/til/some-thing/` would feel asymmetric/second-class next to flat posts. Typed-everywhere is cleaner than flat-then-typed.
- **Dated `/YYYY/MM/{slug}/`.** Traditional blog style (Simon Willison). Rejected because it ties a post to its first publication date in the URL — and posts here are treated as **living artefacts** that may be revised in place. A 2024 URL serving 2027-updated content is weird.
- **Year-only `/YYYY/{slug}/`.** Same date-in-URL objection as above, in milder form.

## Consequence

The slug is forever. Once a post is published, its slug must not change — even if the title does. To support corrections, the workflow is: keep the slug, update title and content freely.
