# AGENTS.md

## Cursor Cloud specific instructions

### What this project is
A static, single-file HTML website ("Voodoo Clam Clan" — a New Orleans trip planning site). There is **no build step, no package manager, and no dependencies** to install. The only runtime needed is Python 3 (already present) to serve the files over HTTP.

The site lives in `vcc/`:
- `vcc/index.html` — main landing page (hero, countdown, itinerary, map, pay breakdown)
- `vcc/form.html` — the RSVP / commitment form (core interactive functionality)
- `vcc/diary.html` — page-flip "diary" storybook

### Running the site (dev)
Serve from **inside `vcc/`** — asset paths (`clam_logo.png`, `assets/images/...`) are relative to that directory, so serving from the repo root will break images/links:

```
cd vcc && python3 -m http.server 3333
```

Then open `http://localhost:3333/index.html`. Note: `.claude/launch.json` specifies `python`, but only `python3` exists on this VM — use `python3`.

### Testing notes (gotchas)
- **Do NOT actually submit `form.html` during testing.** It POSTs to a live external endpoint (`formsubmit.co`, defined by `VCC_FORM_ENDPOINT` in the page) which sends a real email. Fill fields to verify behavior, but don't click the final submit/send button.
- There are **no lint, automated test, or build commands** for this repo — verification is manual (serve + load pages in a browser / `curl` the URLs).
- `index.html` has a `var PHASE` flag near the top of its `<script>` that toggles `.phase-3-only` sections; changing it controls which sections are visible.
