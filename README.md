# Jack Morgan: journalism portfolio

A static site: no build step, no dependencies. GitHub Pages serves the files as they are.

## Files

- `index.html`: the page, its styles and its script. You rarely need to touch it.
- `articles.js`: all the content. This is the file you edit.
- `pieces/`: full texts shown under "Read in full", one text file per piece.

## Add a piece

1. Open the live site with `#add` on the end of the address. A form appears at the bottom of the page.
2. Fill it in and press "Copy entry".
3. Open `articles.js`, paste the entry at the top of the `articles` list, and save.
4. Commit and push. The site updates in a minute or two.

Or copy an existing line in `articles.js` and change the values. The comment at the top of that file explains each field.

## Other changes, all in articles.js

- **Selected:** add `featured: true` to up to three pieces.
- **Summary for a paywalled piece:** add `summary: ["First paragraph.", "Second paragraph."]`.
- **Running stories:** give a piece `thread: "pfas"` (or another id from the `threads` list).
- **Reports and forums:** add a line to `reports`.
- **Bio, headline line, contact details:** the `profile` block at the top.

## Host a piece in full

1. Save the text as `pieces/your-file-name.md`: a blank line between paragraphs, `## ` for a subheading, `- ` for a bullet, `[text](https://link)` for a link.
2. Add `full: "pieces/your-file-name.md"` to its entry, and optionally `fullNote: "Originally published by ..."`.

Only do this for work that is free to republish. Environment Analyst pieces behind the paywall get a summary instead.

## Preview before pushing

From this folder run `python3 -m http.server` and open http://localhost:8000. Opening `index.html` directly also works, except that "Read in full" needs the local server.

## Custom domain

In the repository go to Settings, then Pages, and enter the domain under "Custom domain". GitHub adds a `CNAME` file for you. At the registrar, add the same four A records and `www` CNAME used for the art site.
