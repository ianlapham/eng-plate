# eng-plate

Bookmarkable eng plate for **Ian Lapham (Fomo)**.

**Live:** https://ianlapham.github.io/eng-plate/

Dark, mobile-friendly static dashboard. **One card per feature**, grouped by simple lifecycle status — not ownership buckets.

## Layout

- `docs/index.html` — single-page UI (GitHub Pages from `/docs` on `main`)
- `docs/data.json` — machine-readable plate (also mirrored at repo-root `data.json` for agents)
- Source of truth for content: weekday plate brief `tracking/board.md` on the eng agent

## Status model (feature lifecycle)

| Status | Meaning |
|--------|---------|
| **Needs you** | Must act now — merge, review, reply, decide, design |
| **Started** | Work in flight — drafts, owning wire-ups, waiting on device/design |
| **Not started** | No PR / not kicked yet |
| **Parked** | Explicitly parked, HOLD, standing skip, or no-op |

Filters: **Needs you + Started** (default) · All · Needs you · Started · Not started · Parked.

Do **not** use the old Ready yours / Ready others ownership buckets. Deduplicate overlaps into a single feature card (prefer **Needs you** if Ian must act now, and mention progress in the body — never duplicate the card).

## Card fields

- `id`, `title` — plain-English feature name (never bare `#NNNN`)
- `description` — 1–2 sentences what/why
- `action` — optional “Do …” line (Merge / Review / Design / Wait …)
- `status` / `statusLabel` — `needs-you` \| `started` \| `not-started` \| `parked`
- `repo` — `app` \| `web` \| `fomo` \| `slack`
- `primaryLink` / `secondaryLinks` — PR / Slack / Notion with human labels (or `null`)

Omit done clutter (e.g. swaps → trades DONE) unless it still needs a Notion checkbox clear — prefer leave it off.

## How PM should refresh `data.json` on plate briefs

After each weekday plate brief (or any material plate change):

1. Read the latest `tracking/board.md` from the eng agent tracking folder.
2. Update **both**:
   - `/workspace/plate-dashboard/data.json`
   - `/workspace/plate-dashboard/docs/data.json`  
   (keep them identical; the Pages site loads `./data.json` from `/docs`).
3. Set `lastUpdated` / `lastUpdatedIso` from the board header.
4. Map items into the four lifecycle sections; merge duplicates into one feature card (~25–30 cards max).
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
