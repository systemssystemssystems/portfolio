# Jack Morgan: journalism portfolio

Static site served by GitHub Pages from the `main` branch root. No build step, no dependencies, no framework. `README.md` is the owner-facing guide to editing content; read it too.

This is a separate project from the art site (systemssystemssystems.faith). Do not link the two, share code between them, or reuse that repo.

## Structure

- `index.html`: the whole page: markup, styles and one inline script that renders everything from `window.SITE`. Rarely needs editing.
- `articles.js`: all content, as one `window.SITE = { ... }` object. The comment at the top documents the article fields.
  - `profile`: name, role, statement, intro, bio, facts, contact.
  - `workNote`, `reportsNote`, `earlierNote`: notes shown under section headings.
  - `threads`: running stories (`pfas`, `water-reform`, `data-centres`); a piece joins one with `thread: "<id>"`.
  - `reports`: reports and forums (13).
  - `earlier`: eight Ocki Sustainability pieces from early 2024, each with `full: "pieces/<file>.md"`.
  - `articles`: 212 Environment Analyst pieces, one object per line. 118 have `roundup: true`.
- `pieces/`: full texts fetched by "Read in full". Minimal markdown only: blank line between paragraphs, `## ` subheading, `- ` bullet, `[text](https://link)`. Nothing else is parsed.
- `.nojekyll`: tells Pages to serve files as they are. Keep it.

## How the page behaves

- Topic and type filter chips are built from the `beat` and `type` values in `articles`, ordered by count. There is no separate list of topics to maintain.
- Roundups are hidden from "All work" until "Include weekly roundups" is ticked (94 pieces shown without, 212 with).
- "Selected" shows the first three pieces with `featured: true`.
- "Read in full" fetches its file on first open, so it needs a server; it fails when `index.html` is opened from disk.
- Adding `#add` to the address shows a form that builds an entry to paste into `articles.js`.

## Preview

    python3 -m http.server

Run from this folder, then open http://localhost:8000.

## Publishing

Commit and push to `main`; Pages redeploys in a minute or two. Only host a piece in full if it is free to republish. Environment Analyst pieces behind the paywall get a `summary` instead.

A custom domain is planned, set up the same way as the art site: four A records plus a `www` CNAME, HTTPS enforced. Do not add a `CNAME` file until Jack asks; GitHub creates it when the domain is entered in Settings, Pages.

## Open items

Known and unfinished. Jack will come back to these; do not fix them unprompted.

- "Selected" shows three stand-in pieces (`featured: true`) with no summaries.
- The topic (`beat`) grouping was guessed from headline keywords and has not been reviewed.
- In `pieces/dfe-sustainability-strategy.md`, "is listed here" has no link.
- Months (`when`) and some headlines for the Ocki pieces in `earlier` are unconfirmed.
