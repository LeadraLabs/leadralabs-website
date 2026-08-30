# Leadra Labs marketing site

Static HTML/CSS/vanilla-JS site, no build step, deployed via Cloudflare Pages. No framework, no bundler, no package.json.

## Structure

- `index.html` — homepage
- `about.html` — About page
- `capabilities/*.html` — five capability detail pages (Emotional Regulation, Critical Thinking, Situational Judgement, Change Agility, Influence)
- `assets/style.css` — single shared stylesheet, flat class names, CSS custom properties for the navy/gold/sand palette (`--navy`, `--gold`, `--sand`, etc.)
- `assets/icons/` — capability icons; `assets/logo.png` — the real Leadra logo
- `content.json` — most page copy, loaded at runtime and overlaid onto `[data-content]` / `[data-content-list]` / `[data-field]` elements (see `CONTENT_GUIDE.md` for how Nova edits this without touching HTML)
- `*.pdf` in repo root — the real hosted legal documents (Privacy Policy, Terms of Use, User Safety Statement), linked from every page's footer

## content.json overlay mechanics

Each HTML page has a small inline script (bottom of `<body>`) that fetches `content.json` and walks `[data-content]` (single string), `[data-content-list]` (array, clones `container.children[0]` as the template), and nested `[data-field]` / `[data-field-list]` inside card objects. If `content.json` is missing/unreachable, the hardcoded HTML text already present is shown as a fallback — so hardcoded fallback text must always be kept in sync with content.json.

**Known bug in the shared overlay script** (`populateList()`/`applyFieldsToCard()`, duplicated per page): the array-templating logic assumes the list container starts with **exactly one** child element to use as the clone template. If a container has more than one static child, cloning silently drops the wrong item when trimming excess nodes at the end, so later items can end up showing earlier items' values. Also, `[data-field="text"]` must be placed on a *child* of the list-item element, not the list-item element itself, because the fill callback does `li.querySelector('[data-field="text"]')` which never matches `li` itself. Any new `data-content-list` / `data-field-list` block must follow both rules: single-child template, `data-field="text"` nested one level in.

## About page

Restructured 2026-08-30 to match a new Claude Design export: "Who Leadra is for" (5 career-stage cards) → "Why learning inside the work is the part that sticks" (behavioural-science rationale) → "Meet the founder" (Nova's bio) → "How we use AI" (kept from the previous version) → closing CTA. The old "Where we're headed" roadmap section was dropped.
