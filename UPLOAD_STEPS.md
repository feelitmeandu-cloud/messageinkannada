# Upload steps (repo: feelitmeandu-cloud/messageinkannada)

## What you get
```
reader.html            ← app + FULL LIST of all 1218 messages embedded (works instantly, no index fetch)
messages-list.html     ← plain list page (all 1218, search box) if you want a simple index page
data/index.json.gz     ← optional richer index (Kannada previews for search)
data/parts/*.json.gz   ← 87 parts, ~0.9 MB each, EN + ಕನ್ನಡ
```
Total **~81 MB, 92 files** → fits GitHub web upload (limit: 100 files / commit).

## Steps
1. Unzip `branham-reader-gz.zip`.
2. Repo → **Add file ▾ → Upload files** (or the “uploading an existing file” link).
3. Drag **reader.html, messages-list.html, the two .md files and the `data` folder** at once.
4. Wait for all ✔ → message `reader + data` → **Commit changes**.
5. Settings → **Pages** → Branch **main**, folder **/(root)** → Save.
   - Reader: `https://feelitmeandu-cloud.github.io/messageinkannada/reader.html`
   - List:   `https://feelitmeandu-cloud.github.io/messageinkannada/messages-list.html`
6. Blogspot → Pages → New page → HTML view:
```html
<iframe src="https://feelitmeandu-cloud.github.io/messageinkannada/reader.html"
        style="width:100%;height:100vh;border:0" loading="lazy" referrerpolicy="no-referrer"></iframe>
```

## Notes
- The message list is **inside reader.html** — it appears instantly even before any data loads.
- Paragraph text loads per message (`data/parts/part-0xx.json.gz`), unzipped in the browser.
- `DATA_BASE` in reader.html controls where parts live:
  - `"./"` (same folder), Pages URL, or jsDelivr:
    `https://cdn.jsdelivr.net/gh/feelitmeandu-cloud/messageinkannada@main/`
- If the web upload still fails, use **GitHub Desktop** (clone → copy files → commit → push).
