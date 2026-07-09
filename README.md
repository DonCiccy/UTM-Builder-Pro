# UTM Builder Pro

Build standardized UTM tracking URLs, then audit existing campaigns for naming inconsistencies — in one tool.

**[→ Live demo](https://donciccy.github.io/UTM-Builder-Pro)**

---

## What it does

Marketers build UTM links by hand or half-remember their own naming conventions, so "Meta", "meta" and "facebook" end up as three different sources in the same GA4 property. UTM Builder Pro fixes both ends of that problem: the **Build** tab generates clean, correctly-formatted tracking URLs from a simple form (with A/B variant support and optional Bitly shortening), while the **Audit** tab scans a CSV export — or your own activity log — and clusters inconsistent source, medium and campaign values so you can fix them before they wreck your attribution.

Everything runs client-side. No signup, no server, no data leaves your browser.

## Features

| Feature | Note |
|---------|------|
| UTM link builder | Source, medium, campaign, content and term fields with A/B variant generation (comma-separated content/term produce every combination) |
| Saved presets | Save a source/medium/campaign combination by name and reapply it in one click |
| Activity log | Every generated link is saved locally, searchable, exportable to CSV |
| Optional Bitly shortening | Paste your own Bitly token (stored locally only) to auto-shorten generated links |
| Consistency audit | Upload a CSV (raw URLs or a GA4 Source/Medium export) and get unique values clustered by similarity |
| Built-in synonym dictionary | Recognizes common source/medium synonyms (meta/facebook/fb/ig/instagram, google/adwords/gads, email/newsletter, organic/seo/search) |
| Audit your own log | Skip the CSV — audit the links you've already generated with one click |
| Normalized CSV export | Download a fix-list mapping every inconsistent value to its suggested canonical form |

## How to use

**Build**
1. Enter your destination URL and pick source, medium and campaign
2. Optionally add comma-separated content/term variants for A/B testing
3. Generate — links are added to your Activity Log automatically
4. Save recurring setups as presets for one-click reuse next time

**Audit**
1. Upload a CSV (a plain list of URLs, or a GA4 Source/Medium export) — or click "Audit my Activity Log"
2. Review the clusters: 🔴 Critical means genuinely different-looking values that mean the same channel (e.g. "newsletter" vs "mail"); 🟡 Warning covers case or spelling variants
3. Export the normalized CSV as a fix-list for your tracking setup

## Technical approach

Consistency detection runs in three passes: an exact-match pass against a built-in synonym dictionary (catches semantically identical but textually different values like "fb" → "Meta"), a case/whitespace-normalization pass, and a light Levenshtein-distance pass (edit distance ≤1, length >3) to catch likely typos without over-clustering genuinely distinct values. Each cluster is scored Critical or Warning depending on how it was matched, then mapped to a suggested canonical value.

The CSV parser (PapaParse) accepts either a column of full URLs — parsed client-side with the native `URL` API to extract `utm_*` params — or direct Source/Medium/Campaign columns as GA4 exports typically use, and combines both if present.

## Local development

Open `index.html` in any browser. No installation, no build step.

## License

MIT — use it freely, credits appreciated.
