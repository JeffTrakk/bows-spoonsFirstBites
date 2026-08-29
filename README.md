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

## Layout

| Path | What it is |
| --- | --- |
| `Bows and Spoons First Bites.dc.html` | The whole app — markup, logic class and tweakable props in one file |
| `support.js` | Runtime that mounts the component (React, template compiler) |
| `_ds/nocturne-…/` | Nocturne design system — tokens stylesheet and component bundle |
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
