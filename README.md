# SEO/GEO Content Tool — Writer + Checker

A single-file browser tool that bundles an SEO/GEO **writer** workflow and a **content checker** review workflow into one interface. Drop `index.html` into any browser, type the topic + language + market, and start producing a publish-ready article in one shot.

No build step, no backend, no dependencies. State persists in `localStorage`.

## Writer mode — 3-step wizard

The writer was designed to start working the moment you enter the basics.

1. **Intake** — three required fields: subject, language, market. Advanced inputs (audience, brand, length, content type, notes) are collapsed by default.
2. **Click Start →** drops you into the working canvas.
3. **Generate the article** — three numbered steps in one panel:
   - **① Get the prompt** — `📋 Copy full prompt` (paste into any AI) **OR** `✨ Generate with AI` (runs the prompt directly here if you set an API key in Settings)
   - **② Paste the response** — single textarea, drafts are saved automatically
   - **③ Fill the fields** — `⤵ Parse & fill fields` distributes the response into the article, meta, image and advanced panels using `=== SECTION ===` delimiters
4. **Outputs sit on the canvas as editable panels**, in priority order:
   - 📝 **Article** — full publish-ready body (markdown)
   - 🎯 **Meta Tags** — 3 title options · 3 description options · 1 URL slug · with character counters
   - 🖼️ **Featured Image** — style · mood · prompt · alt text · filename
5. **▶ Advanced sections (optional)** — research · GEO prompts · outline · fact check · audits.
6. **📦 Final Bundle** — auto-built markdown that stitches article + meta + image + audits. Copy or download `.md`.
7. **Hand off to Checker →** — preloads the bundle as the text-to-check in Checker mode.

## Language support

The mega prompt injects strict language-specific rules when you pick a language:

- **Hebrew / Arabic** — RTL text direction, character purity rules, banned Hebrew/Arabic filler phrases (לצלול, הסיבה לכך פשוטה, לסיכום, בעידן המודרני, etc.), keyboard layout corruption warnings.
- **Russian / Cyrillic** — pure Cyrillic body, no Latin mixing.
- **English / Western** — strict orthography, em-dash ban, banned AI phrases.

The prompt also explicitly tells the AI to write the meta title and description in the same language as the body (with URL slug staying English/transliterated for SEO).

## Generate with AI

You can run the AI step directly in the tool without copy-pasting anywhere. Click **✨ Generate with AI** in the Generate panel — the tool calls the configured provider, parses the response, and fills every field.

**Default provider: 🌱 Pollinations.ai** — free public API, no key required, works out of the box. Models: `openai-fast`, `openai-large`, `mistral`, `llama`, `qwen-coder`.

**Free / local alternatives** (via ⚙ Settings):

- **🦙 Ollama (local)** — runs on your hardware, no API key. Default URL `http://localhost:11434/v1`. Models: `llama3.2`, `mistral`, `qwen2.5`, `phi3`, `gemma2`. Requires [Ollama](https://ollama.com) installed and a model pulled.
- **OpenAI** (BYOK): `gpt-4o-mini` (cheap, fast), `gpt-4o`, `gpt-4-turbo`, `o1-mini`
- **Anthropic** (BYOK): `claude-3-5-sonnet-latest`, `claude-3-5-haiku-latest`
- **Google Gemini** (BYOK): `gemini-1.5-flash`, `gemini-1.5-pro`, `gemini-2.0-flash-exp`

API keys are stored only in your browser's localStorage and sent directly to the provider — never through any intermediate server.

If you don't want to use BYOK, the **Copy full prompt** workflow still works exactly as before.

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
[full markdown article in the target language]

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
[hyphenated-slug — ASCII / transliteration]

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
- RTL UI handling for Hebrew / Arabic (working canvas is LTR but prompt respects RTL body)

## Running it

Open `index.html` in any modern browser. No server, no install.

## Tech notes

- Single file, ~80 KB, no external requests.
- Vanilla JS, no framework, no build step.
- Theme is `data-theme` on `<html>`; everything else is CSS variables.
- BYOK uses `fetch()` directly to `api.openai.com` or `api.anthropic.com` from your browser.
- State shape is in the `state` object near the top of the `<script>` block — easy to inspect or extend.

## License

[MIT](./LICENSE)