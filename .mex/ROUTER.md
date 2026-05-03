# Chicken Kings Vault — Project State

## What This Is

Unblocked games site. Hundreds of games in `gamefiles/`, catalogue in `games.js` (const template literal of `.game-link` anchors), served as a static site.

## Key Files

| Path | Purpose |
|---|---|
| `index.html` | Main page — game grid, search, tag filter, suggestions shelf, music widget |
| `games.js` | Full game catalogue as HTML template literal (`const games`) |
| `assets/app.css` | All styles for the main page |
| `assets/app.js` | Search, tag filter, suggestion algorithm, music player, SW registration |
| `proxy.html` | Scramjet web proxy browser UI |
| `sw.js` | Service worker — imports Scramjet worker from `/cdn/scramjet.worker.js` |
| `gamefiles/*.html` | Individual game pages (iframe wrappers) |
| `favicon.png` | Site logo/favicon |

## Infrastructure

- `/cgi/` — WISP WebSocket server (handled by backend team)
- `/cdn/` — BARE HTTP server + Scramjet client bundle files (handled by backend team)
- `/service/` — Scramjet proxy prefix (URL rewriting)

## Suggestion Algorithm (`assets/app.js`)

Reads `ckv_history` from localStorage (array of `{href, title}` objects, max 60 entries). Builds a tag-frequency map from recent plays, scores unplayed games by tag overlap, shows top 8 in the "picked for you" shelf. Tags derived from title keyword matching via `tagKeywords` map. Shelf only shows when history has 2+ entries.

## Music Player

`tracks` array at top of `assets/app.js`. Empty by default. Drop `.mp3` files into `/audio/` and add paths to the array to enable. Widget dims itself when no tracks configured.

## Adding Games

Add new entry to `games.js` template literal following existing `.game-link` pattern. Add corresponding `gamefiles/gamename.html` iframe wrapper.

## Patterns

See `.mex/patterns/` (none yet — add as patterns emerge).
