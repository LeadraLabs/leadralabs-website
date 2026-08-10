# Editing website copy — a guide for Nova

## What is `content.json`?

`content.json` is a single file in this repository that holds almost all of the words on the Leadra Labs website — homepage headlines and buttons, the About page, the five capability detail pages, pricing, the footer text, and more.

Before this change, changing any wording meant editing raw HTML files, which is risky: it's very easy to accidentally break a tag or delete a quote mark and take down the whole page.

Now, the homepage, the About page, and all five capability pages automatically load their text from `content.json` when someone visits the site. That means you can change wording by editing **only** `content.json` — you never need to open or touch any `.html` file, any CSS, or any JavaScript file again for a copy change.

## Step-by-step: how to edit content.json

1. Go to the repository on GitHub (ask Kathleen for the link if you don't have it).
2. Click on the file named `content.json` in the file list.
3. Click the pencil icon (✏️) in the top-right of the file view — this opens GitHub's built-in editor. (It may be labeled "Edit this file.")
4. Use your browser's find function (Ctrl+F or Cmd+F) to jump to the section you want. The file is organized in the same order as the sections appear on the page, and each section has a clear name, for example:
   - `"nav"` — the top navigation bar
   - `"hero"` — the big headline at the top of the page
   - `"how_it_works"` — the "Grounded in behavioural science" section
   - `"pricing"` — the three pricing cards
   - `"community"` — the "coming soon" community section
   - `"get_access"` — the "Ready to build your leadership identity?" section
   - `"footer"` — the tagline and copyright line at the bottom
   - `"about"` — the entire About page: hero copy, the founder bio, the "How we use AI" section, the "Where we're headed" roadmap, and the closing CTA heading
   - `"capabilities_pages"` — the five capability detail pages (Emotional Regulation, Critical Thinking, Situational Judgement, Change Agility, Influence), each with its own pill label, subtitle, body paragraphs, and "How Leadra supports..." section
5. Find the piece of text you want to change. It will look like this:
   ```
   "headline": "Leadership is built in moments.",
   ```
   The part in quotes **after the colon** is the actual text shown on the site. That's the only part you should change.
6. Carefully replace the text between the quote marks with your new wording. Leave everything else — the part before the colon, the quote marks themselves, and the comma at the end — exactly as it is.
7. Scroll down and click the green **"Commit changes..."** button.
8. Write a short, plain description of what you changed (e.g. "Update hero headline") and click **"Commit changes"** again to confirm.

## The one rule that matters most

**Only ever change text that is between two quote marks (`"..."`).**

Do not delete or add:
- Quote marks (`"`)
- Commas (`,`)
- Curly brackets (`{` `}`)
- Square brackets (`[` `]`)

Even removing a single comma or quote mark can break the entire file, which means the whole website could stop showing its text correctly. If you're ever unsure whether something is "editable text" or "structure," stop and ask Kathleen or Claude Code before saving.

A safe edit looks like changing this:
```
"headline": "Leadership is built in moments.",
```
into this:
```
"headline": "Leadership is built in bold moments.",
```
— only the words between the quotes changed. Everything else (colon, comma, quote marks) stayed exactly the same.

## Editing a paragraph in a list (About page and capability pages)

Some sections — like the About page's hero copy, the founder bio, and each capability page's body paragraphs — are stored as a **list** of paragraphs rather than a single block of text. It looks like this:
```
"hero_paragraphs": [
  "Leadership is shaped in the moments you cannot plan for. The quiet pause...",
  "Leadra is a behavioural development app that supports you in those moments...",
  "Leadership development matters because the demands on leaders are higher than ever...",
  "Leadra was created in Australia for leaders at every stage of their journey..."
],
```
Each paragraph is its own set of quote marks, separated by commas, inside square brackets `[ ]`. To edit one paragraph, only change the text inside its quote marks — leave the square brackets, the commas between paragraphs, and the number of paragraphs exactly as they are. Adding or removing an entire paragraph (not just editing its wording) is a bigger structural change — ask Kathleen or Claude Code for help with that rather than doing it directly.

## What happens after you save

Once you commit your change on GitHub, Cloudflare Pages (the service hosting the site) automatically detects the update and rebuilds the live site. This usually takes **1–2 minutes**.

To check your change went live:
1. Wait a couple of minutes.
2. Visit [leadralabs.com](https://leadralabs.com) in a browser.
3. Do a hard refresh (Ctrl+Shift+R on Windows, Cmd+Shift+R on Mac) to make sure you're not seeing a cached older version.
4. Confirm your new text is showing.

## If something breaks

If you accidentally break the file's structure (for example, delete a quote mark or comma by mistake), the safest sign is: the site loads, but some or all of the text reverts to older wording instead of showing your update. (This is by design — the page always has fallback text built in, so visitors will never see a blank or broken page, but your edit won't show up either.)

If this happens:
1. Don't panic — nothing is permanently lost.
2. Go to `content.json` on GitHub and click **"History"** (or look at the commits list for that file).
3. Find the last version that worked, open it, and either copy the correct content back into the current file, or ask Kathleen or Claude Code to restore it for you. GitHub keeps every past version, so recovery is always possible.

## What's *not* in content.json (on purpose)

A few things are deliberately left out of `content.json` and should not be added there:

- **The five capability names and one-line descriptions shown on the homepage grid** (e.g. "Stay grounded when pressure spikes" under Emotional Regulation) — this short copy has been finalized and is intentionally kept out of the editable file. Note this is different from the full capability detail pages (`capabilities_pages` in content.json), which **are** editable — those are the pages you reach by clicking a capability card.
- **Final pricing figures** where marked — some prices are placeholders during the current testing period and will be updated deliberately by the team when ready, rather than through routine content edits.
- **Page metadata** (the description shown in Google search results and social media link previews) — these live directly in each page's own `.html` file (e.g. `index.html`, `about.html`, or a file in `capabilities/`) because search engines and social platforms can't read `content.json`; changes to these lines need to be made in the relevant HTML file directly, so ask Kathleen or Claude Code for help if these need updating.
- **Links (URLs)** — button and link destinations (where a button takes you when clicked) are not in `content.json`, only the button's visible label text is. Changing a link's destination is a code change, not a content change.

If you're ever unsure whether something belongs in `content.json`, it's always fine to ask.
