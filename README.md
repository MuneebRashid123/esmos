# ESMOS - School Management Platform

Static web app (HTML + CSS + JavaScript). No build step needed.

## Files
- `index.html` - page structure
- `style.css` - all styling
- `script.js` - all app logic (portals, fees, attendance, results, ratings)
- `favicon.png` - site icon
- `.nojekyll` - tells GitHub Pages to serve files as they are

## Deploy on GitHub Pages
1. Create a new repository on GitHub (for example `esmos`).
2. Upload all files from this folder to the repository root (Add file > Upload files), then Commit.
3. Open Settings > Pages. Under "Build and deployment" set Source to "Deploy from a branch", Branch to `main` and folder to `/ (root)`, then Save.
4. After about a minute your site is live at `https://YOUR-USERNAME.github.io/esmos/`.

## Demo logins
Open the site, tap "Try live demo", choose a portal. The demo credentials are pre-filled on each login screen.

## Notes
- Data is stored in the browser (local mode), so it stays on each device.
- Fonts load from Google Fonts, so an internet connection is needed for the exact look.
