# eng-plate

Bookmarkable eng plate for **Ian Lapham (Fomo)**.

**Live:** https://ianlapham.github.io/eng-plate/

Dark, mobile-friendly static dashboard. One card per plate item with plain-English feature name, what it is, what to do, status badge, and PR/Slack links.

## Layout

- `docs/index.html` — single-page UI (GitHub Pages from `/docs` on `main`)
- `docs/data.json` — machine-readable plate sections (also mirrored at repo-root `data.json` for agents)
- Source of truth for content: weekday plate brief `tracking/board.md` on the eng agent

## Sections

- Needs you
- Ready — yours
- Ready — others
- In progress
- Park
- Decisions / not started

Filters: All / Needs you / Review / Decisions.

## How PM should refresh `data.json` on plate briefs

After each weekday plate brief (or any material plate change):

1. Read the latest `tracking/board.md` from the eng agent tracking folder.
2. Update **both**:
   - `/workspace/plate-dashboard/data.json`
   - `/workspace/plate-dashboard/docs/data.json`  
   (keep them identical; the Pages site loads `./data.json` from `/docs`).
3. Set `lastUpdated` / `lastUpdatedIso` from the board header (e.g. `Fri Sep 25, 2026 ~10:51am ET`).
4. For each plate item, keep:
   - `title` — feature name (never bare `#NNNN`)
   - `description` — 1–2 sentences
   - `action` — what Ian should do
   - `status` / `statusLabel` — badge
   - `repo` — `app` | `web` | `fomo` | `slack`
   - `primaryLink` — main PR or Slack URL (or `null`)
5. Commit and push to `main` as `ianlapham`:

```bash
cd /workspace/plate-dashboard
git add data.json docs/data.json docs/index.html README.md
git commit -m "chore: refresh eng plate $(date '+%Y-%m-%d')"
git push origin main
```

Pages usually updates within a minute or two. Hard-refresh the live URL if the browser caches `data.json`.

## Repo

- https://github.com/ianlapham/eng-plate
- Public. No secrets. PR links to `github.com/fomo-family/...` are fine.
