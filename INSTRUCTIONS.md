# EN + ಕನ್ನಡ Reader — Blogspot / GitHub / Cloudflare

```
reader.html                 ← the app (single file, no libraries)
data/index.json             ← 1218 messages (date, title, slug, part, kn preview)
data/parts/part-001…102.json← 12 messages each, EN + KN (~2.8 MB)
```

Reader fetches **one part per message** — fast on mobile. Split view = same part, no extra request.

---

## 1. GitHub (primary)

1. New **public** repo, e.g. `branham-en-kn`.
2. Upload `reader.html` + the `data` folder (drag & drop, keep structure).
3. CDN URL for the data:
   `https://cdn.jsdelivr.net/gh/<USER>/branham-en-kn@main/`
   Test: open `…/data/index.json`, JSON must show.

## 2. Cloudflare Pages (fallback)

Workers & Pages → Create → Pages → **Upload assets** → same folder → `https://<project>.pages.dev/`.
Change one line in `reader.html`:
```js
const DATA_BASE = "https://<project>.pages.dev/";
```

## 3. Blogspot — 3 ways

**A. iframe (safest, 1 line)** — Pages → New page → HTML view:
```html
<iframe src="https://<USER>.github.io/branham-en-kn/reader.html"
        style="width:100%;height:100vh;border:0" loading="lazy"></iframe>
```
(Enable GitHub Pages: Settings → Pages → main / root.)

**B. Native paste** — copy `<style>`, the body markup, and the `<script>` from `reader.html` into a
Blogger Page (HTML view) and set `DATA_BASE` to your jsDelivr URL.

**C. Theme gadget** — Blogger → Layout → Add HTML/JavaScript gadget → same paste. Good for a sidebar.

Deep links: `#/63-0730` (message), `#/63-0730/12` (paragraph 12).

## 4. UI map

| Where | Icon | What |
|---|---|---|
| Dock | 🌙 | dark / light |
| Dock | ▯ | split view on/off (EN + KN) |
| Dock | 🔍 | search (list search, or full-message focus) |
| Dock | A/ಕ | cycle EN + KN → ಕನ್ನಡ → English |
| Dock | sliders | menu: language, font size (A− … A++), background, text colour, word search in message, jump to paragraph, prev/next |
| Bottom sheet | — | all settings save per device (localStorage) |

## 5. JSON vs SQLite — why JSON here

| | Split JSON (this) | SQLite (WASM) |
|---|---|---|
| First message visible | ~2.8 MB fetch | whole DB (~90–250 MB) downloaded first |
| Init cost on mobile | none | 1.2–1.6 MB engine + decompress |
| CDN / browser caching | per-message ✅ | all-or-nothing |
| Hosting | any static host ✅ | needs headers + COOP/COEP for some builds |
| Full-text across all | build index (optional) | native FTS5 ✅ |

So: **JSON for reading, SQLite only if you later want instant full-corpus search offline.**
If you want that, I can export an FTS5 `.db` plus a search box that downloads it only once.

## 6. Updating

Re-run the split script → upload changed part files. jsDelivr caches ~12 h; use `@latest` or `?v=2`.
