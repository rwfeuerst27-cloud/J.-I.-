# Daily Inspection — install & deploy

Pen-first daily jobsite inspection app. Scribble with the S-Pen, tap the OK/N/A/D
boxes, flatten to a clean PDF, and send it to Drive. Works offline. Installs to the
home screen / DeX desktop like a real app.

## Files
- `index.html`        — the whole app
- `manifest.json`     — home-screen identity (icon, name, standalone launch)
- `service-worker.js` — offline caching (runs with no signal in the trench)
- `icon-192.png`, `icon-512.png` — app icons

All five files must sit in the SAME folder.

## Why it has to be hosted (not opened as a file)
Service worker, install, and the share-sheet all require a secure origin (HTTPS).
`file://` will not work. Use any free static host. Two easy ones:

### Option A — GitHub Pages
1. Make a repo, drop all 5 files in the root, commit.
2. Repo → Settings → Pages → Source: `main` / root → Save.
3. URL appears in ~1 min: `https://<you>.github.io/<repo>/`

### Option B — Cloudflare Pages
1. dash.cloudflare.com → Workers & Pages → Create → Pages → Upload assets.
2. Drag the 5 files in → Deploy. URL is instant.

## Install on the Tab S9 (DeX or tablet)
1. Open the URL in Chrome **or** Samsung Internet.
2. Menu (⋮) → **Add to Home screen** / **Install app**.
3. Launch from the icon — it opens full-screen, no browser bar.

## Daily flow
- Tap icon → scribble fields with S-Pen, tap OK/N/A/D, sign at the bottom.
- Trackpad/finger taps operate the boxes and focus a field to TYPE (pen stays default).
- **Ctrl+S** (or the orange **Save → Drive** button) flattens everything to PDF and
  fires the share sheet → pick **Drive** → choose your inspection folder. Drive
  remembers the folder, so it's one tap after the first time.
- Auto-named: `Inspection_<date>_<project>.pdf`.
- **New** clears the form for the next morning. Entries auto-save as you go, so a
  crash or accidental close never loses the sheet.

## Toolbar
- **Pen: S-Pen / Any** — S-Pen-only capture (palm rejection) vs. let mouse/finger ink too.
- **Erase**, color swatches, width slider, **Undo** (Ctrl+Z), **Clear ink** (current page).

## Optional upgrade — silent auto-upload (Path 2)
The share sheet is one tap. If you ever want ZERO taps (PDF lands in a fixed Drive
folder automatically), that needs a one-time Google Cloud OAuth client + a pasted
client ID, and you maintain token refresh. Hook point is `saveShare()` in index.html.
Ask and I'll wire it.
