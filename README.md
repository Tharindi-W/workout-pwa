# Workout Tracker PWA

A mobile-first Progressive Web App for tracking gym sessions with progressive overload logging. Built as a personal project — no frameworks, no backend, no dependencies.

![PWA](https://img.shields.io/badge/PWA-ready-brightgreen) ![Offline](https://img.shields.io/badge/offline-capable-blue) ![No deps](https://img.shields.io/badge/dependencies-none-lightgrey)

## Live Demo

https://extraordinary-salmiakki-a8bce7.netlify.app/
## Features

- **5 workout sessions** — 2 upper body, 2 lower body, 1 cardio/abs
- **Progressive overload tracking** — last session's sets shown alongside current for every exercise
- **Week navigation** — browse any past or future week
- **Overload hints** — per-exercise guidance on when to increase weight based on rep ranges
- **Offline-first** — full service worker caching, works with no internet after first load
- **Export / import** — CSV export for spreadsheet analysis, JSON for full backup and restore
- **Installable** — add to home screen on Android (Chrome) and iOS (Safari) as a standalone app
- **Zero dependencies** — plain HTML, CSS, and vanilla JS; no build step required

## Tech Stack

| Layer | Choice |
|---|---|
| Frontend | Vanilla HTML / CSS / JavaScript |
| Storage | `localStorage` (browser-native) |
| Offline | Service Worker (Cache API) |
| Install | Web App Manifest (PWA) |
| Hosting | Netlify (static, free tier) |
| Build | None — single HTML file |

## Project Structure

```
workout-pwa/
├── index.html        # Entire app — UI, logic, session data
├── sw.js             # Service worker for offline caching
├── manifest.json     # PWA manifest (name, icons, theme)
├── icons/
│   ├── icon-192.png  # PWA icon (Android home screen)
│   └── icon-512.png  # PWA icon (splash screen)
└── README.md
```

## Getting Started

### Run locally

No server needed for basic use — just open `index.html` in a browser.

For full PWA functionality (service worker, offline mode), serve over HTTP:

```bash
# Python
python3 -m http.server 8080

# Node
npx serve .
```

Then open `http://localhost:8080`.

### Deploy to Netlify

1. Fork or clone this repo
2. Go to [netlify.com](https://netlify.com) and create a free account
3. Drag and drop the `workout-pwa` folder onto the Netlify dashboard
4. Your app is live at `yourapp.netlify.app`

### Install on phone

- **Android (Chrome):** tap the three-dot menu → "Add to home screen"
- **iPhone (Safari):** tap the share icon → "Add to Home Screen"

## Data Management

All data is stored in the browser's `localStorage`. Use the in-app menu (⋮) to:

- **Export CSV** — opens in Excel/Google Sheets; one row per set
- **Export JSON** — full backup including all weeks and sessions
- **Import CSV / JSON** — restore from any backup file

> Tip: export a JSON backup weekly to avoid data loss if you clear your browser.

## Session Structure

| Session | Focus |
|---|---|
| Session 1 | Upper body day 1 — bench, shoulder press, lat pulldown, rear delt, supersets |
| Session 2 | Lower body day 1 — squats, leg press, lunges, leg curl, calves |
| Session 3 | Cardio + abs — treadmill sprints / jog alternating weekly, optional abs circuit |
| Session 4 | Upper body day 2 — incline press, rows, Arnold press, pulldown, curls |
| Session 5 | Lower body day 2 — hip thrust, Bulgarian split squat, RDL, leg extension |

## Progressive Overload Logic

Each exercise targets a rep range based on movement type:

- **Heavy compounds** (squats, hip thrusts, bench): 6-10 reps
- **Rows and pulldowns**: 8-12 reps
- **Shoulder and isolation work**: 10-15 reps
- **Rear delt, flies, calves**: 12-20 reps

Rule: if you exceed the top of the range across all sets, increase weight next session. If you cannot hit the bottom of the range on set 1, drop weight. Stay at current weight and add reps until you hit the top, then progress.

## License

MIT — free to use, fork, and adapt.
