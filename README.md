# SEO/GEO Content Tool — Writer + Checker

A single-file browser tool that bundles an SEO/GEO **writer** workflow and a **content checker** review workflow into one interface. Drop `index.html` into any browser, fill in a topic, work through the nine writing stages, then hand the bundle off to the checker for fact-level review.

No build step, no backend, no dependencies. State persists in `localStorage`.

## What's inside

### Writer mode (9 stages)

The writer follows a fixed pipeline so each article ships with every SEO/GEO asset:

| Stage | Output |
| --- | --- |
| Intake | Topic, language, market, audience, brand, word count, content type |
| 1 | Competitor research · keyword map · content gaps |
| 2 | GEO prompts (10–15) · quote-ready answers for AI search |
| 3 | Outline · H1 with primary keyword · H2/H3 · FAQ |
| 4 | Article body (markdown, live word counter) |
| 5 | Meta title × 3, meta description × 3, URL slug |
| 6 | Featured image prompt (16:9, no text/logos) · alt · filename |
| 7 | Fact check table · clickable source list |
| 8 | Uniqueness audit · math/empirical audit |
| 9 | Humanization · AI-pattern scan · tone check |
| ★ Final Bundle | Everything stitched into one publish-ready markdown |

Each stage has a status pill (Pending → In progress → Done). Stages flip to "In progress" automatically once you start typing.

### Checker mode

Paste any text and walk through the review in this order (priority-driven):

1. Assumptions
2. Overall assessment (2–3 sentences)
3. Strengths
4. **Required fixes** — structured builder with priority tags P1–P5, original vs. suggested phrasing, and the reason for each fix
5. Suggestions for improvement
6. Items to verify
7. Edited version (publish-ready rewrite, only if requested)

The "Required fixes" section auto-rebuilds the consolidated markdown as you add or edit fixes, so you can copy one clean block downstream.

## Writer → Checker handoff

When the writer finishes stage 9, the **Final Bundle** stitches the article, meta package, image brief, fact-check table and audits into one markdown block. Clicking **Hand off to Checker →** confirms in a modal and preloads the bundle as the text-to-check in Checker mode. The intake language and audience are forwarded so the checker can use them as defaults.

## Other features

- 🌓 Light / dark theme toggle (persists)
- ⬇ Export the entire project to JSON · ⬆ Import to restore
- 🗑 Reset with confirmation modal
- Per-section copy buttons
- Auto-save on every keystroke
- RTL language support (Hebrew, Arabic) with character-set-aware counters
- "Detect language" button in the checker (heuristic for Hebrew / Arabic / Cyrillic)

## Running it

Just open `index.html` in any modern browser. No server, no install.

For a tidy workflow:

1. Open the file once — it creates a localStorage slot.
2. Fill the intake, work the writer.
4. Hand off to checker, walk the review.
5. Use the per-section Copy buttons or the **Copy full review** / **Download .md** actions to ship.

## Tech notes

- Single file, ~90 KB, no external requests.
- Vanilla JS, no framework, no build step.
- Theme is `data-theme` on `<html>`; everything else is CSS variables.
- State shape is in the `state` object near the top of the `<script>` block — easy to inspect or extend.

## License

[MIT](./LICENSE)