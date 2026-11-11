# Jack Morgan: journalism portfolio

Static site served by GitHub Pages from the `main` branch root. No build step, no dependencies, no framework. `README.md` is the owner-facing guide to editing content; read it too.

This is a separate project from the art site (systemssystemssystems.faith). Do not link the two, share code between them, or reuse that repo.

## Structure

- `index.html`: the whole page: markup, styles and one inline script that renders everything from `window.SITE`. Rarely needs editing.
- `articles.js`: all content, as one `window.SITE = { ... }` object. The comment at the top documents the article fields.
  - `profile`: name, role, statement, intro, bio, facts, contact.
  - `workNote`, `reportsNote`, `earlierNote`: notes shown under section headings.
  - `threads`: the "Subjects followed over time" section, called running stories in the code (`pfas`, `water-reform`, `data-centres`, `consulting-market`, `reporting`, `brownfield`); a piece joins one with `thread: "<id>"`.
  - `reports`: 15 entries: market assessments, survey reports, insight reports and summits. Business Leaders' Forums and Leadership Network roundtables were removed at Jack's request; do not add them back. Roles follow Jack's outline of what he did ("led" or "contributed").
  - `earlier`: eight Ocki Sustainability pieces from early 2024, each with `full: "pieces/<file>.md"`.
  - `articles`: 212 Environment Analyst pieces, one object per line. 118 have `roundup: true`. `free: true` marks pieces outside the paywall (see "Free to read" below).
- `pieces/`: full texts fetched by "Read in full". Minimal markdown only: blank line between paragraphs, `## ` subheading, `- ` bullet, `[text](https://link)`. Nothing else is parsed.
- `.nojekyll`: tells Pages to serve files as they are. Keep it.

## How the page behaves

- Topic chips and the type dropdown are built from the `beat` and `type` values in `articles`, ordered by count. There is no separate list of topics to maintain.
- Roundups are hidden from Work until "Include weekly roundups" is ticked (94 pieces without, 212 with).
- Long lists are cut short: Work shows the latest 8 until "Show all" is pressed or any filter is used; running stories show 4 (newest first), Reports 6, Earlier work 4, each with a "Show all" link. The limits are the constants `LATEST`, `THREAD_MAX`, `REPORT_MAX`, `EARLIER_MAX` at the top of the script.
- "Free to read only" narrows Work to pieces with `free: true` and also pulls in the `earlier` pieces that have a `full` text (treated as free in code, sorted by their `when` month).
- Running stories sit in one row that scrolls sideways, with arrow buttons in the section heading that appear only when the row overflows.
- Dates show as month and year only (`fmt` in the script). There is no piece count in the Work heading and no status text while the list is cut to the latest 8; both were removed at Jack's request. `workNote` and `reportsNote` are empty strings, which hides those notes.
- The region dropdown (UK, EU, US, Global) matches UK and Global on `edition` (BRN counts as UK) and EU and US on the optional `region` field.
- Section titles (h2) are deliberately much larger and bolder than the sub-headings beneath them (1.625rem/700 against 1.0625rem/600), with an ink-coloured rule above each section; Jack found them hard to tell apart.
- Menu: above 40rem the whole masthead (name plus links) is sticky. On phones the name scrolls away and only the link row stays pinned, as one line that swipes sideways (`.mast{display:contents}` makes this work). The link for the section being read is bold and underlined (`aria-current`, set by the scroll handler near the end of the script). Built after feedback from mobile readers.
- Each section opens with a 4px black bar and generous space below the previous one, also from that feedback.
- "Selected" shows the first four pieces with `featured: true`, four across on desktop, two by two on tablets, stacked on phones.
- "Read in full" fetches its file on first open, so it needs a server; it fails when `index.html` is opened from disk.
- Adding `#add` to the address shows a form that builds an entry to paste into `articles.js`.

## Free to read

`free: true` was set in November 2026 by fetching every article `url` and reading the page's schema.org `"isAccessibleForFree"` value (paywalled pages also contain "to continue reading"). The `also` link was not used. Environment Analyst rate-limits: more than a few requests in quick succession returns 429, so check one at a time with a pause of a few seconds. Access can change over time, so re-check before relying on the flags.

## Design

One typeface throughout: the device's system sans, with no web fonts loaded. Headlines differ by weight and size only. White background, light mode only (no dark theme), at Jack's request. The opening is deliberately plain, a bold line and a paragraph with no oversized slogan. The Work button says "Show more pieces" with no total, because the list may be incomplete and Jack does not want an exact count implied there. No monospace, no uppercase tracked labels, no decorative reference codes; these were removed on purpose to make the page plainer. Each row has one quiet metadata line (type, topic, edition, access). The outlet is left off rows when it is the most common one (Environment Analyst). Jack wants it to stay simple and not look corporate; keep changes restrained.

## Preview

    python3 -m http.server

Run from this folder, then open http://localhost:8000.

## Publishing

Commit and push to `main`; Pages redeploys in a minute or two. Only host a piece in full if it is free to republish. Environment Analyst pieces behind the paywall get a `summary` instead.

The site is served at jackmorgan.site (registered at Namecheap, November 2026; four A records to GitHub Pages plus a `www` CNAME to `systemssystemssystems.github.io`). The `CNAME` file in the repo root holds the domain; keep it. The old address, systemssystemssystems.faith/portfolio/, redirects here.

## Open items

Known and unfinished. Jack will come back to these; do not fix them unprompted.

- "Selected" shows four pieces (three stand-ins plus the CSRD piece Jack chose), all (`featured: true`) with no summaries.
- The topic (`beat`) grouping was guessed from headline keywords and has not been reviewed.
- The `consulting-market`, `reporting` and `brownfield` running stories were filled by putting every non-roundup piece with the matching topic into them, and their titles and summaries are drafts. Jack has not reviewed either.
- `region: "EU"` / `"US"` was assigned by matching keywords in headlines and standfirsts (EU, Europe, CSRD, Efrag, Omnibus; US, EPA, NEPA, America, Canada, federal, Trump) and has not been reviewed.
- About is cut back to one paragraph and two facts (Education, Also) for now; Jack removed the rest pending a rewrite.
- In `reports`, three dates are placeholders to be confirmed: UK Market Assessment Nov 2025 (day), UK Early Careers report 2025 (shown as "2025") and Future of Sustainability 2026 (shown as "2026"). "Europe in Focus" is Jack's name for the report; Environment Analyst's page calls it "Focus on Europe".
- The About wording is to be reworked using phrasing from Jack's LinkedIn profile (linkedin.com/in/jackmorgan827). The profile sits behind a sign-in wall, so this needs Jack to sign in or paste the text.
- In `pieces/dfe-sustainability-strategy.md`, "is listed here" has no link.
- Months (`when`) and some headlines for the Ocki pieces in `earlier` are unconfirmed.
