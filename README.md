# CR Attendance (Static PWA)

This project is a static Progressive Web App (PWA) that can be deployed to any static host.

## Project structure

- `index.html` – app UI + JavaScript logic
- `manifest.json` – PWA metadata
- `service-worker.js` – offline caching

## Prerequisites

- A static hosting platform (Netlify, Vercel, GitHub Pages, Cloudflare Pages, etc.)
- HTTPS enabled (required for full PWA behavior outside localhost)

## Run locally

```bash
python3 -m http.server 8080
```

Open: `http://localhost:8080`

## Deploy (generic)

1. Push repository to your Git provider.
2. Create a new site/project in your static hosting platform.
3. Configure as a static site:
   - **Build command:** none
   - **Output / publish directory:** `.` (repo root)
4. Deploy.

## Deploy with common platforms

### Netlify

- New site → Import from Git
- Build command: *(empty)*
- Publish directory: `.`

### Vercel

- Add New Project → Import repo
- Framework preset: **Other**
- Build command: *(empty)*
- Output directory: `.`

### GitHub Pages

- Repository Settings → Pages
- Source: deploy from branch
- Branch: `main` (or your default branch), folder `/ (root)`

## Backend/API note (important)

This frontend calls Google Apps Script endpoints already hardcoded in `index.html` (`APPSCRIPT_URL`, `ROSTER_URL`, `ROSTER_SECRET`).

If you change backend deployment, update these constants before releasing.

## Post-deploy verification

1. Open deployed URL.
2. Confirm these files are reachable:
   - `/manifest.json`
   - `/service-worker.js`
3. Open browser DevTools → **Application**:
   - Manifest is detected
   - Service worker is registered and active
4. Perform one attendance flow (login/load roster/submit) to verify Apps Script connectivity.

## Updating after deployment

1. Commit and push changes.
2. Host auto-redeploys.
3. If stale assets appear, do a hard refresh once to update service worker cache.
