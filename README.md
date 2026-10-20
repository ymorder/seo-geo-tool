# SEO/GEO Content Tool — Writer + Checker

A single-file browser tool that bundles an SEO/GEO **writer** workflow and a **content checker** review workflow into one interface. Drop `index.html` into any browser, type the topic + language + market, and start producing a publish-ready article in one shot.

No build step, no backend, no dependencies. State persists in `localStorage`.

## Writer mode — streamlined flow

The writer was designed to start working the moment you enter the basics.

1. **Intake** — three required fields: subject, language, market. Advanced inputs (audience, brand, length, content type, notes) are collapsed by default.
2. **Start** → drops you into the working canvas.
3. **Generate & Parse** at the top:
   - **📋 Copy full prompt** generates a comprehensive prompt that asks the AI to do the research, writing, meta tags and image brief in one shot.
   - **📥 Paste response** lets you paste the AI's reply back. **⤵ Parse & fill fields** distributes the response into the right fields automatically using `=== SECTION ===` delimiters.
4. **Outputs sit on the canvas as editable panels**, in order of priority:
   - 📝 **Article** — full publish-ready body (markdown)
   - 🎯 **Meta Tags** — 3 title options · 3 description options · 1 URL slug · with character counters
   - 🖼️ **Featured Image** — style · mood · prompt · alt text · filename
5. **▶ Advanced sections (optional)** — research · GEO prompts · outline · fact check · audits. Open only if you asked the AI for them.
6. **📦 Final Bundle** — auto-built markdown that stitches article + meta + image + audits. Copy or download `.md`.
7. **Hand off to Checker →** — preloads the bundle as the text-to-check in Checker mode.

The whole working view is a single scrollable canvas — no stage navigation, no manual paste-into-each-field.

## Checker mode

Paste any text and walk through the priority-driven review:

1. **Assumptions** — only if no task card was attached
2. **Overall Assessment** — 2–3 sentences, publication verdict
3. **Strengths** — what already works
4. **Required Fixes** — structured builder with priority tags P1–P5, original vs. suggested phrasing, and reason per fix. Consolidated markdown auto-rebuilds.
5. **Suggestions** — optional polish
6. **To Verify** — facts that can't be confirmed
7. **Edited Version** — publish-ready rewrite, only if requested

## Required response format (for the parser)

The Parse & fill button expects the AI response in this format:

```
=== ARTICLE ===
[full markdown article]

=== ASSUMPTIONS ===
[bullet list]

=== META TITLES ===
1. [title A]
2. [title B]
3. [title C — recommended]

=== META DESCRIPTIONS ===
1. [desc A]
2. [desc B]
3. [desc C — recommended]

=== SLUG ===
[hyphenated-slug]

=== IMAGE STYLE ===
[Realistic editorial photography | Modern abstract conceptual art | ...]

=== IMAGE MOOD ===
[mood / lighting]

=== IMAGE PROMPT ===
[16:9 · no text · no logos]

=== IMAGE ALT ===
[alt text including primary keyword]

=== IMAGE FILENAME ===
[hyphenated-filename.jpg]

=== FACT CHECK ===
[markdown table + source list]

=== AUDITS ===
[uniqueness · math · humanization]
```

The comprehensive prompt the **Copy full prompt** button generates asks for this format.

## Other features

- 🌓 Light / dark theme toggle (persists)
- ⬇ Export entire project to JSON · ⬆ Import to restore
- 🗑 Reset with confirmation modal
- Per-section copy buttons
- Auto-save on every keystroke
- RTL language support (Hebrew, Arabic) with character-set-aware counters
- "Detect language" button in the checker (heuristic for Hebrew / Arabic / Cyrillic)

## Running it

Open `index.html` in any modern browser. No server, no install.

## Tech notes

- Single file, ~72 KB, no external requests.
- Vanilla JS, no framework, no build step.
- Theme is `data-theme` on `<html>`; everything else is CSS variables.
- State shape is in the `state` object near the top of the `<script>` block — easy to inspect or extend.

## License

[MIT](./LICENSE)