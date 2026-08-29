# First Bites Design System

The canonical design language of the **Bows and Spoons First Bites** app, derived
from the app itself. It builds on the existing **Nocturne** foundation
(`_ds/nocturne-…/`) and formalizes the layer Nocturne never documented but the app
depends on: the **health-status semantics**.

- **`tokens.css`** — the complete, source-of-truth token set. Link it, and take every
  colour, font, space, radius and shadow from a `var(--…)`. Never hard-code a value a
  token already carries.
- **`index.html`** — the living style guide. Open it in a browser (or view the published
  reference) to see the whole system rendered.

## What this is

A quiet, dense, dark interface for a parent working through a multi-day home
food-introduction protocol. The look is Nocturne — a near-neutral blue-grey ground,
Inter at 500, an 8px grid at 0.70× density, a single blurple accent (`#9184d9`) used as
a line and a glow rather than a flood, and rules that fade to transparent at their ends.

What makes it a *medical companion* rather than a generic dark app is the semantic layer.

## Health-status semantics — the First Bites layer

In a home allergy protocol, colour is not decoration; it tells a parent whether to carry
on, watch closely, or call 911. Three voices, each a **first-class role** — never the
accent, never each other:

| Role | Base | Text-on-dark | Meaning in the app |
| --- | --- | --- | --- |
| **Success** (safe) | `--color-success` `#5FAE87` | `--color-success-300` `#9FD6BB` | Dose taken, watch window clear, tolerated. |
| **Caution** (mild) | `--color-caution` `#D0A05C` | `--color-caution-300` `#E6C48D` | Mild reaction, review pending, watch running. |
| **Danger** (severe) | `--color-danger` `#D9736A` | `--color-danger-100…400` | Reaction plan, 911, severe symptoms. |

Each role carries a `-tint` (10–12% fill) and `-edge` (34% hairline) for the app's
standard status surface: a tinted background, a hairline inset border, and a light-step
text colour on top. Danger additionally carries `--color-danger-ink` (`#1B1015`) — the
only place text sits **on** a filled semantic surface (the 911 button).

### Rules

- Reserve each voice for its meaning. Danger is the emergency, never a highlight or a
  brand pop. Never style a status with the accent, and never borrow one semantic's colour
  for another.
- Danger is **the one filled button** in the system — because in an emergency it must win.
  Every other action is an accent outline.
- Semantics are separate from the accent hue and do not count as the accent.

## Foundation quick reference

- **Colour** — dark ground `#161826`, surface `#232532`, ink `#e9e9ed`, accent `#9184d9`.
  Each role has a 100–900 OKLCH ramp on a shared lightness scale; contrast comes from
  value, not saturation. No pure black or white.
- **Type** — Inter for headings (weight 500) over Inter for body. Hierarchy is size and
  space; never bolden headings past 500.
- **Spacing** — `--space-*`, density 0.70×, dense on purpose. Radius 4 / 8 / 14px.
- **Elevation** — a hairline edge plus ambient darkness (`--shadow-sm/md/lg`); don't
  stack heavy shadows.
- **Icons** — [Phosphor](https://phosphoricons.com), regular and fill.
- **Motion** — two signatures: `fb-halo` (the 3.4s emergency-button pulse) and `fb-rise`
  (an 8px opacity enter).

## Using it

```html
<link rel="stylesheet" href="design-system/tokens.css">
```

```css
.reaction-surface {
  background: var(--color-danger-tint);
  box-shadow: inset 0 0 0 1px var(--color-danger-edge);
  color: var(--color-danger-100);
}
.dose-taken { color: var(--color-success-300); }
```

## Relationship to Nocturne

Nocturne (`_ds/nocturne-…/styles.css` + `readme.md`) remains the foundation and the
component layer (`.btn`, `.card`, `.tag`, `.input`, `.seg`, `.table`, `.dialog`, `.hr`,
`.lighten`). This folder does not replace it — it names the product's semantic colours
and the app-specific patterns (alert bar, dose card, watch-window timer, status pills)
built on top, so they stop living only as inline styles inside the app file.

---

**Not a medical device.** This app does not diagnose allergy. Clinician instructions
always take precedence over anything shown in the app.
