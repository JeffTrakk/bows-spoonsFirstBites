# Bows and Spoons — First Bites

Companion app for the Bows and Spoons First Bites infant allergy testing kit. Guides a parent
through a multi-day home food-introduction protocol, logs reactions, records paediatric visits,
and keeps emergency contacts one tap away.

**Not a medical device.** It does not diagnose allergy. Clinician instructions always take
precedence over anything shown in the app.

## Running it

No build step, no dependencies to install. Serve the folder over HTTP and open the page:

```
python3 -m http.server 8000
# then visit http://localhost:8000/Bows%20and%20Spoons%20First%20Bites.dc.html
```

(Opening the file directly with `file://` will fail — the runtime fetches sibling files.)

A prebuilt single-file version that works offline with no server lives at
`export/Bows and Spoons First Bites (standalone).html`.

## Component library & website

`index.html` at the repo root is an **interactive, mobile-friendly component library** —
every component in the design system, live: clickable buttons with toasts, a working
segmented control and radios, tap-to-copy colour swatches and tokens, a status-voice
switcher, a live watch-window timer, a modal dialog, and the standalone app embedded in a
phone frame. It's a static, zero-dependency page (the design tokens are inlined; icons are
an inline SVG sprite), so it runs anywhere you serve the folder.

```
python3 -m http.server 8000
# component library:  http://localhost:8000/
# the live app:       http://localhost:8000/app/
```

### Deploy to Vercel

The repo is a static site — no build step. Either:

- **Dashboard** — import the GitHub repo at [vercel.com/new](https://vercel.com/new);
  Framework Preset **Other**, no build command, output directory `.` (root). Deploy.
- **CLI** — `npm i -g vercel` then `vercel` from the repo root.

`vercel.json` sets clean URLs and cache headers. After deploy: `/` is the component
library and `/app` is the live First Bites app.

## Layout

| Path | What it is |
| --- | --- |
| `index.html` | Interactive component-library website (the Vercel homepage) |
| `vercel.json` | Static-deploy config — clean URLs and cache headers |
| `app/index.html` | The live standalone First Bites app, served at `/app` |
| `Bows and Spoons First Bites.dc.html` | The app source — markup, logic class and tweakable props in one file |
| `support.js` | Runtime that mounts the component (React, template compiler) |
| `design-system/` | First Bites design system — tokens, the component stylesheet, a living style guide and the written guide |
| `export/` | Prebuilt standalone HTML |

The app file has three parts: the template (markup between `<x-dc>` tags), a `class Component`
logic class holding all state and handlers, and a `data-props` JSON block declaring the
tweakable props (`defaultTake`, `startInSetup`, `startDay`).

## Screens

- **Setup** — kit activation, baby profile, protocol choice, first contact and home address.
- **Today** — the current dose step, in either a focus card or a full checklist, with a live
  two-hour watch-window timer.
- **Plan** — the 24-day ladder across eight allergens, three doses each.
- **Log** — symptom chips, severity picker with severity-specific guidance, photo attachment,
  feed/sleep/nappy diary.
- **Visits** — appointment prep summary, growth and visit history, and a visit logger with
  measurements, percentiles, milestones and an audio note.
- **Care** — unlimited medical contacts with one-tap dialling and the emergency action plan.

An emergency bar with a 911 dial and the reaction plan is pinned to every screen.

## Known stubs

These are prototype placeholders, not finished behaviour:

- **Recording and transcription** — no microphone access; the recorder simulates a waveform and
  inserts a canned transcript. Wire to the Web Speech API or an on-device model.
- **Persistence** — all state is in memory and resets on reload. No storage layer yet.
- **Clinician chat** — the care-team panel is a placeholder for the future nurse connection.
- **Protocol content** — allergen list, dose amounts and day counts are illustrative and must be
  replaced with the kit's real clinical protocol before any real use.
- **Percentiles** — typed in as the clinician reads them out. The app never computes them from a
  growth chart, by design.
