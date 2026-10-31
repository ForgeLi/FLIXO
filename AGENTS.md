# AGENTS.md

Non-obvious setup notes for this repository (FLIXO).

## What this is
A plain static site: `index.html`, `style.css`, `script.js`. No package manager, no
build step, no backend, no database. All posts/state live in the browser's
`localStorage` under the key `flixo_demo_posts_v1` (seeded from `starterPosts` in
`script.js`), so there is nothing server-side and no credentials to configure.

## Running it (sandbox / local)
```bash
docker compose -f docker-compose.base44.yml up -d --build
```
- Serves the working copy from the repo root on host port `3000` with
  `python -m http.server` (repo bind-mounted at `/app`), so file edits show up on
  refresh — no image rebuild needed when editing HTML/CSS/JS.
- Fonts come from Google Fonts over the network; the app still renders without them
  (falls back to system sans-serif).

## Verifying it works
- `curl -sS -o /dev/null -w '%{http_code}' http://localhost:3000/` → `200`
- In the UI: feed shows 3 seeded posts; liking a post bumps the count and persists
  across reload; "Create post" adds a post to the top of the feed; the bookmark fills
  the Saved view; search with no match shows the empty state; nav switches
  Home/Explore/Saved/My profile; layout has no horizontal overflow at 375px.

## Notes
- There is no live-reload dev server (static files), so after a change refresh the
  preview (or call `reload_preview`) to see it.
- Tests/linting: none configured in the repo.
