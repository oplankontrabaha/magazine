# OKB App — launcher for the Oplan Kontra Baha web app

A tiny website that turns the OKB Apps Script link into an **installable app**:
a home-screen icon, a menu of the four pages, and each page opening full-screen
inside the app. Nothing is copied — every page is the live `/exec` web app.

## Launch it (about 3 minutes)

1. On GitHub, click **New repository**. Name it `okb` (any name works). Keep it **Public** — GitHub Pages is free only for public repos. Click **Create repository**.
2. Click **uploading an existing file** (or **Add file → Upload files**). Drag in **all 8 files** from this folder. Click **Commit changes**.
3. Go to **Settings → Pages**. Under *Build and deployment*, set **Source: Deploy from a branch**, **Branch: `main`**, folder **`/ (root)`**. Click **Save**.
4. Wait a minute or two, then refresh the Pages screen. Your app address appears at the top:
   `https://<your-username>.github.io/okb/`

That address is the app. Open it on a phone:
- **iPhone:** Safari → **Share** → **Add to Home Screen**.
- **Android:** Chrome shows an **Install** button in the app's header (or ⋮ → *Install app*).

## What is in this folder

| File | What it is |
|---|---|
| `index.html` | The app: header, menu of the four pages, and the full-screen frame that shows the live web app. The `/exec` link is at the top of its `<script>`, in `CONFIG`. |
| `manifest.webmanifest` | Tells phones the app's name, colours and icon so it can be installed. |
| `sw.js` | Keeps the menu available offline. The live pages still need internet. |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | App icons (Android / desktop). |
| `apple-touch-icon.png` | App icon for iPhone and iPad. |
| `README.md` | This guide. |

Keep all files in the root of the repo — no folders.

## Links the app understands

The app has its own short links. `?page=` picks a page; anything after `#` is
passed to the page as a route.

```
https://<you>.github.io/okb/                      the menu
https://<you>.github.io/okb/?page=duo             OKB Magazine
https://<you>.github.io/okb/?page=monitor         Project Monitoring
https://<you>.github.io/okb/?page=2               Waterway Magazine (PDF export)
https://<you>.github.io/okb/?page=mapping         Regional maps
https://<you>.github.io/okb/?page=duo#regionvi/iloilo/waterway/buntatala-creek
```

## Changing things

- **New `/exec` link** (only if you create a *new deployment* in Apps Script): open `index.html`, change `exec:` inside `CONFIG`, commit. Editing an existing deployment to a *new version* keeps the same link, so nothing to change.
- **Force phones to pick up a changed `index.html`:** in `sw.js`, change `okb-shell-v1` to `okb-shell-v2`, commit.
- **VIP (no-password) mode:** `CONFIG.vipWord` is empty on purpose. If you fill it in, *everyone* who finds this public site skips the password, and the word is readable in the page source. Only do that in a private setting, and remember the launcher can be shared just like the VIP link.

## If a page refuses to open inside the app

Use the **Open in browser** button in the header. The web app must be deployed
with **Who has access: Anyone** (not "Anyone with a Google account") for it to
work inside the frame — Google sign-in screens cannot be shown inside another
site.
